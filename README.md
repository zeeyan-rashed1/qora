# QORA — Cloudflare Workers Static Assets

This repository is prepared to deploy the supplied single-file QORA website as a static-asset Cloudflare Worker.

## Structure

- `public/index.html` — QORA website
- `wrangler.jsonc` — Cloudflare Workers static-assets configuration

## Cloudflare dashboard settings

For the existing `qora` Worker connected to this GitHub repository:

- Root directory: `/`
- Build command: leave empty
- Deploy command: `npx wrangler deploy`
- Production branch: `main`
- Preview builds: enabled (optional)
- Cloudflare Access protection: disabled for a public website

The `wrangler.jsonc` file tells Wrangler to publish the contents of `public/` as static assets. No framework build step is required for this single-file HTML edition.

## Deploy

Commit and push these files to the `main` branch. The connected Cloudflare Worker build should then run `npx wrangler deploy`.

## Important production checks

- The HTML contains a Supabase project URL and a Supabase publishable key. A publishable key is intended for browser use, but Supabase Row Level Security (RLS) and policies must protect every table and storage bucket.
- Never add a Supabase `service_role` key, database password, OAuth client secret, or other private credential to `public/` or any public GitHub repository.
- This package publishes the supplied HTML as-is. It does not independently verify every interactive feature, authentication callback, database policy, email flow, or external API.
- The current HTML includes a local-mode feedback fallback. A hosted feedback service must be configured separately if public feedback submissions are expected to reach an administrator.
