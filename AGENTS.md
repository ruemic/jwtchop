# jwtchop

**Decodes any JWT token into its header, payload claims, and signature — entirely in the browser.**

## What it does

jwtchop is a browser-side JWT (JSON Web Token) decoder. Paste any JWT and instantly see:
- **Header** — algorithm (alg) and token type (typ)
- **Payload** — all claims, with standard claims labeled (sub, iss, aud, exp, iat, nbf, jti)
- **Signature** — raw base64url signature string
- **Token status** — valid, expired, expiring soon, or not yet active

No data leaves the browser. No server requests. No logging.

## Input format

A JWT is three base64url-encoded JSON objects joined by dots:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIn0.abc123
```

Any valid JWT with three dot-separated parts is accepted, regardless of algorithm.

## Output

The tool renders four panels in the UI:
1. Header JSON (algorithm + type)
2. Payload JSON (all claims, time claims shown with human-readable date)
3. Raw signature string
4. Token status (expiry countdown, active/expired/not-yet-active)

## How an agent can use it

**Browser-side only (current tier):** Navigate to `https://jwtchop.radicchio.page` and paste the JWT into the textarea. The tool decodes immediately on input — no form submission needed.

**Deep link:** Append the JWT to the URL hash to auto-decode:
```
https://jwtchop.radicchio.page#<JWT_TOKEN>
```

**Planned API (Tier 2):** A future Cloudflare Worker will expose:
```
POST /api/decode
Content-Type: application/json
{"token": "<JWT>"}

→ {"header": {...}, "payload": {...}, "signature": "...", "expired": false}
```

## Pricing

Free. No signup required. The decoder will always be free and browser-side.

Planned paid tier: JWT signing/verification, batch decode, webhook inspector — $9/month.

## Privacy guarantee

jwtchop does not send tokens to any server. All base64url decoding is done with browser-native JavaScript. Verify in DevTools → Network tab: zero requests on token input.

## Support

Contact: https://bitterdesk.com
