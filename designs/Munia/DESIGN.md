# Munia-inspired UI/UX design specification

## 1. Purpose and scope

This specification defines a reusable visual and interaction system inspired by [Munia](https://github.com/leandronorcio/munia). It is intended for developers and coding agents creating web or desktop interfaces.

Munia's visual character is friendly, community-oriented, violet-led, rounded, and content-focused. Its reference patterns include a side navigation on wide screens, compact bottom navigation, feed-like cards, profile surfaces, comments, media viewing, and light and dark themes.

This is a design language, not a requirement to reproduce Munia's social-network feature set. Use profile, feed, comment, and media patterns only when the product has equivalent content relationships.

## 2. Design principles

1. **Human content first.** Give posts, identity, and media clear priority over application chrome.
2. **Violet with restraint.** Use violet for primary actions, active navigation, focus, and selected states, not for all body copy.
3. **Soft but structured.** Rounded surfaces and gentle elevation should clarify grouping without making every region a card.
4. **Readable identity.** Names, handles, biographies, and timestamps have distinct hierarchy.
5. **Predictable interaction.** Actions and states behave consistently across feeds, profiles, forms, and dialogs.
6. **Responsive navigation.** Use side navigation when space permits and a compact persistent pattern on narrow layouts.
7. **Theme parity.** Light and dark themes share semantic roles and comparable readability.
8. **Motion with purpose.** Animate meaningful transitions briefly and respect reduced-motion preferences.

## 3. Foundations and design tokens

### 3.1 Colour system

Use the semantic token names below in both themes. The hex values are normative starting points. Do not copy the reference's incomplete or low-contrast values blindly.

#### Light theme

| Semantic token | CSS property | Value | Intended use |
|---|---|---:|---|
| Background | --bg | #F6F2FA | Soft lavender page canvas, distinct from white cards |
| Foreground | --fg | #1D1424 | Main text |
| Surface | --surface | #FFFFFF | Cards and contained content |
| Surface foreground | --surface-fg | #25152F | Text on cards |
| Elevated surface | --surface-elevated | #FFFFFF | Menus, dialogs, popovers |
| Primary | --primary | #8800CA | Main action and selected emphasis |
| Primary foreground | --primary-fg | #FFFFFF | Text and icons on primary fills |
| Primary hover | --primary-hover | #6F00A8 | Hovered primary control |
| Muted surface | --muted | #EAE0F2 | Quiet controls and secondary panels |
| Muted foreground | --muted-fg | #5E5068 | Secondary text |
| Surface hover | --surface-hover | #E9DFF0 | Hovered quiet controls |
| Border | --border | #E2D6EC | Subtle card, panel, and divider boundaries |
| Strong border | --border-strong | #8A7B91 | Input boundaries and controls requiring a clear edge |
| Input | --input | #F2ECF7 | Recessed form-field fill |
| Ring | --ring | #6B00A8 | Keyboard focus indicator |
| Danger | --danger | #B42336 | Destructive status and actions |
| Danger foreground | --danger-fg | #FFFFFF | Text on danger fills |
| Success | --success | #147A4A | Successful status |
| Success foreground | --success-fg | #FFFFFF | Text on success fills |
| Warning | --warning | #8A5700 | Warning status |
| Warning foreground | --warning-fg | #FFFFFF | Text on warning fills |
| Info | --info | #175EA8 | Informational status |
| Info foreground | --info-fg | #FFFFFF | Text on info fills |
| Overlay | --overlay | rgba(24, 11, 36, 0.64) | Modal scrim; use directly as a translucent colour |

#### Dark theme

| Semantic token | CSS property | Value | Intended use |
|---|---|---:|---|
| Background | --bg | #100023 | Page canvas |
| Foreground | --fg | #FBF3FF | Main text |
| Surface | --surface | #231B38 | Cards and contained content |
| Surface foreground | --surface-fg | #FBF3FF | Text on cards |
| Elevated surface | --surface-elevated | #302544 | Menus, dialogs, popovers |
| Primary | --primary | #C77BFF | Main action and selected emphasis |
| Primary foreground | --primary-fg | #210035 | Text and icons on primary fills |
| Primary hover | --primary-hover | #D69AFF | Hovered primary control |
| Muted surface | --muted | #392D4A | Quiet controls and secondary panels, distinct from elevated surfaces |
| Muted foreground | --muted-fg | #D7C9E2 | Secondary text |
| Surface hover | --surface-hover | #403252 | Hovered quiet controls |
| Border | --border | #3D3054 | Subtle card, panel, and divider boundaries |
| Strong border | --border-strong | #806D91 | Input boundaries and controls requiring a clear edge |
| Input | --input | #171026 | Recessed form-field fill |
| Ring | --ring | #D9A5FF | Keyboard focus indicator |
| Danger | --danger | #FF8B9B | Destructive status and actions |
| Danger foreground | --danger-fg | #2B0710 | Text on danger fills |
| Success | --success | #65D6A0 | Successful status |
| Success foreground | --success-fg | #062217 | Text on success fills |
| Warning | --warning | #FFD27A | Warning status |
| Warning foreground | --warning-fg | #2B1A00 | Text on warning fills |
| Info | --info | #85BEFF | Informational status |
| Info foreground | --info-fg | #071A30 | Text on info fills |
| Overlay | --overlay | rgba(5, 0, 11, 0.72) | Modal scrim; use directly as a translucent colour |

Colour rules:
- Use --fg for ordinary body copy on the page and --surface-fg for copy on cards. Do not colour long-form posts or comments violet.
- Use --primary for the main action, selected navigation, focus, and active states. Do not use it as a default paragraph colour.
- Always pair --primary with --primary-fg. Do not assume white is legible on every violet shade.
- Use --border for restrained card, panel, and divider structure. Use --border-strong for input boundaries and controls that need a clear edge. Do not apply the strong value to every passive divider. Keep input fill distinct from elevated surfaces.
- Use muted text only for secondary information. Essential instructions and validation messages use readable foreground or semantic status colours.
- Status colours are semantic. Pair them with text or an icon and use the corresponding foreground token on filled status treatments.
- The dark popover and secondary surfaces must stay within the warm violet/plum family. Avoid unrelated blue-grey surfaces that look copied from a different theme.
- Keep theme switching consistent across all components. Do not animate a long crossfade that makes text temporarily hard to read.

### 3.2 Typography

Use Poppins as the preferred family for its friendly geometric character. Provide a robust sans-serif fallback. Use regular and medium weights for most interface text, semibold for headings and key labels, and bold sparingly.

| Style | CSS token | Size / line height | Weight | Typical use |
|---|---|---:|---:|---|
| xs | --text-xs | 12px / 16px | 400–500 | Timestamps and compact metadata |
| sm | --text-sm | 14px / 20px | 400–500 | Handles, labels, and secondary controls |
| base | --text-base | 16px / 24px | 400 | Posts, comments, and body copy |
| lg | --text-lg | 18px / 28px | 500 | Card and profile subheadings |
| xl | --text-xl | 20px / 28px | 600 | Section headings |
| 2xl | --text-2xl | 24px / 32px | 600 | Page titles |
| 3xl | --text-3xl | 30px / 36px | 600–700 | Profile and discovery headings |
| 4xl | --text-4xl | 36px / 44px | 700 | Rare display use |

Use natural casing. Keep posts, comments, and biographies readable at the base size. Use smaller text for timestamps and counts, not for essential instructions. Do not truncate user-generated content without an explicit expand affordance.

### 3.3 Spacing scale

Use a 4px base unit.

| Token | Value |
|---|---:|
| --space-1 | 4px |
| --space-2 | 8px |
| --space-3 | 12px |
| --space-4 | 16px |
| --space-5 | 20px |
| --space-6 | 24px |
| --space-8 | 32px |
| --space-10 | 40px |
| --space-12 | 48px |
| --space-16 | 64px |

Use 8–12px for compact identity and action groups, 16–20px for card padding, 20–24px between feed items, and 32–48px between major sections. On narrow layouts, reduce outer margins before reducing internal control spacing or hit areas.

### 3.4 Shape and borders

| Token | Value | Use |
|---|---:|---|
| --radius-sm | 4px | Badges and compact labels |
| --radius-md | 8px | Inputs and compact controls |
| --radius-lg | 12px | Standard cards and buttons |
| --radius-xl | 16px | Dialogs and larger surfaces |
| --radius-2xl | 24px | Profile and discovery surfaces |
| --radius-full | 9999px | Avatars, pills, and circular actions |
| --border-width | 1px | Standard boundary |
| --border-width-strong | 2px | Focused or selected boundary |

Rounded geometry is a defining trait, but not every element needs the largest radius. Use a consistent radius within each component family. Avatars remain circular. Inputs use rounded rectangles, not floating-label shapes that depend on placeholder behaviour.

### 3.5 Elevation

| Level | Treatment | Use |
|---|---|---|
| 0 | No shadow | Page canvas and ordinary content |
| 1 | 0 2px 8px rgba(28,0,45,.08) | Cards and subtle separation in light theme |
| 2 | 0 8px 24px rgba(20,0,35,.18) | Menus and popovers |
| 3 | 0 16px 48px rgba(8,0,20,.32) | Dialogs and media viewer |

In dark theme, reduce shadow reliance and use surface contrast and borders to define layers. Do not use shadow as a substitute for a visible boundary or focus indicator.

### 3.6 Motion tokens

| Token | Value | Use |
|---|---:|---|
| --motion-fast | 120ms | Button press and small feedback |
| --motion-normal | 180ms | Menus, tabs, and control state |
| --motion-slow | 240ms | Dialogs and content expansion |
| --motion-ease-out | cubic-bezier(0.16, 1, 0.3, 1) | Entering and settling |
| --motion-ease-in-out | cubic-bezier(0.4, 0, 0.2, 1) | Position and theme state changes |

Prefer opacity, small transforms, and controlled height changes for genuine expansion. Avoid elastic overshoot and layout shifts. Respect reduced-motion preferences.

## 4. Layout and navigation

### 4.1 Application shell

The reference uses persistent side navigation on wide layouts and a bottom navigation bar on compact layouts.

Wide layout:
- Place the brand mark and wordmark above the destination list.
- Keep the navigation visually quiet and stable.
- Give the main content the greatest visual weight.
- Use a consistent content alignment boundary.

Compact layout:
- Move primary destinations to a bottom bar or another persistent compact pattern.
- Centre and distribute icons evenly.
- Use a short horizontal violet marker for the active destination.
- Respect device safe areas and add content padding so the bar does not obscure controls.
- If there are too many destinations, use a deliberate overflow pattern rather than shrinking hit areas.

### 4.2 Navigation states

- Default: muted icon and label.
- Hover: subtle tinted surface or icon emphasis.
- Active: persistent violet marker and stronger label weight.
- Focus: visible focus ring with adequate contrast.
- Disabled: reduced emphasis and no misleading hover response.

The side rail uses a vertical active marker; the compact bottom bar uses a horizontal marker. Active state must be communicated by more than colour. Make the whole navigation item interactive.

## 5. Content surfaces and social patterns

### 5.1 Cards and feed items

Use rounded surfaces with consistent padding and predictable hierarchy. A card should make content easier to scan, not create another unnecessary layer.

A post-like item may contain:
1. Author row: avatar, display name, handle or context, timestamp, and optional actions.
2. Main text or rich content.
3. Optional media.
4. Action row with controls and counts.
5. Optional discussion or related content.

Keep the author row compact. The post content has the strongest priority. User-generated text wraps naturally. Mentions and hashtags may be interactive, but do not colour all body copy with the accent. Put edit and delete actions in a predictable contextual menu.

### 5.2 Comments and replies

Use avatar alignment and indentation to communicate hierarchy. Keep author name and timestamp close to the comment. Reaction and reply actions are compact. Indent replies enough to show relationship while preserving width on narrow screens. Provide clear expand/collapse labels. A deep-linked comment may receive a temporary accessible highlight.

### 5.3 Profiles and avatars

Avatars are circular and preserve source aspect ratio. Provide initials or a neutral mark when no image exists. Use meaningful alternative text when an image conveys identity; use empty alternative text when adjacent text already identifies the person.

Profile header:
- Use a wide cover image as context, not as a place for essential text.
- Overlap the avatar with the cover in a controlled way.
- Place the primary profile action near the identity block.
- Make display name strongest, followed by handle and biography.
- Keep counts secondary.
- Use a distinct profile tab row.
- Adapt avatar overlap and tabs on narrow screens without clipping controls.

Discovery cards may use a restrained tinted header region with a centred avatar and a body containing identity, biography, and counts. Do not turn context-specific or identity-coded colours into universal rules.

### 5.4 Media

Inline media stays within the content width, preserves intrinsic aspect ratio, and uses rounded clipping. Do not arbitrarily crop user uploads. For multiple assets, use a clear grid or carousel and provide an obvious route to the larger viewer.

The full-screen viewer reduces surrounding interface noise. Provide visible close and navigation controls, position information for multiple assets, keyboard navigation, and zoom/pan where useful. Video controls remain usable and captions are supported when available.

## 6. Components and interaction patterns

### 6.1 Buttons

| Variant | Appearance | Use |
|---|---|---|
| Primary | Violet fill with theme-appropriate primary foreground | Main local action |
| Secondary | Muted neutral fill | Alternative action |
| Outline | Transparent or surface fill with violet boundary/text | Visible lower-priority action |
| Ghost | Minimal surface | Icon actions and quiet controls |
| Destructive | Danger semantic treatment | Risky or irreversible action |

Do not place multiple competing primary actions together. Use pill shapes for prominent actions where appropriate and circular icon buttons for familiar single-purpose actions. Every icon-only control needs an accessible name. Provide default, hover, pressed, focus-visible, disabled, and pending states.

### 6.2 Inputs and forms

Use a recessed --input fill with a --border-strong boundary and a distinct focus ring.

- Place a persistent label above or beside the field. Do not use floating labels that begin as placeholder text.
- Keep the label visible and readable at all times.
- Use placeholder text only for examples or supplementary hints.
- Support text, search, password, number, date, select, checkbox, radio, switch, and textarea controls.
- Place validation beside the affected field and associate it programmatically.
- Preserve typed content after recoverable validation errors.
- Confirm before discarding meaningful unsaved composition.
- For attachments, show previews and obvious remove/reorder controls.

### 6.3 Dialogs, menus, and popovers

Dialogs use a rounded --surface-elevated surface with a clear title, content region, and action area, over the translucent --overlay scrim. Provide a close affordance. Move focus into the dialog, contain it when modal, and restore it to the trigger on close. Support Escape when dismissal is safe. Confirm before discarding meaningful unsaved work.

Menus and popovers use compact floating surfaces with readable labels and predictable spacing. Group related actions, use separators sparingly, distinguish destructive actions, and keep the panel within the viewport. A tooltip is never the only way to understand a control.

### 6.4 Notifications and feedback

Toasts use a semantic icon, concise title, optional message, and close action.

- Success uses the success semantic role.
- Warning uses the warning semantic role.
- Error uses the danger semantic role.
- Neutral or informational messages use a quiet neutral or info treatment.

Do not rely on colour alone. Important errors must remain available in the relevant screen and not disappear only with a toast.

Notification items communicate who or what caused the event, what happened, and when. Use an avatar or contextual icon, readable event text, and a small unread indicator. Distinguish read and unread states without overwhelming the content.

### 6.5 Loading, empty, and error states

- Loading: restrained spinner or skeleton that preserves expected layout.
- Empty: explain why the region is empty and offer a relevant next step when one exists.
- Error: state what failed in plain language and offer retry where useful.
- End of content: use a quiet completion message rather than unexplained blank space.

Avoid large flashing indicators for brief operations.

## 7. Responsive behaviour: web and desktop

### 7.1 Wide screens

Use side navigation when it improves orientation. Keep text-heavy content at a readable measure. Use extra width for secondary panels or multi-column discovery only when useful. Keep dialogs and media viewers proportionate.

### 7.2 Medium screens

Reduce outer margins. Collapse secondary columns before the main content becomes cramped. Preserve comfortable card padding and touch targets. Use compact navigation when the full rail no longer fits.

### 7.3 Narrow screens

Use compact or bottom navigation. Stack content into a primary column. Allow filters and action groups to wrap. Keep media within the viewport. Add bottom padding for persistent navigation. Keep important actions reachable without precision pointer movement.

### 7.4 Desktop applications

Keep navigation and content hierarchy consistent with the web version. Follow host-platform window controls unless a deliberate, accessible custom title bar is used. Support resizing and smaller-than-default windows. Ensure menus, dialogs, and popovers are not clipped. Use native file pickers and system affordances when they improve the task. Keyboard shortcuts are enhancements, not replacements for visible controls.

## 8. Accessibility and usability

- Use semantic HTML, landmarks, and controls.
- Make every interactive element keyboard reachable.
- Provide visible focus indicators.
- Give icon-only controls accessible names.
- Associate labels, helper text, and validation messages with fields.
- Manage focus correctly in dialogs and menus.
- Support keyboard operation for tabs, menus, media viewers, and navigation.
- Maintain sufficient contrast in both themes for text and meaningful control boundaries.
- Never communicate state through colour alone.
- Provide meaningful alternative text for informative imagery.
- Support captions for video when available.
- Respect reduced motion, browser zoom, and text enlargement.
- Keep touch targets comfortably operable.

## 9. Iconography

Use a consistent family of simple stroke-based icons. Keep stroke weight and optical size consistent. Use the same icon for the same action throughout the product. Avoid emoji as substitutes for core interface icons. Hide decorative icons from assistive technology and label the containing control.

## 10. Implementation and adaptation guidance

- Centralise semantic colour, typography, spacing, radius, border, elevation, focus, and motion tokens.
- Use the same semantic token names in light and dark themes.
- Build reusable primitives for buttons, icon buttons, inputs, textareas, badges, avatars, cards, tabs, menus, dialogs, toasts, and loading/empty/error states.
- Keep content components composable: a post is assembled from identity, content, media, and action regions.
- Do not force every screen into a card layout.
- Do not add social features merely because the reference contains them.
- Do not copy source CSS defects or incomplete semantic token sets.
- Adapt the violet-led visual language to the actual product's content and workflows.

## 11. Quality checklist

- [ ] Light and dark themes share the same complete semantic token taxonomy.
- [ ] Primary foreground pairings are explicit and readable.
- [ ] Card text uses foreground tokens, not saturated violet body copy.
- [ ] Borders are visible against both canvas and surface.
- [ ] Dark surfaces use a coherent warm violet/plum family.
- [ ] Form labels remain visible above or beside fields; no placeholder-only floating labels.
- [ ] Typography, spacing, radius, elevation, and motion follow the defined scales.
- [ ] Side and bottom navigation have clear, distinct active indicators.
- [ ] Posts, comments, profiles, and media remain readable at narrow widths.
- [ ] Loading, empty, error, and notification states are designed.
- [ ] Keyboard, touch, focus, zoom, text enlargement, and reduced motion are supported.
- [ ] Product-specific social features are not imposed on unrelated products.
