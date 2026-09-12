# Proof of Concept: The Unknown Server (APK Analysis)

| Field | Detail |
|---|---|
| Challenge | The Unknown Server |
| Category | Reverse Engineering |
| Difficulty | Hard |
| Points | 85 |
| Evidence | `evidence.zip` → `evidence.apk` |
| Status | Solved |

## 1. Scenario

A victim downloaded an Android application from an unknown source. The application initially appeared harmless, but investigation established that it was covertly forwarding OTP messages without authorization. The recovered evidence was the application's APK file.

## 2. Objective

Statically analyze the APK to determine the server IP address and port it communicates with, and report them in the required format `FLAG{SERVER_IP:PORT}`.

## 3. Methodology

- APK/ZIP extraction (APKs are standard ZIP archives containing compiled DEX bytecode)
- String analysis of the DEX files for application-specific class and configuration names
- Identification of the relevant configuration class and its static fields
- Base64 decoding of an obfuscated, fragmented server address

## 4. Investigation Steps

### Step 1 — Extract the evidence
The evidence archive (`evidence.zip`) contained `evidence.apk`. Both were extracted using standard `unzip`:

```bash
unzip evidence.zip
unzip -q evidence.apk -d evidence_extracted
```

### Step 2 — Locate the relevant application code
The APK contained multiple DEX files. Searching `classes3.dex` for application-specific identifiers revealed a custom package and class:

```
Package: com.devicesync.service
Class:   com/devicesync/service/GatewayProfile
```

### Step 3 — Identify the communication port
`GatewayProfile` contained several configuration fields, including `ROUTING_PORT`, `TRANSPORT_MODE`, and `SESSION_ID`. Searching the DEX strings for the routing configuration confirmed:

```
ROUTING_PORT = 8443
```

### Step 4 — Recover the obfuscated server IP
The server address was not stored as plaintext, but split across three separate Base64-encoded string fragments embedded in the class:

```
My44MC
4xNDU
uMjc=
```

Concatenated in the order referenced by the application code:

```
My44MC4xNDUuMjc=
```

Decoding this value:

```bash
echo 'My44MC4xNDUuMjc=' | base64 -d or cyberchef web
```

returned:

```
3.80.145.27
```

### Step 5 — Construct the flag
Combining the recovered IP and port per the required `FLAG{SERVER_IP:PORT}` format:

```
FLAG{3.80.145.27:8443}
```

## 5. Evidence Summary

| Field | Value |
|---|---|
| Application package | com.devicesync.service |
| Configuration class | GatewayProfile |
| Server port | 8443 |
| Server IP (fragments) | `My44MC` + `4xNDU` + `uMjc=` → `My44MC4xNDUuMjc=` |
| Decoded server IP | 3.80.145.27 |

## 6. Conclusion

The server's communication details were recovered entirely through static analysis — no execution of the malicious application was required. The port was stored as a plain configuration constant, while the IP address had been deliberately split across three separate Base64 fragments, presumably to evade simple string-based detection. Reassembling and decoding the fragments in the order the application itself references them was the key step.

## 7. Flag

```
FLAG{3.80.145.27:8443}
```
