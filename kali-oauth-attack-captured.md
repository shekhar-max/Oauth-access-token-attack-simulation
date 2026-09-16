# OAuth 2.0 App Attack & Detection Lab

An end-to-end, multi-zone homelab simulation demonstrating an **Illicit Consent Grant / OAuth App Phishing Attack**. This project showcases how cybercriminals exploit trusted Identity Providers (IdPs) via social engineering to bypass Multi-Factor Authentication (MFA) and establish long-term account persistence, alongside modern Network and Host-based SIEM detection engineering methodologies.

---

## 🌐 Network Topology & Architecture
The environment simulates an enterprise segmentation model partitioned into four primary zones behind a central firewall running NAT:

*   🟥 **Attacker Zone (Kali Linux - 192.168.40.2):** Hosts the rogue phishing application infrastructure.
*   🟦 **DMZ Zone (Ubuntu/Windows - 192.168.10.2):** Acts as the employee/victim machine navigating the web.
*   ⬜ **Applications Zone (Ubuntu Server - 192.168.20.3):** Runs containerized production identity infrastructure.
*   🟦 **SIEM Zone (Splunk Host - 192.168.20.3:8000):** Consumes logs via Suricata IDS for threat hunting.

---

## 🛠️ Lab Component Stack

### 1. Identity Provider (Applications Zone)
Deployed **Keycloak (v24.0.0)** via Docker to act as the corporate authorization server:
```bash
sudo docker run -d -p 8082:8080 --name keycloak \
  -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin \
  quay.io/keycloak/keycloak:24.0.0 start-dev --hostname-strict=false --http-enabled=true
```
*   **Target Realm:** `master`
*   **Victim Credentials:** `victim` / `password123`
*   **Registered Client ID:** `malicious-app`
*   **Valid Redirect URI:** `http://192.168.40`

### 2. Rogue Application Infrastructure (Attacker Zone)
A lightweight **Python Flask** web server hosted on Kali Linux running within a sandboxed virtual environment. It dynamically crafts standard OAuth2 authorization links requesting wide-scope permissions (`openid profile email`) and captures callback codes to exfiltrate account access tokens.

---

## 💥 Execution & Exploit Flow
1. **Phishing:** The victim (DMZ) visits the attacker's server at `http://192.168.40.2:5000`.
2. **Redirection:** The victim clicks "Login with Corporate Keycloak" and is redirected to the legitimate enterprise server on port `8082`.
3. **Consent Grant:** The victim authenticates and clicks "Accept" on the OAuth permissions screen.
4. **Exfiltration:** Keycloak routes the Authorization Code back to Kali (`/callback`). The Python backend instantly swaps the code for a permanent JWT access token, achieving persistence without needing the account password.

---

## 🔍 Detection Engineering & Threat Hunting

### Suricata Network IDS
Suricata passively monitors traffic across network zones and intercepts raw unencrypted HTTP streams passing authorization codes and application details over the wire.

### Splunk Enterprise SIEM
Splunk ingests Suricata's JSON syslog events to trace the metadata of the attack lifecycle.

#### Simple Analytical Query:
```spl
index=* "malicious-app" 
| table _time, host, source, _raw
```

#### Incident Report Extraction Query:
```spl
index=* "malicious-app"
| rex field=_raw "client_id=(?<client_id>[^&\s\"]+)"
| rex field=_raw "src_ip\":\"(?<src_ip>[^\"]+)"
| rex field=_raw "dest_ip\":\"(?<dest_ip>[^\"]+)"
| rex field=_raw "http_user_agent\":\"(?<user_agent>[^\"]+)"
| table _time, src_ip, dest_ip, client_id, user_agent
| sort - _time
```

---

## 🛡️ Remediation & Mitigations
*   **Enterprise Scoping Rules:** Enforce tenant-wide policies preventing unverified or non-admin-approved apps from requesting user data.
*   **Session Revocation:** Administrators can terminate an active compromise by heading to the IdP administration panel -> **Users** -> **Consents** -> Select App -> Click **Revoke**.
