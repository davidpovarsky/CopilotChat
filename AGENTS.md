# CopilotChat Agent Notes

## Signed macOS deploys

- When deploying `CopilotChatMac.app` to `/Applications`, always use a properly signed build.
- Do not deploy a build created with `CODE_SIGNING_ALLOWED=NO` to `/Applications`.
- An unsigned/ad-hoc deploy changes the app identity and can break OAuth persistence because the app loses the expected keychain/iCloud entitlements.
- For deploy builds, use normal Xcode signing so the app keeps:
  - `Authority=Apple Development`
  - `TeamIdentifier=MW4GWYGX56`
  - `keychain-access-groups`
  - iCloud / ubiquity entitlements

## Safe deploy checklist

- Build `CopilotChatMac` without disabling code signing.
- Before replacing `/Applications/CopilotChatMac.app`, verify the built app is signed.
- After copying to `/Applications`, verify:
  - `codesign -dv --verbose=4 /Applications/CopilotChatMac.app`
  - `codesign -d --entitlements - /Applications/CopilotChatMac.app`
- If an unsigned app was deployed by mistake, tell the user clearly that OAuth/keychain state may appear lost because of the bad deploy method.

## Living Project Board

`PROJECT_BOARD.md` is this repository's shared living project board. Before starting substantial work, scan it for relevant context. During normal work, agents should proactively add concise, actionable entries when they discover something with genuine future value, including:

- useful technical discoveries
- optimization opportunities
- implementation tricks
- architectural ideas
- possible future improvements
- experiments worth running
- unresolved issues or questions
- follow-up work that should not be lost

Do this proactively even when the discovery is incidental to the current task. Do not add trivial observations, temporary debugging chatter, information already documented elsewhere, generic suggestions with no project relevance, or every step performed during a task. The board supports memory but is not a source of truth when repository code, documentation, or current state contradicts it.

When an item is implemented, mark it complete and optionally record the date and commit/PR, moving it to `Done` when useful. Delete or archive obsolete entries when appropriate.

Updating `PROJECT_BOARD.md` as a side effect of another task is allowed and encouraged when a worthwhile discovery is made. Recording an idea is allowed; implementing unrelated ideas is not.

Preserve all existing repository-specific instructions.
