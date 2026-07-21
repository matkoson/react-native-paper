# Menu MD3 compliance audit (RNP-18)

Source of truth: callstack/react-native-paper#4977 checklist + M3 menus anatomy.

## Must-haves from #4977

| Spec item | Status | Evidence |
| --- | --- | --- |
| Container bg elevation level2 / surfaceContainerLow (standard) | Pass | utils.getMenuContainerColor |
| Item label onSurface | Pass | tokens.standardColors.label |
| Leading/trailing icon onSurfaceVariant | Pass | tokens.standardColors.icon |
| Disabled opacity 0.38 | Pass | getMenuItemColor contentOpacity |
| Selected tertiaryContainer / onTertiaryContainer | Pass | selected styles + tests + android/02 |
| Vibrant scheme (tertiaryContainer surface, tertiary selected) | Pass | colorScheme prop + android/03 |
| paddingVertical 8 container | Pass | Menu surface |
| Item min/max width 112/280 | Pass | MenuTokens.sizes |
| Item paddingHorizontal 12 | Pass | MenuItem |
| Icon→label gap 12 | Pass | MenuTokens |
| Item height 48 / dense 32 | Pass | fixed height when no supportingText |
| labelLarge title (was bodyLarge) | Pass | MenuItem + test |
| supportingText bodySmall | Pass | MenuItem + android/02 full "Insert clipboard" |
| trailingSupportingText labelLarge | Pass | MenuItem + android/02 full "⌘C" |
| Container corner.large (16) | Pass | getMenuContainerBorderRadius |
| First/last item corner.medium | Pass | Menu clones direct Menu.Item only |
| Selected item corner.medium | Pass | getMenuItemBorderRadius |
| Spring open/close + reduce-motion | Pass | toRawSpring in Menu show/hide |
| Composition-safe (type identity, no displayName) | Pass | Menu.tsx |

## Drift found + fixed this pass

1. **Supporting text clipped** — fixed height 48 with two-line anatomy. Fix: minHeight + paddingVertical when supportingText set.
2. **Trailing shortcut zero-width** — content minWidth starved trailing flex. Fix: intrinsic row (alignSelf flex-start, flexGrow 0 content, flexShrink 0 trailing).
3. **Example missing vibrant** — added "Vibrant color scheme" menu.

## Deferred (stretch / not required for baseline)

- Menu.Section / group gaps (Divider still used)
- Badge, submenu, shape morph

## Screenshots

Android (Pixel 9 Pro XL, API emulator, existing example APK + Metro):

- android/00-menu-example-closed.png
- android/01-menu-with-icons-open.png
- android/02-menu-selected-supporting.png
- android/03-menu-vibrant.png
- android/04-menu-bottom.png

iOS: sim booted + app installed; idb tap blocked (SimulatorKit missing from active Xcode). Screenshots pending once HID works.

## Tests

- Menu + MenuItem: 33 passed
