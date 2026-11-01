# DESIGN.md

## Purpose

This document defines the visual language and interaction principles for a product inspired by the **JustAnime** interface. Use it as the shared UI/UX specification when designing or implementing screens, components, and states for either a web application or a desktop application.

The goal is to reproduce the character of JustAnime's experience: **cinematic, dark, image-led, content-dense without feeling crowded, and quick to navigate**. Anime artwork should carry most of the visual weight. Interface chrome should organise the catalogue and playback experience without competing with the content.

This is a design specification, not a feature list or a screen-by-screen wireframe. Do not assume that every product using this design must have anime catalogues, streaming, schedules, or the same routes as JustAnime. Apply the visual and interaction principles to the product's actual content and workflows.

## Design principles

1. **Content is the foreground.** Artwork, titles, and useful metadata take priority over decoration. Use interface surfaces to frame content, not to dominate it.
2. **Dark and cinematic.** Build depth through near-black backgrounds, restrained charcoal surfaces, subtle borders, and imagery that fades naturally into the surrounding interface.
3. **High information clarity.** Keep titles readable, metadata compact, and actions easy to distinguish. Avoid unnecessary panels, labels, and decorative elements.
4. **Browse without friction.** Search, categories, filters, collections, and related content should be easy to discover and quick to operate.
5. **Consistent interaction language.** Reuse the same hover, focus, selected, loading, and disabled behaviours throughout the product.
6. **Responsive by composition.** Preserve hierarchy and usability as the available space changes. Reflow content rather than shrinking a desktop layout until it becomes cramped.
7. **Motion supports orientation.** Use transitions to communicate state changes and spatial relationships. Never make animation a prerequisite for understanding or operating the interface.

## Visual identity

### Overall appearance

Use a predominantly monochrome dark interface. The base should read as black rather than blue, purple, or neutral mid-grey. Separate regions with small changes in luminance rather than strong coloured surfaces or heavy shadows.

The visual hierarchy should normally follow this order:

- primary content and artwork;
- page or section title;
- primary action;
- supporting metadata and secondary actions;
- borders, separators, and decorative effects.

Do not give every element equal contrast. Reserve the brightest treatment for the most important content or action in a given context.

### Colour palette

The repository's global stylesheet uses the following core values. Treat them as reference tokens and preserve their relationships when extending the system:

| Token | Reference value | Use |
|---|---|---|
| `background` | `#0A0A0A` | Main page and application background |
| `foreground` | `#FFFFFF` | Primary text and high-contrast controls |
| `primary` | `#D1D1D1` | Primary neutral accent and active details |
| `secondary` | `#404040` | Stronger muted surfaces and secondary emphasis |
| `accent` | `#808080` | Supporting accent and subdued emphasis |
| `card` | `#131313` | Cards, menus, dropdowns, and contained surfaces |
| `border` | `#2A2A2A` | Dividers, outlines, and low-emphasis edges |
| `hover` | `#333333` | Hovered rows, controls, and interactive surfaces |
| `text-muted` | `#8A8A8A` | Descriptions, hints, and secondary metadata |

Rules for colour use:

- Keep most large surfaces within the background/card/border range.
- Use white or near-white for primary text. Use muted grey for secondary details, not for important instructions or essential status messages.
- Use the primary light neutral for selected states and primary actions. A light button with dark text should be visually distinct from a quiet outlined or transparent secondary action.
- Use semantic colours sparingly. A rating, warning, error, or success state may need a distinct hue, but do not turn the general interface into a multicoloured dashboard.
- Keep overlay text legible over all artwork. Apply local gradients or scrims instead of relying on the image to provide a uniform text background.
- Avoid introducing gradients as a general surface treatment. Gradients belong primarily to image overlays and cinematic transitions.

### Typography

The reference project uses **Geist Sans** for general interface text and **Geist Mono** as an available monospaced companion. Use a clean modern sans-serif as the default.

Typography should be direct and compact:

- Use strong, clear headings for page and section titles.
- Use medium or semibold weights for catalogue titles and interactive labels.
- Use regular weight for descriptions and supporting copy.
- Use compact text for metadata, badges, timestamps, episode counts, and helper labels.
- Keep line lengths controlled, especially for synopsis text and descriptions.
- Truncate or clamp long titles only where the full title remains available through a detail view, tooltip, or accessible name.

Do not use all-caps for all interface text. Reserve uppercase styling for short metadata labels or compact navigation labels where it improves scanning. Avoid excessively wide letter spacing in paragraphs and titles.

### Shape, borders, and depth

Use moderate rounded corners consistent with the reference interface. Poster media, cards, search fields, dropdowns, and content containers should feel related, but not every element needs the same radius.

- Use subtle one-pixel borders to define surfaces against the black background.
- Prefer a border and slight tonal shift over a large shadow for ordinary cards.
- Use stronger shadows only when an element floats above the page, such as a menu, suggestion list, popover, or modal.
- Clip image content cleanly to its card shape.
- Avoid excessive nested cards. A card inside a card inside another card weakens the content hierarchy.

## Layout and composition

### Shared page frame

The page frame should provide a stable place for the brand, navigation, search, and primary content. Keep the frame visually quiet so the catalogue remains the focus.

Use a consistent horizontal content boundary across the application. On wide screens, allow content to breathe and use the available width for grids, artwork, and supporting columns. On narrow screens, reduce outer gutters and reflow content in a deliberate order.

The layout must adapt to the viewport or desktop window. Do not enforce fixed page widths or hard-coded assumptions about the number of cards that fit. Use flexible grids, measured overflow, and sensible minimum sizes.

### Navigation and header

The JustAnime reference uses a fixed top navigation bar containing the brand, search, key navigation/actions, and a compact menu on smaller screens.

Keep the header recognisable and consistent across pages:

- Place the logo or wordmark in a stable, easy-to-find position.
- Make search prominent and available from primary browsing contexts.
- Keep the main navigation concise. Do not overload the header with every destination or filter.
- Group secondary actions together and give them less visual weight than search and the primary navigation.
- Provide a compact navigation mode when the viewport cannot support the full header comfortably.
- When the header changes appearance after scrolling, keep the change subtle and avoid layout jumps.

For a desktop application, preserve this hierarchy within the application window. Integrate with the host window in a deliberate way; do not duplicate native title-bar controls or platform chrome unless the application intentionally uses a custom frame.

### Content sections

Use clear section headings and consistent vertical rhythm to distinguish groups of content. A section heading should identify the content collection and may include a restrained “view all” or equivalent action.

Do not wrap every section in a visible panel. Most catalogue sections should sit directly on the page background, with spacing and headings providing separation. Use a contained card surface for modules that genuinely behave as a distinct unit, such as a calendar, filter panel, or compact information group.

### Featured / spotlight content

A featured area may use a wide landscape image as a cinematic backdrop. The artwork should fill the area without distortion. Place a dark gradient over it so that the title, metadata, synopsis, and actions remain legible.

The content hierarchy should be:

1. concise metadata;
2. prominent title;
3. optional secondary/original title;
4. short synopsis or supporting description;
5. clear primary action and a quieter secondary action.

Keep the text group anchored to a part of the image with sufficient negative space. Do not allow controls or text to obscure the focal subject. On small screens, simplify the copy and stack actions rather than compressing a desktop composition.

If the featured content rotates, provide visible previous/next or pagination controls, expose the current position, support keyboard operation, and respect reduced-motion preferences. Autoplay must not be the only way to discover content and should pause when the user interacts or when the interface is not visible.

## Catalogue and media presentation

### Poster cards

Poster cards are a defining JustAnime pattern. Artwork should be the primary visual element, with title and minimal metadata immediately associated with it.

- Use a consistent portrait aspect ratio for poster artwork. The reference implementation uses a 2:3 ratio for catalogue posters; preserve that visual proportion unless the actual content requires another format.
- Use `object-fit: cover` or the platform equivalent. Never stretch artwork to fill a card.
- Keep the poster edge clean and use a restrained corner radius.
- Place compact badges over the image only when they communicate useful facts, such as content type, language, episode availability, or release status.
- Give badges a dark, translucent backing so they remain legible over varied artwork.
- Keep the title outside the poster image in the normal card layout. Allow enough space for multi-line titles and use consistent clamping behaviour.
- Avoid adding a dense block of ratings, tags, and descriptions beneath every poster. Surface additional information in a detail view or on demand.

Hover/focus treatment:

- Slightly lift or scale the poster to signal interactivity; keep the movement subtle.
- A dark overlay may appear over the artwork, revealing a centred play or open affordance where appropriate.
- Do not make hover the only way to access an action. The equivalent action must be reachable by keyboard, touch, and assistive technology.
- Keep focus indication visible and distinct from the hover treatment.

### Horizontal content rails

Use horizontal rails when a collection benefits from quick scanning without consuming the full vertical page. Examples in the reference include recent episodes, anime collections, and seasonal content.

- Keep card widths consistent within a rail.
- Allow touch, trackpad, mouse-wheel, and keyboard scrolling where supported.
- Use scroll snapping only when it improves alignment and does not trap the user in a forced paging pattern.
- Show directional controls when they are useful and available; hide or disable them at the relevant boundary.
- Do not hide the only indication that more content exists. A scrollbar may be visually subdued, but keyboard and assistive technology users must still be able to discover and operate the rail.
- At narrow widths, reduce the visible card count naturally rather than shrinking cards below a comfortable reading size.

### Grids and lists

Use grids for browsing and searching when users need to compare many items at once. Choose the number of columns from available space and card readability, not from a fixed desktop/mobile assumption.

Use lists for information that is better understood row by row, such as episode listings, release schedules, or search results with richer metadata. Keep rows aligned, scan-friendly, and visually separated without creating heavy boxes around every item.

## Search, filters, and discovery

### Search

Search is a primary navigation tool and should be easy to reach from the main browsing experience.

- Use a clear placeholder that describes what can be searched.
- Give the field a visible focus state and a comfortable input area.
- Debounce remote suggestions when appropriate, but do not make the user wait unnecessarily after submitting a complete query.
- Suggestions should appear in a surface above surrounding content, with a clear boundary, readable text, and optional small thumbnail.
- Each suggestion should have a clear primary label and compact secondary metadata.
- Support arrow-key navigation, Enter to select, Escape to close, and pointer/touch selection.
- Provide explicit loading, empty, and error states. Never leave a blank dropdown that looks broken.
- Clicking outside may dismiss suggestions, but focus and selection should behave predictably.

### Filters and sorting

Filters should be compact and understandable. Group related filter options and make the selected values visible after the menu closes.

- Use menus, popovers, or dedicated filter panels depending on the complexity and available space.
- Opening one filter should not unexpectedly leave many unrelated menus open.
- Show active filter state clearly and provide a simple way to clear filters.
- Use familiar labels and avoid abbreviations unless the domain makes them unambiguous.
- Preserve selections while the user browses results, unless the user explicitly resets them.
- Keep sorting separate from categorical filtering when that makes the controls easier to understand.

## Detail and information views

A detail view should combine a strong artwork anchor with structured information. The JustAnime reference uses a poster, a subdued enlarged artwork background, a title block, metadata chips, a primary watch action, and tabbed supporting information.

Apply these principles:

- Use one dominant poster or image to establish the subject.
- A faint, enlarged version of the artwork may sit behind the content, but keep its opacity low and fade it into the page background so it never competes with text.
- Present the title and alternate title clearly. Do not make the original title or synopsis more prominent than the main title.
- Group rating, year, release status, format, episode availability, and similar facts into compact metadata chips.
- Use tags for genres, studios, and related classification. Keep the tags visually quiet and allow them to wrap.
- Use tabs or an equivalent section switcher for distinct groups of supporting information. The active tab should be visible through text contrast and a simple underline or border accent, not a large coloured block.
- Let synopsis text expand when it is truncated. The full text must remain accessible.
- Keep related content and recommendations visually connected to the detail page without competing with the primary information.

## Playback experience

The player is a focused media surface. The video itself should occupy the dominant area; controls should be visible when needed and recede when playback is uninterrupted.

- Use a true video aspect ratio and a black or near-black player background.
- Keep playback controls grouped logically: play/pause, timeline, volume, elapsed/total time, playback options, picture-in-picture where supported, and fullscreen.
- Place a subtle dark gradient behind controls rather than a large opaque toolbar.
- Show controls when the pointer enters the player or the user interacts; hide them after inactivity only while playback is active.
- Keep controls available to keyboard and touch users. On touch devices, provide explicit ways to reveal and dismiss controls.
- The timeline should distinguish played, buffered, and unplayed portions. Any extra markers must have a clear meaning and an accessible description.
- Preview thumbnails, quality selectors, playback speed, audio settings, and subtitle controls should appear in compact, well-layered menus.
- Loading, buffering, unavailable-source, and playback-error states must be distinct. Explain what happened and provide a recovery action where possible.
- Never let a loading animation obscure an error message or prevent the user from changing source or retrying.

## Components and interaction patterns

### Buttons

Use a clear hierarchy:

- **Primary:** light neutral surface with dark text; reserved for the main action in a context.
- **Secondary:** transparent or dark surface with a subtle border; used for alternative actions.
- **Tertiary:** text or icon action with minimal chrome; used for low-priority actions.
- **Destructive:** visually distinct and used only for destructive operations.

Buttons should have visible hover, focus, pressed, disabled, and loading states. Labels should use clear verbs. Icon-only buttons require an accessible name and a tooltip or equivalent label where useful.

### Tabs

Use a simple underline or border to mark the selected tab. Inactive tabs should remain readable but quieter. Tabs must expose selected state semantically and support keyboard navigation according to the chosen tab pattern.

### Menus, dropdowns, and popovers

Use the `card` surface, a subtle border, and a modest shadow to distinguish floating content from the page. Align menus with their trigger and keep them within the viewport. Dismiss on Escape and on an outside interaction. Do not dismiss when the user interacts inside the panel.

### Modals

Use a dark translucent scrim to separate the modal from the page. Keep the dialog surface within the same dark palette and provide a clear close action. Trap focus while open, restore focus on close, and support Escape when dismissal is safe. On small screens, use a layout that remains usable without forcing tiny content into a desktop-shaped dialog.

### Badges and metadata chips

Badges are compact supporting information, not decorative stickers. Use a quiet dark translucent treatment over images and a subdued card treatment on plain surfaces. Keep labels short, consistent, and meaningful.

### Loading and empty states

Use skeletons that approximate the shape of the content being loaded, with low-contrast charcoal blocks. Avoid flashing or high-contrast shimmer. Empty states should explain why no content is present and, where appropriate, offer a next step. Error states should not look like ordinary empty states.

### Feedback

Use concise inline feedback for local actions and unobtrusive toasts for transient events. Avoid stacking multiple notifications over important content. Do not use colour alone to communicate success, warning, or failure.

## Motion and feedback

The reference uses short fades, upward entrances, image hover transitions, carousel fades, and small shifts to make interaction feel responsive.

Use motion with restraint:

- Prefer opacity and small positional changes for entering and leaving content.
- Use subtle image scale or lift on hover, without causing surrounding layout to jump.
- Keep menus and popovers responsive; animation must not delay interaction.
- Use smooth scrolling only for user-requested navigation, not as an always-running effect.
- Avoid parallax, large zooms, bouncing, or continuous decorative motion.
- Respect `prefers-reduced-motion`. Reduced motion must remove or simplify nonessential animation without hiding state changes.
- Avoid animating large blurred or full-screen layers when doing so causes poor performance, especially in constrained desktop WebViews.

Motion should be consistent across web and desktop builds. Where platform constraints differ, preserve the intent and timing hierarchy rather than forcing an identical rendering effect.

## Responsive web and desktop application behaviour

This design language is shared across browser and desktop application surfaces. The layout should adapt to the available content area rather than assuming a particular device category.

### Web

- Keep browser navigation and application navigation distinct. Do not imitate browser controls inside the page.
- Use a stable header and responsive navigation pattern.
- Preserve direct links and normal browser navigation semantics for content pages.
- Ensure sticky or fixed elements do not cover focused controls, anchors, or important page content.
- Make wide artwork and content rails usable with mouse, keyboard, touch, and trackpad.

### Desktop application

- Use the same content palette, typography, cards, and interaction states as the web experience.
- Integrate with the native window frame deliberately. Avoid duplicating operating-system title bars, window controls, or system menus.
- Make dense catalogue layouts take advantage of a wide window while maintaining sensible content widths and whitespace.
- Support keyboard shortcuts only when they map to clear, discoverable actions. Do not make essential actions shortcut-only.
- Ensure dialogs, menus, and floating panels stay within the application window and do not become clipped by the desktop shell.
- Treat window resizing as a normal layout change. Reflow columns and rails smoothly without losing the user's place or selected content.

### Touch and small viewports

- Convert full navigation into a compact menu when needed, but keep search straightforward to reach.
- Reflow detail views so artwork, title, actions, and metadata remain in a useful reading order.
- Ensure cards remain large enough to identify and select.
- Keep player controls touch-accessible and avoid hover-only interactions.
- Allow chips and filters to wrap or move into a filter panel; do not force horizontal overflow for essential controls.

## Accessibility and usability

- Maintain sufficient text and control contrast against the dark palette.
- Provide visible keyboard focus. Do not remove outlines without replacing them with a stronger focus indicator.
- Use semantic headings, landmarks, buttons, links, inputs, lists, and tab roles.
- Provide useful alternative text for meaningful artwork. Treat purely decorative background artwork as decorative.
- Give every icon-only action an accessible name.
- Ensure hover interactions have keyboard and touch equivalents.
- Do not encode state using colour alone; include text, iconography, or semantic attributes.
- Support browser zoom and desktop display scaling without clipping controls or content.
- Respect reduced-motion settings and avoid flashing effects.
- Keep player controls operable by keyboard and screen reader.
- Make loading, empty, offline, and error states understandable without relying on animation.

## Content and imagery

Artwork quality is central to this design. Use the best available image variant appropriate to the context: wide banner artwork for featured areas, portrait posters for catalogue cards and detail identity, and landscape thumbnails for video previews.

- Preserve source aspect ratios and crop intentionally.
- Use predictable fallbacks when artwork is missing or fails to load.
- Avoid layout shifts while images load by reserving their aspect ratio and surface area.
- Use gradients or scrims to protect text contrast rather than heavily darkening every image.
- Do not place important text inside images.
- Avoid generic stock imagery when the product's own media is available.

## Design consistency rules

1. Use the same background, card, border, foreground, and muted-text relationships throughout the product.
2. Reuse established button, card, badge, tab, dropdown, and modal patterns instead of inventing near-duplicates.
3. Keep primary actions visually obvious but scarce within each content area.
4. Give every interaction a complete set of states: default, hover, focus, active/selected, disabled, loading, and error where relevant.
5. Keep poster treatment, badge placement, title hierarchy, and metadata density consistent across catalogue surfaces.
6. Preserve a clear content hierarchy when the layout changes between narrow and wide viewports.
7. Do not introduce additional accent colours, decorative effects, or new corner styles without a clear product reason.
8. Do not let visual effects reduce readability, performance, or accessibility.
9. Avoid arbitrary fixed dimensions. Let image aspect ratios, content needs, and available space drive layout decisions.
10. Prefer a cohesive system over literal copying of one individual screen.

## Implementation guidance for designers and coding agents

Before creating or changing a UI:

1. Identify the user's primary task and the content hierarchy for the surface being designed.
2. Select the closest existing pattern from this specification: featured content, poster card, rail, grid, list, detail view, filter, modal, or player.
3. Reuse design tokens and existing components where possible.
4. Design all relevant interaction states, not only the initial screenshot.
5. Check the layout at narrow, medium, and wide available sizes, including a resizable desktop window where applicable.
6. Test mouse, keyboard, and touch interactions for the same core tasks.
7. Check missing images, long titles, empty results, loading, network failure, and media errors.
8. Verify reduced-motion and display-scaling behaviour.

Do not infer a product feature merely because it exists in the JustAnime reference. Do not copy the source repository's bugs, awkward edge cases, or implementation limitations. Reproduce the intended visual language and interaction quality, while choosing the implementation that best serves the target product.

## Reference implementation

The following source files were inspected to ground this specification in the JustAnime repository. Use them as visual and behavioural references, not as a requirement to copy their code verbatim.

- [Global visual tokens and styles](https://github.com/sankethodgar/JustAnime/blob/main/src/app/globals.css)
- [Root typography and application shell](https://github.com/sankethodgar/JustAnime/blob/main/src/app/layout.js)
- [Landing page and search suggestions](https://github.com/sankethodgar/JustAnime/blob/main/src/app/page.jsx)
- [Shared page layout and footer](https://github.com/sankethodgar/JustAnime/blob/main/src/components/SharedLayout.js)
- [Main navigation and search](https://github.com/sankethodgar/JustAnime/blob/main/src/components/Navbar.js)
- [Poster card](https://github.com/sankethodgar/JustAnime/blob/main/src/components/AnimeCard.js)
- [Horizontal catalogue rail](https://github.com/sankethodgar/JustAnime/blob/main/src/components/AnimeRow.js)
- [Featured spotlight carousel](https://github.com/sankethodgar/JustAnime/blob/main/src/components/SpotlightCarousel.js)
- [Detail view](https://github.com/sankethodgar/JustAnime/blob/main/src/components/AnimeDetails.js)
- [Tabs and catalogue selection](https://github.com/sankethodgar/JustAnime/blob/main/src/components/AnimeTabs.js)
- [Catalogue filters](https://github.com/sankethodgar/JustAnime/blob/main/src/components/AnimeFilters.js)
- [Release calendar](https://github.com/sankethodgar/JustAnime/blob/main/src/components/AnimeCalendar.js)
- [Video player and playback controls](https://github.com/sankethodgar/JustAnime/blob/main/src/components/VideoPlayer.js)

---

**Design direction in one sentence:** a restrained, near-black cinematic interface where artwork leads, navigation stays compact, metadata stays quiet, and every interaction feels direct and consistent across web and desktop.
