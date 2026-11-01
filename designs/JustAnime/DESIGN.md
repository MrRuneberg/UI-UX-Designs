# JustAnime-inspired UI/UX design specification

## 1. Purpose and scope

This specification defines a reusable visual and interaction system inspired by [JustAnime](https://github.com/sankethodgar/JustAnime). It is intended for developers and coding agents building web or desktop interfaces.

The design character is cinematic, dark, image-led, information-dense without feeling crowded, and quick to navigate. Artwork and primary content carry the visual weight; interface chrome organises the experience without competing with it.

This is a design language, not a requirement to reproduce JustAnime's routes, anime catalogue, streaming features, or product structure. Apply media-specific patterns only when the product actually contains media. Use the shared foundations for other kinds of content.

## 2. Design principles

1. **Content leads.** Artwork, titles, and task-relevant information take priority over decoration.
2. **Dark and cinematic.** Use near-black foundations, restrained charcoal surfaces, subtle depth, and carefully controlled image overlays.
3. **Readable density.** Keep metadata compact, but never reduce essential text or controls to achieve density.
4. **Fast discovery.** Search, navigation, filters, and collections should be easy to find and operate.
5. **Consistent states.** Hover, focus, selected, loading, disabled, and error states use the same rules across components.
6. **Responsive composition.** Reflow content as space changes; do not shrink desktop layouts into cramped mobile versions.
7. **Purposeful motion.** Motion communicates state and spatial relationships. It is never required to understand or operate a control.
8. **Progressive detail.** Show essential information immediately and reveal secondary detail when requested.

## 3. Foundations and design tokens

### 3.1 Colour system

Use the following semantic tokens as the source of truth. Values are hex so they can be copied directly into CSS variables, design tools, or implementation themes.

| Semantic token | CSS property | Value | Intended use |
|---|---|---:|---|
| Background | --bg | #0A0A0A | Application and page canvas |
| Foreground | --fg | #FFFFFF | Main text and important icons |
| Surface | --surface | #171717 | Cards, panels, and contained content |
| Surface foreground | --surface-fg | #F5F5F5 | Text on contained surfaces |
| Elevated surface | --surface-elevated | #202020 | Menus, dialogs, and raised layers |
| Primary | --primary | #D1D1D1 | Main neutral action and selected emphasis |
| Primary foreground | --primary-fg | #111111 | Text and icons on primary controls |
| Primary hover | --primary-hover | #E5E5E5 | Hovered primary control |
| Muted surface | --muted | #242424 | Quiet controls and supporting regions |
| Muted foreground | --muted-fg | #B8B8B8 | Secondary text and metadata |
| Surface hover | --surface-hover | #303030 | Hovered rows and quiet controls |
| Border | --border | #262626 | Subtle card, panel, and divider boundaries |\n| Strong border | --border-strong | #666666 | Input boundaries and controls requiring a clear edge |
| Input | --input | #141414 | Recessed form-field fill |
| Ring | --ring | #E5E5E5 | Keyboard focus indicator |
| Danger | --danger | #FF6B6B | Destructive status and actions |
| Danger foreground | --danger-fg | #240707 | Text on danger fills |
| Success | --success | #55D6A1 | Successful status |
| Success foreground | --success-fg | #071D14 | Text on success fills |
| Warning | --warning | #FFD166 | Warning status |
| Warning foreground | --warning-fg | #241900 | Text on warning fills |
| Info | --info | #79B8FF | Informational status |
| Info foreground | --info-fg | #07182B | Text on info fills |
| Overlay | --overlay | rgba(0, 0, 0, 0.68) | Modal scrims; use directly as a translucent colour |

Rules:
- Use the neutral primary treatment for the principal action in a local context. Its text and icon colour is always --primary-fg; do not default to white text on a light button.
- Use near-white for primary reading text and --muted-fg for secondary information. Do not use muted text for instructions, errors, or essential status.
- Keep large surfaces close to the background. Use surface changes and borders to establish grouping rather than adding saturated colour.
- Semantic status colours are reserved for status and destructive meaning. Pair them with text or an icon.
- Place a local dark gradient or scrim behind text over artwork. Never assume an image provides consistent contrast.
- The reference palette is dark-only. If a light theme is later required, define and test a complete light semantic palette rather than mechanically inverting these values.

### 3.2 Typography

Use Geist Sans as the preferred interface family and Geist Mono for numeric, technical, or aligned data. Provide system sans-serif and monospace fallbacks.

| Style | Size / line height | Weight | Typical use |
|---|---:|---:|---|
| xs | 12px / 16px | 400–500 | Compact metadata, timestamps |
| sm | 14px / 20px | 400–500 | Supporting labels and controls |
| base | 16px / 24px | 400 | Body text and descriptions |
| lg | 18px / 28px | 500 | Card titles and lead copy |
| xl | 20px / 28px | 600 | Section headings |
| 2xl | 24px / 32px | 600 | Page titles |
| 3xl | 30px / 36px | 600–700 | Featured titles |
| 4xl | 36px / 44px | 700 | Large display titles, used sparingly |

Use medium or semibold weights for titles and interactive labels, regular weight for reading text, and compact sizes for secondary metadata. Do not use uppercase for paragraphs. Keep synopsis and description line lengths controlled. Clamp titles only when the complete title remains available elsewhere or through an accessible name.

### 3.3 Spacing scale

Use a 4px base unit. Select values from this scale rather than inventing unrelated gaps.

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

Use 8–12px for compact control groups, 16–24px for card padding, 24–32px between related content groups, and 32–48px between major page sections. Reduce outer gutters before reducing control hit areas on narrow screens.

### 3.4 Shape, borders, and elevation

| Token | Value | Use |
|---|---:|---|
| --radius-sm | 4px | Badges and compact elements |
| --radius-md | 8px | Inputs, buttons, and small cards |
| --radius-lg | 12px | Standard cards and menus |
| --radius-xl | 16px | Dialogs and large media surfaces |
| --radius-2xl | 24px | Featured containers when appropriate |
| --radius-full | 9999px | Pills and circular controls |
| --border-width | 1px | Standard boundary |
| --border-width-strong | 2px | Selected or emphasized boundary |

Prefer a border and small tonal shift over a large shadow for ordinary cards. Use a soft shadow only for layers that float above the page. Clip artwork to its container. Avoid nested card-on-card layouts.

### 3.5 Elevation

| Level | Treatment | Use |
|---|---|---|
| 0 | No shadow | Page canvas and ordinary content |
| 1 | 0 2px 8px rgba(0,0,0,.22) | Cards raised slightly from the canvas |
| 2 | 0 8px 24px rgba(0,0,0,.38) | Menus and popovers |
| 3 | 0 16px 48px rgba(0,0,0,.52) | Dialogs and media overlays |

Do not use elevation as the only indication of grouping or focus.

### 3.6 Motion tokens

| Token | Value | Use |
|---|---:|---|
| --motion-fast | 120ms | Press and small hover feedback |
| --motion-normal | 180ms | Buttons, tabs, and menu transitions |
| --motion-slow | 240ms | Dialogs and larger content transitions |
| --motion-ease-out | cubic-bezier(0.16, 1, 0.3, 1) | Entering and settling |
| --motion-ease-in-out | cubic-bezier(0.4, 0, 0.2, 1) | State changes and movement |

Prefer opacity and small transforms. Do not animate large layout changes or delay an action. Disable nonessential movement when reduced motion is requested.

## 4. Layout and navigation

### 4.1 Application frame

Provide a stable frame for brand, navigation, search, and primary content. Keep one consistent content boundary across pages. On wide screens, use available width for artwork, grids, and useful supporting columns; do not stretch reading text across the entire display.

### 4.2 Header and navigation

The reference uses a fixed top navigation containing brand, search, key destinations, and a compact menu on smaller screens.

- Keep the logo or wordmark in a stable position.
- Make search easy to reach from browsing contexts.
- Keep top-level destinations concise; put secondary destinations in a menu.
- Group account and utility actions separately from primary navigation.
- On compact screens, use a clear menu or compact navigation pattern rather than squeezing all labels into the header.
- If the header changes on scroll, keep the transition subtle and prevent layout jumps.
- In desktop applications, integrate with the host window deliberately. Do not duplicate native title-bar controls unless the product intentionally uses an accessible custom frame.

### 4.3 Page sections

Use section headings and consistent vertical rhythm to group collections. A section may include a restrained “view all” action. Most content sections should sit directly on the page background; reserve visible panels for modules that behave as distinct units.

### 4.4 Featured content

A featured area may use a wide landscape image as a backdrop.

- Preserve the source image's proportions and use cover cropping only when the crop remains intentional.
- Apply a dark gradient behind the text, strongest near the copy and fading toward the image focal point.
- Order content as compact metadata, title, optional alternate title, short description, then actions.
- Keep the text group in negative space and away from the focal subject.
- On narrow screens, shorten the description and stack actions.
- If the feature rotates, show position and controls, support keyboard input, pause autoplay after interaction, and respect reduced motion. Autoplay must never be the only way to discover an item.

## 5. Content and media patterns

### 5.1 Poster cards

Poster cards are a defining pattern when the product contains catalogue-style media.

- Use a 2:3 portrait ratio for poster artwork.
- Use cover cropping without stretching; keep the focal subject visible.
- Keep title and essential metadata outside the image in the standard card layout.
- Use compact dark-backed badges only for useful facts such as format, language, availability, or release status.
- Limit metadata beneath each poster. Put richer detail on a detail view.
- Use a subtle lift or scale on hover-capable devices, without shifting surrounding layout.

Touch and hover behaviour must be explicit:
- Tapping the card body opens its detail view.
- A separate play/open action is available as a visible control on touch layouts; do not hide the only route to that action behind hover.
- On pointer layouts, the overlay may reveal that same secondary action, but keyboard focus must reveal it too.
- If the card has only one action, make the whole card the action and do not add a redundant overlay button.

### 5.2 Horizontal rails

Use horizontal rails for collections that benefit from quick scanning.

- Keep card widths consistent within a rail.
- Support touch, trackpad, wheel, and keyboard scrolling where the platform permits.
- Use scroll snapping only when it improves alignment and does not trap users in forced paging.
- Directional controls appear only when useful and must reflect the rail's boundaries.
- Keep overflow discoverable; do not hide the only indication that more items exist.
- On narrow screens, reduce the number of visible cards rather than shrinking them below readable sizes.

### 5.3 Grids and lists

Use responsive grids for browsing and comparison. Derive columns from available width and card readability, not a fixed device label. Use lists for row-oriented information such as episodes, schedules, and rich search results. Align row content and separate rows quietly.

### 5.4 Detail views

Combine one dominant image with structured information.

- Use a poster or hero image as the visual anchor.
- An enlarged background image may be used at low opacity, fading into the canvas.
- Make the main title the strongest text; keep alternate titles secondary.
- Group rating, year, status, format, and availability into compact metadata.
- Use quiet tags for genres or classifications.
- Use tabs for genuinely distinct supporting sections, with a simple underline or border for selection.
- Let users expand truncated synopsis text.
- Keep related content connected to the detail view without competing with its primary information.

### 5.5 Playback

The player is a focused media surface. Video dominates; controls appear when needed.

- Use the correct media aspect ratio and a black player canvas.
- Group play/pause, timeline, volume, elapsed/total time, playback options, picture-in-picture, and fullscreen logically.
- Use a subtle gradient behind controls, not a large opaque toolbar.
- During active playback, controls may hide after inactivity; pause hiding while the user interacts.
- Touch users need an explicit way to reveal and dismiss controls.
- Distinguish played, buffered, and remaining timeline portions.
- Put quality, speed, audio, subtitles, and preview controls in compact menus.
- Distinguish loading, buffering, unavailable source, and playback failure. Provide retry or source selection when possible.
- Never let a spinner cover an error or block recovery.

## 6. Components and interaction patterns

### 6.1 Buttons

| Variant | Appearance | Use |
|---|---|---|
| Primary | Light neutral fill, dark foreground | Main local action |
| Secondary | Dark surface with subtle border | Alternative action |
| Tertiary | Text or minimal icon treatment | Low-priority action |
| Destructive | Danger semantic treatment | Irreversible or risky action |

Use clear verbs. Avoid multiple competing primary actions in one region. Icon-only buttons need accessible names and a tooltip where the meaning is not obvious. Provide default, hover, focus-visible, pressed, disabled, and pending states.

### 6.2 Inputs and forms

- Use a persistent label above or beside each field. A placeholder is supplementary example text, never the only label.
- Use a recessed input fill (--input), a strong boundary (--border-strong), and a distinct focus ring. Reserve --border for subtle card and divider structure.
- Support text, search, password, number, date, select, checkbox, radio, switch, and textarea controls with consistent sizing and state treatment.
- Group related fields with section labels and spacing.
- Place validation beside the affected field and explain how to correct the value.
- Preserve entered values after recoverable validation or network failures.
- Use helper text for format requirements and constraints before submission, not only after an error.

### 6.3 Search and filters

Search is a primary navigation tool.

- Use an explicit label or accessible name and a clear prompt describing searchable content.
- Show suggestions in an elevated surface with a clear boundary.
- Support arrow-key navigation, Enter to select, Escape to close, and pointer/touch selection.
- Provide loading, empty, and error states.
- Group filters by meaning, expose selected values after a menu closes, and provide a clear reset action.
- Preserve search and filter state while browsing results unless the user resets it.

### 6.4 Tabs, menus, and popovers

Use a simple underline or border for selected tabs. Expose selected state semantically and support the keyboard pattern for tabs. Menus use the elevated surface, modest shadow, and alignment to their trigger. Keep them within the viewport. Escape closes the menu; outside interaction may close it when safe.

### 6.5 Dialogs

Use the translucent --overlay scrim and a surface from the same palette. Provide a clear title, close action, and predictable action order. Move focus into the dialog, contain focus while modal, and restore focus to the trigger on close. Escape dismisses when safe. On narrow screens, adapt the dialog to available space rather than scaling down a desktop panel.

### 6.6 Badges, loading, and feedback

Badges communicate facts, not decoration. Use quiet dark backing over imagery. Skeletons approximate the shape of the content and remain low contrast. Empty states explain why content is absent and offer a next step when one exists. Errors must look distinct from empty states. Use concise inline feedback for local actions and unobtrusive toasts for transient events.

## 7. Responsive behaviour: web and desktop

### 7.1 Wide layouts

Use the full header, flexible grids, and optional supporting columns where they improve the task. Keep reading text at a controlled measure. Avoid fixed page widths.

### 7.2 Compact layouts

Reduce outer gutters first. Collapse secondary columns before compressing the main content. Move navigation into a compact menu or suitable persistent pattern. Stack featured actions and allow filter controls to wrap or open in a panel.

### 7.3 Desktop windows

Preserve the web visual language while respecting the host platform's window controls. Support resizing, zoom or system scaling, and smaller-than-default windows. Menus, dialogs, and media controls must not be clipped. Use native file pickers and system affordances when they improve the task. Do not use mobile bottom navigation in a spacious desktop window.

## 8. Accessibility and usability

- Use semantic landmarks and controls.
- Ensure every action is keyboard reachable with a visible focus indicator.
- Give icon-only controls accessible names.
- Associate labels, helper text, and validation messages with fields.
- Support keyboard operation for tabs, menus, rails, and media controls.
- Maintain readable contrast for text and meaningful control boundaries.
- Never communicate status or selection through colour alone.
- Provide meaningful alternative text for informative images; decorative images use empty alternative text.
- Provide captions for video when available.
- Respect reduced-motion preferences, browser zoom, and text enlargement.
- Keep touch targets comfortably operable.
- Do not disable text selection or browser zoom globally.

## 9. Iconography

Use a consistent simple line-icon family. Keep stroke weight and optical size consistent. Use the same icon for the same action throughout the product. Avoid emoji as substitutes for core interface icons. Decorative icons are hidden from assistive technology; controls carry the accessible name.

## 10. Implementation and adaptation guidance

- Centralise semantic colours, typography, spacing, radii, borders, elevation, focus, and motion.
- Build reusable primitives for buttons, fields, cards, tabs, menus, dialogs, badges, and feedback states.
- Keep content components composable.
- Do not add anime, streaming, schedule, or catalogue features to a product that does not need them.
- Do not copy source CSS defects or treat a reference implementation's accidental behaviour as a design requirement.
- If a pattern conflicts with the product's task, preserve the visual principles and choose a more suitable interaction.

## 11. Quality checklist

- [ ] The interface remains dark, cinematic, and content-led.
- [ ] Primary actions use dark foreground text on the light neutral primary surface.
- [ ] Semantic status colours have explicit foreground pairings.
- [ ] Type, spacing, radius, elevation, and motion follow the defined scales.
- [ ] Poster cards have an explicit touch interaction, not a hover-only action.
- [ ] Search, filters, forms, and media controls have complete states.
- [ ] Layouts reflow without fixed page widths or clipped controls.
- [ ] Keyboard, touch, reduced motion, zoom, and text enlargement are supported.
- [ ] The design adapts to actual product content instead of imposing JustAnime features.
