# iOS page objects (Wikipedia, `org.wikimedia.wikipedia`)

One file per page action in `ios/pages/`: onboarding, launch, tab bar, search, article, contents, saved, crash guard.
Selectors are accessibility ids / labels seen on the live app (iPhone simulator, iOS 27.2, 2026-11-25).

- Maestro treats ids and text as regular expressions: escape or replace parentheses.
- `onboarding_complete` relaunches the app after **Skip** (the tab bar ids are missing otherwise; see the comment
  in the file). Use it only when onboarding itself is under test.
- `search_assert_clean_start`, `search_assert_no_results_absent` and `nav_assert_tabs_hidden` hold the checks tests use.
- `app_launch_skipping_onboarding` uses the app's own UI-test launch argument for the setup of all other tests.
