# Webhook Signature Validator & Troubleshooter

A single-file, client-side tool to verify a payment webhook / HMAC signature, **auto-detect the actual scheme behind a mismatch**, and **analyse recurring failures across integrations** to surface patterns — the #1 integration bug in payments, troubleshot at scale.

**Live:** https://tiwarivault.github.io/webhook-signature-validator/

## What it does
- Paste a webhook payload + signing secret, pick the scheme (HMAC-SHA256/512/1 or a plain SHA hash), choose hex or base64
- Computes the signature with the browser's **Web Crypto** API and compares it to a received signature → **MATCH / MISMATCH**
- **Auto-diagnosis:** on a mismatch, it tries every scheme × encoding and tells you the *actual* one that reproduces the signature (e.g. "it's HMAC-SHA512/base64, not SHA256/hex") — or flags a wrong secret / modified body when nothing matches
- **Batch / multi-integration analysis:** paste many failed verifications as JSON → it auto-detects each one's real scheme and surfaces the recurring **patterns** across integrations (e.g. "acme uses base64, globex signs with SHA-512"), with optional AI recommendations
- "Load sample (match)", "Mismatch example" and "Load sample batch" buttons demo every path

## Deterministic core vs AI assist
Signature verification **and the auto-diagnosis / pattern detection are deterministic** — reproducible crypto, not a model guessing. That's the point: you never want AI deciding whether a signature is valid. The **AI is optional** and sits on top, turning the detected patterns into context-aware recommendations and a prioritised fix.

Crypto + pattern detection = exact math; the "what to do about it across integrations" = AI assist.

## Privacy
100% client-side. The secret and payload never leave your browser. AI mode sends only the scheme name (never the secret) to Anthropic with your own key.

## Note
Ships with fake demo values only. Portfolio project by Prashant Tiwari (payments support → AI).
