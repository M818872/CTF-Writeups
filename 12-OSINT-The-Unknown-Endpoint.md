# Proof of Concept: The Unknown Endpoint

| Field | Detail |
|---|---|
| Challenge | The Unknown Endpoint |
| Category | OSINT |
| Difficulty | Hard |
| Points | 100 |
| Status | Solved |

## 1. Scenario

Investigators recovered a suspicious Android application suspected of unauthorized data collection and covert remote communication. Static analysis showed the app contained embedded configuration data pointing to an external messaging platform.

## 2. Objective

Identify the external messaging service used by the application and determine the username of the automated account it communicates with.

## 3. Methodology

- Static extraction of the APK's resource files (no dynamic execution of the malware was required)
- Structured parsing of embedded JSON configuration
- Verification via the messaging platform's own public API (Telegram Bot API `getMe` endpoint)

## 4. Investigation Steps

### Step 1 — Extract the archive
The evidence was supplied as `Malware APK.zip`, containing an Android App Bundle (`Malicious.apks`) with `base.apk`, and additional split APKs. The archive was extracted with standard `unzip` commands.

### Step 2 — Locate the embedded configuration
`base.apk` contained a configuration file at `res/raw/admin_info.json`. Using Python for structured JSON parsing (rather than manual inspection), the first configured token was extracted:

```bash
TOKEN=$(unzip -p base.apk res/raw/admin_info.json | python3 -c 'import sys,json; print(json.load(sys.stdin)["tokens"][0])')
```

The token's format (beginning with a numeric bot ID, e.g. `8213545127...`) was consistent with a **Telegram Bot API token**. The full credential is withheld from this report for security reasons; it is retained separately in the case evidence should platform verification require it.

### Step 3 — Identify the automated account
The token was queried against Telegram's own public `getMe` endpoint, which confirms bot identity:

```bash
curl -s "https://api.telegram.org/bot${TOKEN}/getMe" | python3 -m json.tool
```

Relevant response:

```json
{
    "ok": true,
    "result": {
        "id": 8213545127,
        "is_bot": true,
        "first_name": "Newpanel",
        "username": "chandpanel_bot"
    }
}
```

## 5. Evidence Summary

| Field | Value |
|---|---|
| Configuration file | `res/raw/admin_info.json` (inside `base.apk`) |
| Messaging platform | Telegram |
| Bot username | `chandpanel_bot` |
| Verification method | Telegram Bot API `getMe` |

## 6. Conclusion

The application's remote-communication channel was identified purely through static analysis of its bundled resources — no execution of the malware was necessary. Telegram's own API was then used as an authoritative, first-party source to confirm the bot's identity, rather than relying on the token alone.

## 7. Flag

```
FLAG{chandpanel_bot}
```
