# Monnify DevKit documentation

Task-focused documentation for [Monnify DevKit v0.4.0](https://github.com/Tawakalt10/monnify-devkit), built and published with Thally Cloud.

- [Live documentation](https://monnify-devkit.thally.app)
- [Build article](https://monnify-devkit.thally.app/articles/build-docs-with-thally)
- [Assessment links and observations](assessment/submission.md)
- [Build and verification notes](assessment/BUILD-NOTES.md)

## Audience and content

The product docs help developers receive and debug a signed simulated Monnify webhook:

1. `src/content/introduction.mdx`: purpose, audience and scope.
2. `src/content/quickstart.mdx`: installation, sandbox login, scaffolding and a verified first event.
3. `src/content/guides/debug-webhooks.mdx`: inspector, forwarding diagnostics, secret mismatch and replay.

The separate build article is in `src/content/articles/build-docs-with-thally.mdx`.

## Run locally

Use Node.js 22.14+ in the 22.x series, or Node.js 24+, and npm.

```bash
npm ci
npm run dev
```

Open http://localhost:3040. Read `AGENTS.md` before editing. Pages live in `src/content/`, navigation in `docs.json`, and site identity in `src/data/site.ts`. Framework internals are managed by the Thally starter release.

## Validate

```bash
npm run check -- --ci
npm run typecheck
npm run build
```

For the pinned CI validation tool:

```bash
npm ci --ignore-scripts --prefix .github/thally-tooling
.github/thally-tooling/node_modules/.bin/thally check --ci .
```

## Publish

Push a reviewed commit to the `main` branch connected to Thally Cloud, then inspect Deployments and verify the live pages.

## Verification boundary

The published DevKit v0.4.0 package was tested locally with synthetic credentials in an isolated profile: signed delivery, inspector/SSE, forwarding, replay, wrong-secret rejection and unreachable-handler diagnosis. Live Monnify authentication was not exercised. The account login step requires manual verification before assessment submission.

## License

[MIT](LICENSE)
