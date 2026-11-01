# Kryoto-inspired UI/UX design specification

## 1. Purpose and scope

This specification defines a reusable visual and interaction system inspired by [Kryoto Desktop](https://github.com/Kryoto-Dev/kryoto-desktop). It covers web interfaces, desktop applications, and products delivered on both platforms.

The goal is to preserve Kryoto's restrained, compact, technical character without reproducing its product screens, branding, or feature set. The product's own requirements determine its information architecture and workflows.

This document specifies design outcomes, not a mandatory framework or implementation stack.

## 2. Design principles

1. **Precise hierarchy.** Use typography, spacing, and contrast before decoration.
2. **Compact, not cramped.** Use space efficiently while preserving readable text and comfortable control targets.
3. **One emphasis at a time.** Reserve the strongest fill for the primary action or active selection in its local context.
4. **Quiet surfaces.** Prefer subtle surface differences and borders over nested cards and heavy shadows.
5. **Technical character.** Use restrained uppercase labels, deliberate tracking, clean line icons, and selected pill-shaped controls.
6. **Progressive disclosure.** Keep infrequent actions in menus or contextual controls.
7. **Platform-aware consistency.** Share the visual system across web and desktop while respecting native window conventions.
8. **Motion with meaning.** Use short feedback and state transitions; never rely on animation to communicate essential information.

## 3. Foundations and design tokens

### 3.1 Colour system

Use a near-black, OLED-inspired palette with a restrained teal primary accent. The exact values below are the normative starting palette; do not leave semantic roles to individual implementation guesses.

| Semantic token | CSS property | Value | Intended use |
|---|---|---:|---|
| Background | --bg | #080A0D | Main application canvas |
| Foreground | --fg | #F3F5F7 | Main text and important icons |
| Surface | --surface | #121820 | Panels and grouped content |
| Surface foreground | --surface-fg | #E8EDF2 | Text on surfaces |
| Elevated surface | --surface-elevated | #1A232D | Menus, dialogs, floating panels |
| Primary | --primary | #75E0D2 | Main action and selected emphasis |
| Primary foreground | --primary-fg | #071311 | Text and icons on primary fills |
| Primary hover | --primary-hover | #91EEE2 | Hovered primary control |
| Muted surface | --muted | #252E38 | Quiet controls and supporting regions |
| Muted foreground | --muted-fg | #C1CBD5 | Secondary text and metadata |
| Surface hover | --surface-hover | #303B47 | Hovered quiet controls |
| Border | --border | #222C38 | Subtle card, panel, and divider boundaries |\n| Strong border | --border-strong | #65717D | Input boundaries and controls requiring a clear edge |
| Input | --input | #0E1319 | Recessed form-field fill |
| Ring | --ring | #9AF5E8 | Keyboard focus indicator |
| Danger | --danger | #FF7777 | Destructive status and actions |
| Danger foreground | --danger-fg | #250707 | Text on danger fills |
| Success | --success | #78DCA4 | Successful status |
| Success foreground | --success-fg | #071D11 | Text on success fills |
| Warning | --warning | #FFD36E | Warning status |
| Warning foreground | --warning-fg | #251A00 | Text on warning fills |
| Info | --info | #78BFFF | Informational status |
| Info foreground | --info-fg | #07182A | Text on info fills |
| Overlay | --overlay | rgba(0, 0, 0, 0.68) | Modal scrims; use directly as a translucent colour |

Rules:
- Use --primary only for the most important action or active state in a local context. Its text always uses --primary-fg.
- Keep background and surface tones close, but distinguish adjacent layers with a visible boundary or luminance change.
- Use --muted-fg for supporting content, not essential instructions or error messages.
- Semantic colours communicate meaning; pair them with a label or icon.
- The dark palette is the default. If an alternate theme is introduced, define all semantic roles as a complete set and validate its contrast. Do not derive it by simply inverting every value.

### 3.2 Typography

The reference has a technical typographic character. Treat Teletext as a display reference for short decorative labels or headings only, not as the default reading face. Bitmap-like type can become difficult to read at fractional scaling, may lack weights, and may not cover all writing systems.

Use a readable sans-serif for body text and controls, with a monospace companion for numeric or code-like data. Geist Sans and Geist Mono are suitable reference families; provide robust system fallbacks.

| Style | Size / line height | Weight | Typical use |
|---|---:|---:|---|
| xs | 12px / 16px | 400–500 | Compact metadata |
| sm | 14px / 20px | 400–500 | Labels and secondary controls |
| base | 16px / 24px | 400 | Body and instructions |
| lg | 18px / 28px | 500 | Panel and card headings |
| xl | 20px / 28px | 600 | Section headings |
| 2xl | 24px / 32px | 600 | Page titles |
| 3xl | 30px / 36px | 600 | Prominent task heading |
| 4xl | 36px / 44px | 700 | Rare display use |

Use uppercase and letter spacing only for short section labels, metadata, and compact navigation where it improves scanning. Never use tracked uppercase for paragraphs, form instructions, or user-authored content. Use tabular numerals for values that change or align.

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

Use 8–12px inside compact controls, 12–16px between related controls, 20–24px for panel padding, and 24–32px between distinct work areas. Compactness must not reduce target sizes or readability.

### 3.4 Shape and surfaces

| Token | Value | Use |
|---|---:|---|
| --radius-sm | 4px | Badges and compact labels |
| --radius-md | 8px | Inputs, menus, and rectangular controls |
| --radius-lg | 12px | Panels and dialogs |
| --radius-xl | 16px | Large contained surfaces |
| --radius-2xl | 20px | Rare large grouping |
| --radius-pill | 9999px | Buttons, chips, segmented navigation |
| --border-width | 1px | Standard boundary |
| --border-width-strong | 2px | Focused or selected boundary |

Pill geometry is a deliberate motif for actions and segmented navigation, not a rule for every control. Inputs, select fields, menus, and work panels use rounded rectangles. This keeps form fields from looking like oversized search pills and avoids a geometry clash.

Prefer thin borders and restrained shadows. Use spacing before adding another card. A static surface must not look interactive unless it can be activated.

### 3.5 Elevation

| Level | Treatment | Use |
|---|---|---|
| 0 | No shadow | Main work area |
| 1 | 0 2px 8px rgba(0,0,0,.24) | Subtle panel separation |
| 2 | 0 8px 24px rgba(0,0,0,.42) | Menus and popovers |
| 3 | 0 16px 48px rgba(0,0,0,.56) | Dialogs and modal layers |

Use opaque surfaces as the baseline. Do not depend on blur or transparency to establish hierarchy.

### 3.6 Motion tokens

| Token | Value | Use |
|---|---:|---|
| --motion-fast | 120ms | Press and focus feedback |
| --motion-normal | 180ms | Menus, tabs, and controls |
| --motion-slow | 240ms | Dialogs and larger transitions |
| --motion-ease-out | cubic-bezier(0.16, 1, 0.3, 1) | Entering and settling |
| --motion-ease-in-out | cubic-bezier(0.4, 0, 0.2, 1) | Selection and position changes |

Keep motion brief. Prefer opacity and transform. Avoid bounce, perpetual animation, large shimmer effects, and layout movement that changes control position during interaction. Respect reduced-motion preferences.

## 4. Layout and navigation

### 4.1 Application frame

Keep the application frame visually quiet. Separate global navigation, local navigation, page actions, and content controls. The current task or content is the visual centre. Do not add branding panels, toolbars, or status regions that duplicate nearby actions.

### 4.2 Segmented navigation

Use segmented pill navigation when the product has a small, stable set of peer destinations.

- Group related destinations into one compact control.
- Use concise labels; add a simple line icon only when it improves recognition.
- Show the active destination with a contrasting filled segment.
- Keep inactive segments quiet but readable.
- Keep page-specific actions outside the destination selector.
- Expose the selected state semantically and support keyboard navigation.
- Use a short active-indicator transition; never delay navigation.

Do not force segmented navigation into a large, nested, or frequently changing information architecture. Use another navigation pattern when it better fits the task.

### 4.3 Work area

Use a clear primary work area with deliberate internal grouping. Add sidebars, inspectors, split views, tabs, or toolbars only when they support a real workflow. Make scroll ownership clear when multiple regions scroll independently. Keep actions near the content they affect.

### 4.4 Persistent actions and status

A compact status or action bar is optional.

- Include only a few relevant global actions or ongoing statuses.
- Show progress only while it helps the user understand ongoing work.
- Do not reserve prominent space for empty placeholders.
- Move secondary actions into overflow or contextual locations on constrained layouts.

## 5. Component specifications

### 5.1 Buttons

| Variant | Appearance | Use |
|---|---|---|
| Primary | Teal filled pill with dark foreground | Main local action |
| Outline | Transparent or surface fill with border | Secondary action |
| Ghost | No permanent border | Low-emphasis action |
| Destructive | Danger semantic treatment | Risky or irreversible action |

Buttons have default, hover, focus-visible, pressed, disabled, and pending states. Use concise labels and consistent casing. Avoid multiple primary buttons competing in one region.

### 5.2 Icon buttons

Use simple line icons with consistent optical size and stroke. Icon-only controls need accessible names; add a tooltip when the action is not self-evident. Do not use emoji or arbitrary text characters as core interface icons.

### 5.3 Inputs and forms

- Use persistent labels above or beside fields; placeholders are supplementary.
- Use rounded rectangular fields with --input fill, --border boundary, and a visible --ring focus state.
- Do not make text inputs full pills merely because buttons are pills.
- Support text, search, password, number, date, select, checkbox, radio, switch, and textarea patterns with coherent geometry.
- Group related fields by spacing and short section labels.
- Put validation next to the affected field and explain how to correct it.
- Preserve values after recoverable errors.
- Keep keyboard and touch operation equivalent to pointer operation.

### 5.4 Cards, panels, and dividers

Use a panel when it represents a meaningful group of content or actions. Keep the surface flat and the border restrained. Avoid nested card-on-card layouts. Use spacing instead of separators where a divider adds no structure.

### 5.5 Menus and popovers

Anchor floating content to its trigger. Use an elevated surface, subtle --border, and restrained shadow. Keep menu rows compact and readable. Add icons, shortcuts, and separators only when useful. Support keyboard operation and Escape dismissal. Menus must remain within the viewport or desktop window and must not depend on hover.

### 5.6 Dialogs and settings

Use a clear title, close action, content region, and predictable footer actions. Long content scrolls inside the dialog. Adapt the panel to available space. A two-pane settings layout is appropriate only when the number and relationship of settings justify it. Group related settings with spacing, not nested cards. Manage focus on open and close.

### 5.7 Tooltips, toasts, and status

Tooltips are short and supplementary; essential instructions must remain visible elsewhere. Toasts are compact, non-blocking, and actionable where appropriate. Status uses text or an icon as well as colour. Design loading, empty, success, warning, offline, and error states. Do not fill empty areas with fabricated sample content.

### 5.8 Tables and structured data

When users compare records or aligned values, use a real table or clearly structured list. Align numeric values consistently, keep column headings persistent when useful, allow horizontal overflow on narrow screens, and provide a stacked or priority-column presentation when a table cannot fit. Do not solve dense data by shrinking text below the defined scale.

## 6. Interaction and motion

### 6.1 Interaction states

Every interactive element defines default, hover, focus, pressed, selected, disabled, pending, and error states as applicable. Hover and selected must not look identical. A state must remain understandable without colour or animation.

### 6.2 Keyboard, pointer, and touch

- All essential actions are keyboard-operable.
- Focus is visible and follows a logical order.
- Menus and dialogs support conventional keyboard behaviour.
- Closing an overlay returns focus to its trigger where appropriate.
- Hover never provides the only access to an action.
- Touch controls do not require precision pointer movement.
- Shortcuts are enhancements, not replacements for visible controls.

### 6.3 Motion

Use motion to explain opening, closing, selection, and feedback. Keep movement short and controlled. Do not move controls away from a pointer or focused element. Disable nonessential motion when reduced motion is requested.

## 7. Web and desktop delivery

### 7.1 Web

Treat the browser viewport as the application area. Do not draw a fake operating-system title bar or duplicate browser controls. Support resizing, browser zoom, text selection, scrolling, keyboard navigation, and native accessibility features. Do not depend on one browser's proprietary rendering behaviour.

### 7.2 Desktop

Respect the host operating system's window conventions. Prefer native title bars unless custom chrome has a clear product benefit. If custom chrome is used, preserve window-manager behaviour and keep interactive controls outside draggable regions. Do not assume a single display scale, compositor, or system theme.

Test the actual desktop runtime, including fonts, focus, scrolling, menus, dialogs, resizing, and system scaling. A browser preview alone is not sufficient evidence that a packaged desktop application behaves correctly.

### 7.3 Platform-specific checks

- **Windows:** verify WebView2 rendering, system scaling, native title-bar controls, and keyboard conventions.
- **macOS:** respect traffic-light control placement and insets when custom title bars are used; verify menu and keyboard conventions.
- **Linux:** test the target toolkit, compositor, window manager, and actual WebKitGTK or other embedded runtime when used. Do not assume transparent corners, backdrop blur, or compositor-specific effects are available.
- **Shared product:** keep semantic tokens, terminology, hierarchy, and interaction states consistent. Limit platform differences to system integration and genuine usability needs.

Do not overfit the design to one Linux/WebKitGTK combination. Likewise, do not imitate Windows or macOS chrome in a Linux application.

## 8. Accessibility and usability

- Maintain sufficient contrast for text, icons, boundaries, and focus.
- Never use colour alone for selection, status, or errors.
- Use semantic controls and accessible names.
- Associate field labels and validation messages with their controls.
- Provide logical reading and focus order.
- Support reduced motion, browser zoom, and text enlargement.
- Ensure menus, dialogs, tables, and forms work with the keyboard.
- Keep targets comfortably operable with supported input methods.
- Important information must not exist only in a tooltip or transient toast.

## 9. Iconography\n\nUse a consistent family of simple line icons. Keep stroke weight and optical size consistent. Use the same icon for the same action throughout the product. Avoid emoji or arbitrary text characters as substitutes for core interface icons. Hide decorative icons from assistive technology and give each icon-only control an accessible name.\n\n## 10. Implementation and adaptation guidance

- Centralise semantic colour, typography, spacing, radius, border, elevation, focus, and motion tokens.
- Build reusable controls and interaction patterns.
- Keep product logic separate from presentation.
- Use a chosen component library only when its appearance and accessibility can be aligned with this specification.
- Do not add dependencies solely for basic controls when a small maintainable implementation is sufficient.
- Do not copy proprietary assets, branding, or product features without authorisation.
- Do not copy source implementation defects as design requirements.

## 11. Quality checklist

- [ ] The interface feels restrained, technical, dark, and precise.
- [ ] Semantic tokens have explicit hex values and foreground pairings.
- [ ] Type, spacing, radius, elevation, and motion use the defined scales.
- [ ] Teletext is not used as the default body or form font.
- [ ] Pills are reserved for actions and segmented controls; fields remain rounded rectangles.
- [ ] Navigation fits the actual information architecture.
- [ ] Forms, tables, menus, dialogs, and status states are specified.
- [ ] Web behaviour supports browser resizing, zoom, and keyboard use.
- [ ] Desktop behaviour respects the target operating system and runtime.
- [ ] No platform-specific rendering assumption is treated as universal.
- [ ] Reduced motion and accessible focus are supported.
