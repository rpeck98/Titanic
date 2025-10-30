sequenceDiagram
    participant A as Attacker (EvilProxy Operator)
    participant V as Victim
    participant P as Phishing Site (EvilProxy Reverse Proxy)
    participant S as Legitimate Service (e.g., Microsoft 365)

    A->>V: Sends phishing lure (e.g., email/SMS with fake link)
    V->>P: Clicks link, enters credentials (username/password)
    P->>S: Forwards request with victim's credentials (real auth)
    S->>P: Returns MFA challenge (e.g., push notification to victim's device)
    P->>V: Mirrors MFA prompt (e.g., fake push or code entry)
    V->>P: Submits MFA response (e.g., approves push or enters code)
    P->>S: Forwards real MFA response
    S->>P: Issues session cookie/token (authenticated session)
    P->>V: Serves fake "success" page + injects stolen cookie
    P->>A: Exfiltrates credentials + session cookie
    A->>S: Uses stolen cookie to access victim's account (bypasses MFA)
    Note over A,S: Attacker now has persistent access
