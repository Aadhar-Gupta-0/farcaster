# farcaster — Verified Polls

A Farcaster Frame polling experiment with poll creation, four voting options, results and Vercel KV storage.

## Security and correctness improvements
- **Fail-closed voting:** the vote handler requires \`HUB_URL\` and \`HOST\`; arbitrary \`untrustedData.fid\` values are no longer accepted as votes.
- Validates frame action host origin rather than checking a potentially spoofable string prefix.
- Bounds and validates poll IDs before constructing storage keys.
- Persists the normalized poll form fields (the prior server action wrote the unmodified poll stub).
- Requires a title and two non-empty options; limits each field length to 150 characters.

## Setup
\`\`\`bash
npm ci
npm run dev
\`\`\`
Copy \`.env.example\` to \`.env.local\` and configure Vercel KV, your public \`HOST\` URL, and a trusted Farcaster \`HUB_URL\`.

**Unconfigured hub = voting unavailable.** This is intentional: a visual demo must not claim votes are authenticated when they are not. The application is based on an early Farcaster Frames example; verify API compatibility before using it in production.

## Caveats
- Additional rate limiting, replay protection, poll access controls, KV atomic vote transactions and automated integration tests remain necessary before public use.
- Existing Farcaster Frames protocol versions have evolved; validate current client compatibility before deployment.
- Original MIT license and upstream attribution are retained.

Adapted from [ethglobal/farcaster-poll](https://github.com/ethglobal/farcaster-poll); maintained as \`Aadhar-Gupta-0/farcaster\`.
