# Webhook Signature Validator

A single-file, client-side tool to verify a payment webhook / HMAC signature and diagnose mismatches — the #1 integration bug in payments.

**Live:** https://tiwarivault.github.io/webhook-signature-validator/

## What it does
- Paste a webhook payload + signing secret, pick the scheme (HMAC-SHA256/512/1 or a plain SHA hash), choose hex or base64
- Computes the signature with the browser's **Web Crypto** API and compares it to a received signature → **MATCH / MISMATCH**
- On a mismatch: a ranked list of likely causes + an optional AI explanation
- "Load sample (match)" and "Mismatch example" buttons demo both outcomes

## Deterministic core vs AI assist
Signature verification is **deterministic HMAC** — and it has to be; you never want a model guessing whether a signature is valid. The **AI is optional** and only assists on a mismatch, reasoning about your specific scheme and returning an ordered debug path.

Crypto = exact math; debugging the mismatch = AI assist.

## Privacy
100% client-side. The secret and payload never leave your browser. AI mode sends only the scheme name (never the secret) to Anthropic with your own key.

## Note
Ships with fake demo values only. Portfolio project by Prashant Tiwari (payments support → AI).
