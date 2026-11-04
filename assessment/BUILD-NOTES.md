# Build notes

## Scope and evidence

- Assessment: three product docs, a published article describing the Thally build, and three brief observations.
- Product: Monnify DevKit v0.4.0, product commit `34a9943`.
- Product source: https://github.com/Tawakalt10/monnify-devkit
- Docs repository: https://github.com/Taofiqq/monnify-devkit-docs
- Site: https://monnify-devkit.thally.app
- User completed Cloud onboarding, installed the GitHub App, created a public docs repository, skipped optional Product sources and Knowledge surfaces, and published the starter.
- Screenshot evidence supplied in the conversation shows the initial deployment as Live and the initial starter readiness at 89/100. That score describes the starter, not the authored docs.

## Documentation decisions

- Audience: developers integrating Monnify with terminal and HTTP familiarity.
- Quickstart outcome: a signed simulated SUCCESSFUL_TRANSACTION reaches the scaffold's Express handler and is accepted.
- Practical guide: inspector on port 4400 forwards to the handler on port 3000; diagnose secret mismatch and replay an event.
- Use `.env` with `node --env-file=.env server.js`. The generated `npm start` does not load `.env` itself.
- Explain the distinction between receiver ACK and forwarding result; the receiver returns 200 even when the app returns 401 or is unreachable.
- Identify simulation as local; no payment is created by trigger.
- Keep Monnify's official API docs as the API reference; replace the starter's unrelated JSONPlaceholder example.
- Put the Part 2 article at its own URL and tab, separate from the three product pages.

## Verification performed

- Product source: 11 existing tests passed; typecheck and build passed.
- Installed the published `monnify-devkit@0.4.0` under a temporary prefix and verified its reported version.
- Isolated test config via a test-only Node preloader overriding `os.homedir()`; no user credentials or local event history were read or changed.
- Scaffolded an Express handler and installed its dependency.
- Confirmed signed trigger -> handler returns 200 and logs the exact reference.
- Confirmed inspector HTML and live SSE payload, valid signature and forwarded 200.
- Confirmed replay retains the payload's transaction reference.
- Confirmed wrong handler secret produces receiver ACK 200, downstream 401, and handler bad-signature log.
- Confirmed stopped handler still produces receiver ACK 200 and a forward-failed log.
- Did not exercise live Monnify login or create real sandbox API payment requests. Review the login step manually with sandbox credentials before submission.
- Test artifacts are outside the repository at `/private/tmp/monnify-docs-check.IGBSKd/`; only synthetic values are used.

## Thally setup observations

- First deployment succeeded through Cloud onboarding, with a visible Live status and source repository.
- Fresh-repository setup required All repositories GitHub App access per the Thally quickstart.
- The shell's default Node 23.11.0 did not match the starter's supported engine range. Used installed Node 22.14.0 for site installation and validation.
- The first network approval review timed out; retrying the repository clone succeeded. This was a local agent environment issue, not a Thally issue.

## Thally validation and preview

- Pinned Thally CLI 0.8.120: `thally check --ci .` passed with 0 errors and 0 warnings.
- `npm run typecheck` passed on Node 22.14.0.
- Production `npm run build` passed and generated the four authored page routes.
- Previewed the homepage, quickstart, debugging guide and build article in Chrome. Verified navigation, headings and code blocks.
- Non-fatal starter warnings: embedding prebuild skipped because its import hit the server-only boundary; Next warned about the parent-directory lockfile and deprecated middleware naming. Framework files were kept within their managed ownership boundary. These warnings did not stop the production build.

## Production verification

- Published content commit `3b480b4` to `main`.
- Thally Cloud Deployments showed the commit message as Current, Successful, and Production LIVE NOW / Healthy (duration 2m 29s).
- Opened the production homepage in Chrome and confirmed the new DevKit introduction and navigation.
- Fetched the production quickstart, debugging guide and build article with curl; all returned the expected authored content.
- Verified `/introduction` resolves to the canonical homepage content. Its Markdown output intentionally uses the frontmatter title rather than the visual Hero title.

## User review before submission

- Exercise sandbox login with your own credentials; the automated checks used synthetic credentials.
- Review the three product pages, build article and observations against your own experience.
