# DESIGN.md

## Purpose

This document defines a reusable UI/UX direction inspired by **Kryoto Desktop**. Use it when designing a web application, a desktop application, or one product delivered on both platforms.

The goal is to carry over Kryoto's visual character and interaction principles, not to reproduce its product, screens, content, or feature set. The product's information architecture, workflows, features, and content must come from its own requirements. Do not invent them to imitate the reference.

This is a design specification, not a technology-stack prescription. It describes the expected visual and interaction outcome while leaving implementation decisions to the project.

Primary reference: <https://github.com/Kryoto-Dev/kryoto-desktop>

## 1. Design direction

The interface should feel:

- **Dark and restrained.** Use a near-black foundation, closely related neutral surfaces, subtle borders, and clear foreground contrast.
- **Compact but readable.** Make efficient use of space without making content, labels, or controls difficult to read or operate.
- **Technical and distinctive.** Use purposeful typography, tracked uppercase labels, simple line icons, pill-shaped controls, and a small set of recognisable status treatments.
- **Precise.** Align elements carefully, use consistent spacing, and make selection and interaction states unambiguous.
- **Quiet.** Keep decoration, persistent chrome, shadows, and visual noise under control. The user's current task should dominate.
- **Cohesive across surfaces.** Preserve the same visual language in browsers and desktop windows while adapting platform-specific framing and behaviour.

Avoid generic dashboard styling, excessive nested cards, oversized decorative headers, gradients used as decoration, and interfaces where every element competes for attention.

## 2. Core principles

1. **Hierarchy over decoration.** Use layout, typography, spacing, and contrast to establish importance. Add borders and surfaces only when they clarify structure.
2. **One strong emphasis at a time.** Reserve the light, filled treatment for the primary action or active selection in its local context. Keep secondary actions quieter.
3. **Content over chrome.** Navigation, toolbars, window framing, and status elements should take only the space they need.
4. **Consistency over novelty.** A given action or state should look and behave the same throughout the product.
5. **Progressive disclosure.** Keep infrequent actions in menus or contextual controls instead of displaying every option permanently.
6. **Motion with meaning.** Animation should explain a state change or provide feedback, never be required to understand the interface.
7. **Adapt the pattern to the task.** Use Kryoto-inspired patterns where they improve clarity. Do not force them into an unsuitable workflow.
8. **Responsive by composition.** Reorganise the interface as space changes; do not merely shrink a wide layout.

## 3. Visual system

### 3.1 Colour

Use a near-black, OLED-inspired theme as the visual baseline. The palette should be predominantly neutral, with high-contrast foreground content and restrained semantic colours.

Define a central set of semantic colour roles:

- `background` and `foreground` for the primary page or application surface.
- `surface` and `surface-foreground` for grouped or raised content.
- `popover` and `popover-foreground` for menus and floating panels.
- `primary` and `primary-foreground` for the most important action or selected item.
- `secondary`, `muted`, and their foreground roles for quiet controls and supporting information.
- `border`, `divider`, `input`, and `focus` for structure and interaction feedback.
- `success`, `warning`, `info`, and `destructive` for meaningful status communication.

Keep the difference between adjacent surfaces subtle but perceptible. Borders should usually be low contrast. Use semantic colours to communicate meaning, not to decorate the interface. Do not invent one-off colours when a semantic token already exists.

The reference uses a very dark OLED palette and offers alternative palettes. Treat the dark neutral palette as the starting point. Additional themes are optional; when present, they must use the same semantic roles and preserve contrast. Do not assume every display renders black identically.

### 3.2 Typography

Typography is a defining part of the reference's identity.

- Use **Teletext** as the primary typographic reference where the font can be included and distributed appropriately. Preserve its compact, technical character.
- Use **Geist Mono** or a comparable monospace face for numeric values, aligned data, code-like content, and fixed-width details.
- Provide sensible system fallbacks. If the reference fonts are unavailable or unsuitable, choose legible alternatives with a similar technical tone rather than an unrelated display font.
- Use uppercase labels with deliberate letter spacing for section labels, compact navigation, and metadata. Do not apply this treatment to paragraphs, long-form content, or user-authored text.
- Keep a clear type hierarchy. Titles should be distinct without being oversized; supporting text should be quieter but still readable.
- Use tabular numerals for changing or aligned values such as counts, durations, sizes, and progress.
- Use font weight sparingly. Reserve stronger weight for emphasis, active items, and important values.

Typography must remain usable at browser zoom levels and operating-system display scaling settings. Never rely on tiny text to achieve density.

### 3.3 Shape and surfaces

- Treat pill-shaped controls as a recognisable visual motif for buttons, icon buttons, chips, and segmented navigation.
- Use rounded rectangular surfaces for dialogs and substantial panels where containment is useful.
- Use consistent corner treatments. Do not mix arbitrary radii within the same component family.
- Prefer thin borders and subtle surface changes over heavy outlines or large shadows.
- Keep shadows restrained and use them only to distinguish floating elements from the content beneath.
- Do not wrap every group of content in a card. Use spacing and alignment before adding another surface.

### 3.4 Spacing and alignment

Use a consistent spacing scale across the interface. Related controls should share alignment, padding, and gaps. Use larger spacing to distinguish separate groups or levels of hierarchy.

Keep layouts visually compact but preserve comfortable control targets and readable line lengths. Dimensions must be chosen in response to content, context, viewport or window space, and input method. Do not copy fixed pixel dimensions from the reference or prescribe arbitrary universal sizes.

## 4. Layout and composition

Kryoto's composition is a reference, not a mandatory screen template. Use only the layout regions the actual product needs.

### 4.1 Application frame

- Keep global framing visually quiet and integrated with the content surfaces.
- Distinguish global navigation, local navigation, page actions, and content controls.
- Keep persistent framing stable while the relevant content changes or scrolls.
- Give the main task or content the greatest visual weight.
- Avoid large branding areas, redundant toolbars, and controls that duplicate actions already available near the content they affect.

### 4.2 Navigation

When a product has a small set of top-level destinations, use Kryoto's **segmented pill navigation** as a reference:

- Place related destinations in one compact, coherent group.
- Use concise labels; add a simple line icon only when it improves recognition.
- Show the active destination with a clearly contrasting filled segment.
- Keep inactive segments muted, with restrained hover and focus feedback.
- Keep page-specific actions separate from the destination selector.
- If animated, move the active indicator smoothly and briefly without delaying the content change.

Use this pattern only when it fits the product's information architecture. Other navigation models should follow the same typography, spacing, colour, and state language. Do not force a segmented control into a large, deeply nested, or frequently changing navigation structure.

### 4.3 Work area

- Make the current task or content the visual centre of the interface.
- Prefer a clear primary work area with deliberate internal grouping over many nested panels.
- Add sidebars, split views, inspectors, tabs, or toolbars only when they support a real workflow.
- Make the ownership of scrolling clear when multiple regions scroll independently.
- Keep actions close to the content they affect.
- Design the composition to handle empty, loading, populated, long, and error states without changing its visual language.

### 4.4 Persistent actions and status

A compact status or action bar may be used when users need persistent access to a small number of global actions or ongoing activity. It is optional, not a required part of the design.

- Keep its contents few, relevant, and visually secondary to the work area.
- Show progress or activity only while it is useful.
- Prefer concise labels, small icons, and restrained progress indicators.
- Do not reserve prominent space for empty placeholders.
- On constrained layouts, move secondary actions and status into an overflow or contextual location.

## 5. Component language

Build a small, coherent set of reusable components. Components should share the same tokens, proportions, typography, and interaction states. The exact component architecture is implementation-dependent.

### 5.1 Buttons

Use consistent semantic variants:

- **Primary:** light filled pill for the main action in a local context.
- **Outline:** quiet surface or transparent background with a subtle border for secondary actions.
- **Ghost:** no permanent border; uses a restrained surface or foreground change on hover and focus.
- **Destructive:** uses the destructive semantic role and clear wording for risky actions.

Every button needs coherent default, hover, focus, pressed, disabled, and pending states. Do not style every action as primary. Keep labels concise and consistent in casing. Make the full intended control area interactive.

### 5.2 Icon buttons

- Use simple, consistent line icons in the visual style of Lucide.
- Keep icon proportions, stroke, alignment, and target areas consistent.
- Give icon-only controls accessible names. Add a tooltip when the icon's meaning is not obvious.
- Do not substitute emoji or arbitrary text characters for interface icons.
- Never rely on icon colour alone to explain an action or state.

### 5.3 Labels and supporting text

Use compact, tracked uppercase labels for section names and metadata when they improve scanning. Use normal casing and tracking for descriptions, instructions, and longer content. Keep supporting information subordinate to the value or content it describes. Avoid repeating information already clear from context.

### 5.4 Cards, panels, and dividers

Use a card or panel only when it groups related content or actions into a meaningful unit. Keep surfaces flat and restrained. Avoid nested card-on-card layouts, excessive outlines, and decorative shadows. Prefer spacing over dividers when a divider adds no useful structure. A static surface must not look interactive unless it is actionable.

### 5.5 Menus and popovers

- Anchor floating content to its trigger and align it predictably.
- Use a distinct but restrained surface, subtle border, and limited shadow.
- Keep menu rows compact and scannable.
- Add icons, shortcuts, headings, or separators only when they add useful information.
- Support keyboard operation and dismissal with Escape where appropriate.
- Dismiss on outside interaction when appropriate, without making accidental dismissal likely during normal use.
- Keep menus within the visible viewport or window.
- Do not make hover the only way to open or use a menu. Touch and keyboard users need equivalent access.
- If menus open on hover, introduce a short intentional delay to prevent accidental opening while the pointer crosses navigation.

### 5.6 Dialogs and settings

- Use a restrained overlay and a clearly bounded panel.
- Provide a clear title, close action, focused content area, and footer actions when needed.
- Keep long content inside a designated scrollable region.
- Adapt the panel to available space rather than preserving a desktop-sized dialog on a narrow viewport.
- A two-pane settings layout with a section rail and content area is a useful reference for complex settings. Use it only when the number and relationship of settings justify it.
- Group related settings with spacing and concise labels rather than unnecessary nested cards.
- Manage focus on open and close. Prevent interaction with content behind a modal dialog.

### 5.7 Tooltips, notifications, and status

- Keep tooltips short and consistent. Essential instructions must not exist only in a tooltip.
- Keep toast notifications compact and non-blocking. Show only the information needed to understand the event and any relevant next action.
- Use restrained status indicators and progress treatments. Pair meaningful status with text; do not rely on colour or animation alone.
- Design loading, empty, success, warning, offline, and error states as part of the same component language.
- Empty states should explain the situation and offer a next step only when one exists. Do not insert fabricated sample content to fill empty space.

### 5.8 Forms and data entry

- Use the same restrained surfaces, borders, typography, and focus treatment as other controls.
- Give every field a persistent, programmatically associated label. Placeholder text is not a substitute for a label.
- Group related fields through spacing and concise section labels.
- Show validation near the affected field and explain how to resolve the issue.
- Preserve entered values when validation fails or a recoverable operation is interrupted.
- Ensure every control works with the supported input methods.

## 6. Interaction and motion

### 6.1 Interaction states

Every interactive element must communicate its state consistently:

- **Default:** quiet and appropriate to its role.
- **Hover:** subtle surface, border, or foreground change on hover-capable devices.
- **Focus:** clearly visible keyboard focus with adequate contrast.
- **Pressed:** immediate, restrained feedback.
- **Selected:** persistent and visually distinct from hover.
- **Disabled:** visibly unavailable and not presented as active.
- **Pending:** communicates ongoing work and prevents accidental duplicate activation when necessary.
- **Error:** identifies the affected control or operation and offers a recovery path where possible.

Do not use the same appearance for hover and persistent selection. State must remain understandable without colour or motion.

### 6.2 Motion

The reference uses brief fades, subtle scale or positional changes, and small status animations. Follow the same restrained approach:

- Use motion to explain opening, closing, selection, navigation, or feedback.
- Prefer opacity and transform where appropriate.
- Keep movement short and controlled.
- Avoid bouncy transitions, decorative perpetual motion, large shimmer effects, and unnecessary layout animation.
- Never make an animation delay an action or move a control away from a pointer or focused element.
- Respect `prefers-reduced-motion` and any in-app reduced-motion setting. Preserve the final state and all status information when animation is disabled.

Treat timing values as design decisions to tune and test, not fixed universal targets.

### 6.3 Keyboard, pointer, and touch

- All essential actions must be keyboard-operable.
- Keep focus visible and the focus order logical.
- Support conventional menu navigation and Escape dismissal where appropriate.
- Return focus to the invoking control when a dialog or menu closes, where applicable.
- Do not make hover the only source of essential information or functionality.
- Preserve selection in content and editable fields. Disable selection only on non-content chrome when needed for window dragging or interaction.
- Use familiar shortcuts where appropriate and show them in menus when available.
- Support touch where the product is expected to run on touch-enabled devices. Do not rely on hover or precision pointer movement.

## 7. Web and desktop delivery

The visual identity must remain consistent across web and desktop. Adapt framing and system behaviour to the platform rather than creating two unrelated designs.

### 7.1 Web

- Treat the browser viewport as the application area. Do not draw a fake operating-system title bar or duplicate browser navigation controls.
- Keep application navigation distinct from browser controls.
- Support browser resizing, zoom, text selection, scrolling, keyboard navigation, and native accessibility features.
- Prefer standard web platform behaviour. Essential appearance and interaction must not depend on one browser's proprietary behaviour.
- Test typography, focus, menus, popovers, dialogs, forms, scrolling, and responsive layouts in the browsers the product supports.

### 7.2 Desktop

- Respect the desktop environment and its window-management conventions. Do not imitate Windows or macOS chrome in a Linux application.
- Prefer native window decorations unless custom chrome has a clear product and usability benefit. If using custom chrome, preserve expected window-manager behaviour and keep interactive controls outside draggable regions.
- Do not assume one display scale, compositor, window manager, desktop environment, or system theme.
- Keep window-specific controls and behaviours in the desktop shell; do not introduce them into the web interface.

### 7.3 Linux and WebKitGTK

When the desktop target is Linux and uses Tauri, validate the design in the actual **WebKitGTK** runtime. A Chromium-based browser preview is not sufficient.

- Prefer opaque window and panel surfaces. Do not make the design depend on transparent corners, backdrop blur, or compositor-specific effects.
- Use CSS effects conservatively. Large blur regions, animated backgrounds, and repaint-heavy effects can perform poorly in some WebKitGTK environments.
- Test font rendering and provide Linux-compatible fallbacks.
- Ensure custom dragging does not intercept buttons, links, menus, text fields, or other interactive elements.
- Verify focus, scrolling, popovers, dialogs, window resizing, display scaling, and animations in the packaged application.
- Treat WebKitGTK compatibility as a design and QA constraint, not as a reason to compromise the shared visual language unnecessarily.

### 7.4 Shared web and desktop product

- Share semantic colour, typography, shape, spacing, component, and motion tokens.
- Keep terminology, information hierarchy, component states, and workflow semantics consistent.
- Adapt the application frame to the platform: browser viewport on the web, desktop window conventions in the native application.
- Do not duplicate browser controls in the desktop shell or desktop window controls in the web page.
- Reflow navigation, dialogs, menus, and persistent status to fit the available space while preserving their visual language and meaning.
- Keep platform-specific exceptions deliberate and limited to usability, accessibility, or system integration needs.

## 8. Accessibility and usability

The visual style must never take priority over usability.

- Maintain sufficient contrast for text, icons, meaningful borders, and focus indicators.
- Do not use colour as the only way to communicate selection, status, error, or progress.
- Use semantic controls and meaningful accessible names. Icon-only controls require accessible labels.
- Provide logical reading and focus order.
- Associate form labels and validation messages with their controls.
- Support reduced motion, browser zoom, and text enlargement without clipping or loss of functionality.
- Keep targets comfortably operable with supported input methods.
- Ensure transient messages remain perceivable long enough to understand and are not the only place important information appears.

## 9. Implementation guidance

This document specifies the design outcome, not a mandatory framework, component library, or code architecture.

- Define semantic tokens centrally for colour, typography, shape, spacing, borders, and motion.
- Build reusable primitives for repeated controls and interaction patterns.
- Keep product logic separate from presentation.
- Use the chosen framework and styling approach without fragmenting the visual system into one-off styles.
- Existing component libraries may be used if their appearance and accessibility behaviour can be brought into alignment with this specification.
- Avoid adding dependencies solely for basic controls when a small, maintainable implementation is sufficient.
- Do not copy Kryoto branding, proprietary assets, names, product terminology, or product features unless separately authorised and appropriate.
- Where a pattern must differ for product, accessibility, or platform reasons, make the exception intentional and consistent.

## 10. Quality criteria

The resulting interface should satisfy all of the following:

- It carries Kryoto's restrained, near-black, technical visual character without copying its product screens.
- Typography, colour, surfaces, borders, spacing, shapes, and icons form one coherent system.
- The content and the user's current task remain the visual priority.
- Navigation and selected states are immediately understandable wherever navigation is needed.
- Components have complete, consistent interaction states.
- Information density is balanced with readability and comfortable interaction targets.
- Layouts adapt to browser viewports and resizable desktop windows without relying on copied dimensions.
- Web behaviour remains usable with resizing, zoom, scrolling, keyboard input, and supported browsers.
- Desktop behaviour respects platform conventions and is tested in its actual runtime.
- Linux builds using WebKitGTK are tested in WebKitGTK, including focus, scrolling, menus, dialogs, fonts, and visual effects.
- Web and desktop versions retain the same visual identity and interaction semantics while respecting platform differences.
- Motion is purposeful, brief, and compatible with reduced-motion preferences.
- Essential operations work with keyboard and supported pointer or touch input.

## 11. Kryoto reference files

Use these files to inspect concrete examples of the reference's implementation. They are references, not required project files or a template architecture.

- [Global styles, design tokens, palettes, typography, and motion](https://github.com/Kryoto-Dev/kryoto-desktop/blob/main/src/styles.css)
- [Buttons, icon buttons, cards, dialogs, menus, labels, and captions](https://github.com/Kryoto-Dev/kryoto-desktop/blob/main/src/ui/index.tsx)
- [Segmented navigation and active selection behaviour](https://github.com/Kryoto-Dev/kryoto-desktop/blob/main/src/shell/NavBar.tsx)
- [Title bar and desktop window interaction patterns](https://github.com/Kryoto-Dev/kryoto-desktop/blob/main/src/shell/TitleBar.tsx)
- [Compact persistent actions and status](https://github.com/Kryoto-Dev/kryoto-desktop/blob/main/src/shell/BottomBar.tsx)
- [Frontend dependencies and font/icon packages](https://github.com/Kryoto-Dev/kryoto-desktop/blob/main/package.json)

When implementation detail matters, inspect the current source file. This specification captures the reusable design direction and does not attempt to document every product-specific behaviour in Kryoto Desktop.
