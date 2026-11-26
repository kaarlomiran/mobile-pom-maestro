# mobile-pom-maestro: Page Object Model for Maestro

Reusable, screen-scoped Maestro subflows ("page objects") shared by test repos.
Selectors live **only here**; tests call page actions and never touch raw selectors.
Maestro has no classes, so one YAML file = one page action.

```
android/pages/   onboarding, home, search (query, language, assertions), article, nav, saved, activity, language, crash guard   (done)
ios/pages/       onboarding, launch, tab bar, search, article, contents, saved, crash guard   (done, see ios/README.md)
```

## Conventions
- One file per page action: `<page>_<action>.yaml`, header `appId: ${APP_ID}`.
- Inputs are env vars (e.g. `QUERY`); document them at the top of each file.
- Prefer resource ids / accessibility text over visible text; no coordinates.
- Page actions end with an `assertVisible` proving they reached the expected state. Checks used by tests live in
  `<page>_assert_<state>.yaml`; the consuming repo's lint fails a test that contains its own selectors.
- On slow devices, wait for a screen (`extendedWaitUntil`) before conditional taps; a fixed number of early checks
  can run before the screen is drawn.
- Merge changes here before the consuming repo's pull request: its checks read this repo's `main`.
- Any change here must be validated by running the consuming repo's flows.

## Consuming
The test repo pins this repo in `pom.lock` and fetches it into `pom/` with `scripts/sync-pom.sh`.
Call from a flow: `- runFlow: ../../pom/android/pages/search_open.yaml`

Target app (Android): Wikipedia, package `org.wikipedia`. Selectors verified against the Maestro sample `wikipedia.apk` on an API 31 emulator.
