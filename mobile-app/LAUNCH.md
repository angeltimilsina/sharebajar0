# BAJAR research beta — release gates

This repo contains a functional Expo mobile **research beta**, not an operating brokerage or forex/crypto exchange. Existing prototype valuations, AI summaries, and price scenarios include illustrative/mock data; do not represent them as real-time licensed investment advice. Real-money order execution is not enabled.

## Build the beta

1. From the repository root, run the backend with `python server.py --host 127.0.0.1 --port 3000` locally and verify `/api/health`. Do not expose that development server directly to the Internet.
2. Provision a secure, monitored, HTTPS backend for beta accounts before external distribution. Enable production authentication, secrets, request limits, persistence, TLS, logging, and a privacy policy. Verify market data licensing for every data route. Never use research-only adapters as licensed execution data.
3. From `mobile-app/`, install dependencies with `npm ci` and run `npm run check`. Run `npx expo export --platform web` to verify the JavaScript bundle. CI checks this automatically.
4. Set the public Expo environment variable `EXPO_PUBLIC_API_URL` to the actual HTTPS beta backend origin **before** building device binaries. Never point a public binary to localhost or a placeholder URL. API tokens and passwords must never be in `EXPO_PUBLIC_*` variables.
5. Sign in to Expo/EAS and initialize the project: `npx eas-cli@latest init`. To share Android testing builds: `npx eas-cli@latest build --platform android --profile preview`. For iOS internal distribution: `npx eas-cli@latest build --platform ios --profile preview` with Apple Developer signing, registered devices, and required provisioning.
6. Test on actual Android and iOS devices: onboarding, market discovery, empty and failed provider states, account sign-in/out, watchlists, reports, keyboard/safe areas, VoiceOver, reduced-motion preference, sensitive data storage and network interruptions.
7. Only after successful device and security testing, use TestFlight / Google Play closed testing, obtain store approvals, and then consider public availability. Connect domain, monitored backend, support contact, and terms and privacy notices first.

**Known blockers:** Production HTTPS API origin, Expo project linkage, store signing credentials, release test evidence, and regulated service/market data partnerships. The `preview` and `production` EAS profiles alone do not deploy an app, create signing certificates, or confer regulatory authorization.
