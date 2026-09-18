# Changelog — FG Editor Switcher (plg_fgeditorswitcher)

## 2.3.2 — Removed UTF-8 BOM from five files
Fixed a byte-order mark at the start of the PHP class file (flagged by the
JED submission checker) plus four more affected files.

## 2.3.1 — JED-compliant extension name
Manifest name changed to `Editor - FG Editor Switcher`, matching JED's
required `{Type} - {Extension Name}` format. Language strings and
`updates.xml` updated to match.

## 2.3.0 — Content survives the switch
Major update, developed with a second-opinion review pass and verified
with JCE:
- Unsaved editor content is now carried over to the new editor instead of
  being lost on reload, with an automatic fallback to a confirmation prompt
  if the handover can't be completed.
- Selectors now set themselves up correctly for fields added later
  (subform rows, AJAX-loaded forms), not just on initial page load.
- Keyboard navigation (arrow keys) no longer triggers the confirmation
  dialog on every key press.
- Editor option labels show proper names (TinyMCE, CodeMirror, JCE) instead
  of `ucfirst()`.
- Dropdown arrow colour now matches the toolbar via CSS instead of a
  JS-rebuilt SVG.
- Removed two orphaned files left over from earlier versions.

## 2.2.2 — Reverted the joomla.asset.json migration
2.2.1's move to `media/joomla.asset.json` broke JS/CSS loading in
real-world testing; reverted to the previously working
`registerAndUseStyle()`/`registerAndUseScript()` calls.

## 2.2.1 — Packaging and manifest cleanup
- Added `<php_minimum>` to the manifest itself.
- Renamed the config field type to `fgeditors` to avoid a possible future
  naming collision.
- Plugin's cookie is now cleared on uninstall.
- Fixed a stale `LICENSE.txt` reference.
- Migrated assets to `joomla.asset.json` (reverted in 2.2.2).

## 2.2.0 — CSP-safe layout
Moved layout from inline `style="..."` attributes to CSS classes, so the
plugin still displays correctly under a strict Content-Security-Policy.

## 2.1.9 — More reliable scroll restoration
Scroll position is now restored after the page fully loads instead of on
`DOMContentLoaded`, so TinyMCE's asynchronous layout changes can no longer
undo it.

## 2.1.8 — Accessibility label + debounced keyboard input
Added an accessible name (`aria-label`/`title`) to the dropdown. Debounced
the change handler so keyboard arrow-key navigation no longer triggers a
confirmation dialog on every key press.

## 2.1.7 — Dropdown arrow colour now matches the toolbar
The arrow is now tinted to match the admin template's own toolbar button
colour instead of always being white.

## 2.1.6 — Avoid resubmitting a POST on switch
Switching editors now uses `location.replace()` instead of
`location.reload()`, avoiding a possible browser "resubmit form?" prompt.

## 2.1.5 — More robust toolbar matching
The selector now finds its own toolbar by DOM position relative to itself,
instead of assuming page-wide DOM order - fixing a possible mismatch on
complex pages.

## 2.1.4 — Stopped mutating Joomla's shared plugin cache
Building the editor list no longer writes into objects held in Joomla's
internal plugin cache.

## 2.1.3 — Safe fallback instead of an empty field
If no usable editor is available at all, a plain `<textarea>` is now shown
instead of an empty field, so content can't be silently lost.

## 2.1.2 — Lazy editor initialisation
Moved editor setup out of the constructor into a once-per-request method,
fixing duplicate warning messages and unnecessary work on every page.

## 2.1.1 — More natural confirmation dialog text

## 2.1.0 — Consolidated the version number into a single PHP constant

## 2.0.9 — Use `$this->params` instead of re-fetching the plugin config

## 2.0.8 — Guaranteed-unique selector ids
Selector ids are now guaranteed unique via a per-request counter, instead
of relying solely on a sanitised field name.

## 2.0.7 — Removed unused hidden input field

## 2.0.6 — More robust fallback when the "None" editor is disabled

## 2.0.5 — Fixed: cancelling the confirmation dialog left the wrong option shown

## 2.0.4 — Prevented the plugin from being able to switch to itself via a manipulated cookie

## 2.0.3 — Fixed a missing dropdown arrow on some admin templates

## 2.0.2 — Fixed language strings not translating
Root cause: the language files were misnamed relative to Joomla's required
`plg_<group>_<element>` pattern (2.0.1 had fixed the wrong thing).

## 2.0.1 — Attempted fix for language strings not translating
Superseded by 2.0.2, which found the actual root cause.

## 2.0.0 — Rebranded into the FG series
Renamed from `plg_editors_switcher` to `plg_fgeditorswitcher`: new
namespace, class, cookie, and element/JS/CSS identifiers; author/copyright
updated; language files consolidated to en-GB and sk-SK. Functionally
identical to the last release of the original plugin line.
