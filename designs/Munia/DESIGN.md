# Munia-Inspired UI/UX Design Specification

## 1. Purpose and scope

This document defines a reusable visual and interaction language inspired by [Munia](https://github.com/leandronorcio/munia). It is intended for human designers, developers, and LLM coding agents creating web applications, desktop applications, or products delivered on both.

The goal is to preserve Munia's design character: a welcoming, accessible, content-centred interface; a vivid violet identity; soft rounded surfaces; prominent user imagery; clear content hierarchy; and restrained, responsive interaction feedback.

This is a design specification, not a product requirements document. It does not require the application to be a social network or to reproduce Munia's feature set. Apply only the patterns that fit the product's actual tasks.

Primary reference: <https://github.com/leandronorcio/munia>

### Repository analysis and reference scope

The repository tree was inventoried across application routes, shared components, UI primitives, contexts, hooks, SVG components, styles, configuration, and supporting code. The design review focused on the global theme tokens, root typography, public landing page, protected application shell, navigation, feed and discovery, profile surfaces, posts and comments, post composition, media viewing, form controls, dialogs, notifications, theme switching, and motion patterns.

The reference implementation uses Next.js, React, TypeScript, Tailwind CSS, React Aria, Framer Motion, and a bespoke SVG icon family. These are implementation details of the reference, not mandatory technologies for a product following this specification.

Useful source references:
- [Global design tokens](https://github.com/leandronorcio/munia/blob/main/src/app/globals.css)
- [Tailwind theme extension](https://github.com/leandronorcio/munia/blob/main/tailwind.config.js)
- [Root layout and typography](https://github.com/leandronorcio/munia/blob/main/src/app/layout.tsx)
- [Public landing page](https://github.com/leandronorcio/munia/blob/main/src/app/%28unprotected%29/page.tsx)
- [Protected application shell](https://github.com/leandronorcio/munia/blob/main/src/app/%28protected%29/layout.tsx)
- [Navigation menu](https://github.com/leandronorcio/munia/blob/main/src/components/MenuBar.tsx)
- [Navigation item states](https://github.com/leandronorcio/munia/blob/main/src/components/MenuBarItem.tsx)
- [Post presentation](https://github.com/leandronorcio/munia/blob/main/src/components/Post.tsx)
- [Comment presentation](https://github.com/leandronorcio/munia/blob/main/src/components/Comment.tsx)
- [Post composer](https://github.com/leandronorcio/munia/blob/main/src/components/CreatePostDialog.tsx)
- [Profile header](https://github.com/leandronorcio/munia/blob/main/src/app/%28protected%29/%5Busername%5D/%28tabs%29/ProfileHeader.tsx)
- [Discovery profile cards](https://github.com/leandronorcio/munia/blob/main/src/components/DiscoverProfile.tsx)
- [Button variants](https://github.com/leandronorcio/munia/blob/main/src/components/ui/variants/buttonVariants.ts)
- [Text input](https://github.com/leandronorcio/munia/blob/main/src/components/ui/TextInput.tsx)
- [Theme switching](https://github.com/leandronorcio/munia/blob/main/src/contexts/ThemeContext.tsx)
- [Toast presentation](https://github.com/leandronorcio/munia/blob/main/src/components/ui/Toast.tsx)
- [Media viewer](https://github.com/leandronorcio/munia/blob/main/src/components/VisualMediaSlider.tsx)

---

## 2. Design character

The interface should feel welcoming, expressive, soft but structured, content-first, and accessible.

- **Welcoming:** rounded geometry, approachable typography, human imagery, and clear language.
- **Expressive:** violet is the recognisable accent, supported by restrained semantic colours.
- **Content-first:** content and media have more visual weight than application chrome.
- **Soft but structured:** rounded surfaces are balanced by alignment, borders, and consistent spacing.
- **Responsive:** navigation and composition adapt to available space rather than merely shrinking.
- **Accessible:** controls expose purpose and state; keyboard and assistive-technology use are first-class.

Establish hierarchy in this order: page identity or heading; main content; user identity and context; primary actions; secondary actions and metadata. Avoid giving every element equal emphasis.

Use a calm, centred composition with a readable content region and a distinct but visually quiet navigation area. Cards should group related content, not wrap every label or line of text.

---

## 3. Colour system

Munia's identity uses saturated violet, deep plum-toned dark surfaces, pale lavender-tinted light surfaces, and restrained semantic colours. Use semantic tokens rather than raw colours scattered through components.

The RGB values below are taken from the reference CSS variables. Treat them as palette anchors, not inflexible values; preserve contrast and adjust when necessary for the target display.

### Light theme

| Token | RGB | Role |
|---|---:|---|
| `background` | `254 253 255` | Near-white page surface with a violet cast |
| `foreground` | `16 0 35` | Main text |
| `card` | `253 250 255` | Raised content surface |
| `card-foreground` | `60 0 119` | Card text |
| `popover` | `251 251 254` | Menus and floating surfaces |
| `primary` | `136 0 202` | Main brand action |
| `primary-accent` | `163 0 241` | Hover/stronger primary |
| `secondary` | `237 238 243` | Secondary surface |
| `secondary-foreground` | `77 81 104` | Secondary text |
| `muted` | `204 208 222` | Quiet fills and separators |
| `muted-foreground` | `77 81 104` | Supporting text |
| `accent` | `125 11 239` | Selected emphasis |
| `border` | `241 224 253` | Soft lavender border |
| `input` | `238 239 249` | Input surface |

### Dark theme

| Token | RGB | Role |
|---|---:|---|
| `background` | `16 0 35` | Deep plum page surface |
| `foreground` | `251 243 255` | Main text |
| `card` | `35 27 56` | Raised content surface |
| `card-foreground` | `231 206 255` | Card text |
| `popover` | `24 31 41` | Menus and floating surfaces |
| `primary` | `177 58 255` | Main brand action |
| `primary-accent` | `169 38 255` | Hover emphasis |
| `secondary` | `40 42 54` | Secondary surface |
| `secondary-foreground` | `204 208 222` | Secondary text |
| `muted` | `77 81 104` | Quiet fills and separators |
| `muted-foreground` | `204 208 222` | Supporting text |
| `accent` | `94 0 156` | Deeper accent surface |
| `border` | `57 49 75` | Subtle plum border |
| `input` | `57 49 75` | Input surface |

### Semantic colours and rules

Use separate success, warning, destructive, and informational treatments. The reference uses green for success, amber/yellow for warning, and pink/red for destructive feedback. Semantic colour must be paired with text, iconography, or another cue; never communicate meaning through colour alone.

- Reserve saturated violet for primary actions, active navigation, focus, and selected states.
- Keep large backgrounds quiet and low-contrast.
- Use muted foreground tokens for timestamps, counts, and helper text.
- Distinguish cards from the page without heavy shadows.
- Do not make every icon and link violet.
- Meet WCAG contrast requirements in both themes.
- Support light, dark, and system preferences when themes are offered.
- Theme changes must update all semantic tokens consistently.

---

## 4. Typography

The reference uses **Poppins** at weights 400, 500, 600, and 700. Its rounded geometric forms contribute to the friendly character. Use Poppins when available and appropriately licensed; otherwise choose a similar geometric sans-serif and provide robust system fallbacks.

Maintain a clear hierarchy:
- Page titles: prominent and bold.
- Section titles: semibold and subordinate to page titles.
- Card/profile titles: semibold and easy to scan.
- Body text: regular weight with comfortable line height.
- Metadata: smaller and muted, but still legible.
- Buttons: semibold, concise labels.
- Form labels: persistent and explicit; placeholders are not labels.

Use readable line lengths. Allow biographies, posts, and comments to wrap naturally. Do not truncate important user-generated content without an expand affordance. Keep timestamps and counts subordinate. Ensure long usernames, URLs, and hashtags cannot cause horizontal overflow.

---

## 5. Shape, borders, elevation, and spacing

### Geometry

Rounded corners are a defining part of the visual language. Use a coherent scale: small for compact controls and tags; medium for inputs and buttons; large for cards and dialogs; extra-large for profile/discovery surfaces; fully rounded for avatars and pill actions. Do not mix unrelated radii within a component family.

### Borders and elevation

Prefer thin, low-contrast borders. Increase contrast for focus, validation, and selected states. Use separators sparingly. Cards may use subtle surface contrast or a soft shadow. Menus and dialogs need enough elevation to read as foreground layers. Avoid heavy shadows around ordinary content and do not use shadows as a substitute for grouping.

### Spacing

Use a consistent spacing scale based on a small base unit. Apply it to card padding, avatar/text gaps, feed rhythm, navigation items, form fields, dialog sections, and page margins. Give content room to breathe. On narrow screens, reduce outer margins before reducing internal touch-target sizes.

---

## 6. Application shell and navigation

The reference uses a persistent side navigation on wider layouts and a bottom navigation bar on compact layouts. Navigation is icon-led, with labels visible in the wider presentation.

### Wide layout

Use a stable side navigation region beside the main content. Keep it visually quiet. The reference places the brand mark and wordmark above the destination list. Do not hard-code its exact width; accommodate labels, accessible hit areas, and the product's actual navigation structure.

### Compact layout

Move primary navigation to a bottom bar or another persistent compact pattern suitable for the platform.

- Centre and evenly distribute icons.
- Use a clear active indicator, such as a short violet bar.
- Respect safe areas.
- Prevent the bar from obscuring content, media controls, or form actions.
- Add bottom content padding to account for the navigation.
- If there are too many destinations, use a deliberate overflow pattern rather than shrinking labels.

### States

The reference uses a vertical violet marker in the side rail and a horizontal marker in the bottom bar. Hover uses a subtle primary-tinted surface.

- Default: muted icon and label.
- Hover: subtle tinted surface or icon emphasis.
- Active: persistent violet marker and stronger label weight.
- Keyboard focus: clearly visible focus ring.
- Disabled: reduced emphasis and no misleading hover feedback.

Active state must be communicated by more than colour. Make the entire navigation item interactive, not only its icon or text. Notification counts may appear as small badges attached to the relevant item.

---

## 7. Content surfaces and feed-like cards

Use rounded cards with a slightly raised surface, consistent padding, and predictable hierarchy. A card should make content easier to scan. Avoid nesting cards unless there is a genuinely separate grouping.

For a stream of content, use a vertical sequence of cards with consistent spacing. A post-like item may contain:
1. Author row: avatar, display name, handle/context, timestamp, optional actions.
2. Main text or rich content.
3. Optional media.
4. Action row with controls and counts.
5. Optional expanded discussion or related content.

Keep the author row compact. The content itself has the strongest priority.

User-generated text should wrap naturally. Mentions and hashtags may be styled as interactive links, but do not colour all text with the accent. Keep edit/delete actions in a predictable contextual menu.

### Discussion and nested content

Comments and replies should communicate hierarchy without excessive borders or boxes. Use avatar alignment to establish authorship. Keep author name and timestamp close to the comment. Keep reaction and reply actions compact. Indent replies enough to show relationship while preserving width on mobile. Provide clear expand/collapse labels. A comment opened through a deep link may receive a temporary accessible highlight.

---

## 8. Identity, avatars, and profile surfaces

Profile imagery is central to the reference's human, community-oriented character.

### Avatars

- Use circular avatars consistently.
- Provide a predictable fallback when no image exists (initials or a simple profile mark).
- Keep sizes consistent within each context.
- Preserve image aspect ratio; never stretch.
- Use meaningful alternative text when the image conveys identity; use empty alt text when adjacent text already identifies the person.

### Profile header

The reference uses a wide cover image, overlapping avatar, identity details, relationship counts, actions, and a tab row.

- Treat the cover as context, not as a place for essential text.
- Anchor the avatar so it visibly overlaps the cover.
- Place the primary profile action near the identity block.
- Make display name strongest, followed by handle and biography.
- Present counts as secondary metadata.
- Keep profile navigation in a distinct tab strip.
- Adapt overlap and tabs for narrow screens without clipping controls.

### Discovery cards

The reference discovery cards use a coloured upper region with a centred avatar and actions, followed by a body containing name, biography, and counts. Keep the header colour restrained, centre identity, align actions consistently, and allow biographies to wrap. Use a neutral fallback when no contextual accent is appropriate. Do not generalise identity- or gender-coded colour treatments into a universal rule.

---

## 9. Buttons and action controls

Use a small, consistent set of button modes:

- **Primary:** solid violet with high-contrast text; use for the main action in a region.
- **Secondary:** muted neutral fill for alternative actions.
- **Subtle/outline:** transparent surface with violet border or text for visible lower-priority actions.
- **Ghost:** minimal surface for icon actions and low-emphasis controls.

Do not place multiple competing primary buttons together. Maintain coherent size variants. Use pill shapes for selected prominent actions where appropriate, and circular icon-only buttons for familiar single-purpose actions. Every icon-only button needs an accessible name.

Buttons need distinct default, hover, pressed, focus-visible, loading, and disabled states. The reference uses subtle press scaling and ring feedback; keep this restrained and avoid shifting surrounding layout. Loading must prevent duplicate submission while preserving button dimensions. Disabled controls must be visibly and functionally disabled.

---

## 10. Forms and text entry

### Inputs

The reference uses rounded filled inputs, floating labels, optional leading icons, and a clear affordance.

- Use a quiet, slightly contrasting input surface.
- Keep the label visible after entry.
- Add leading icons only when they improve recognition.
- Show a clear action only when clearing is useful.
- Place validation feedback near the field.
- Distinguish focus and error states without colour alone.
- Never use placeholder text as the only label.

### Text composition

Long-form composition areas should feel open and uncluttered. Provide adequate writing space and a clear prompt. Keep submission actions easy to find. Preserve typed content after validation errors. Show selected attachments as previews with obvious removal and reordering controls where relevant. Confirm before discarding meaningful unsaved work.

### Search and filters

Make search discoverable without allowing it to dominate. Use explicit labels, group related filters, show selected states, make clearing easy, and preserve query/filter state when appropriate. On narrow layouts, let filters wrap or move into a compact panel.

---

## 11. Dialogs, menus, popovers, and overlays

### Dialogs

Use rounded, elevated surfaces with a distinct title, content region, and action area.

- Make the title immediately discoverable.
- Keep primary and secondary actions in a predictable order.
- Provide a clear close affordance.
- Support Escape where appropriate.
- Move focus into the dialog, contain it for modal dialogs, and restore it to the trigger on close.
- Do not close when users interact inside the dialog.
- Confirm when closing would discard meaningful unsaved work.

### Menus and popovers

Use compact floating surfaces with readable labels and predictable spacing. Group related actions; use separators sparingly; distinguish destructive actions; support keyboard navigation and Escape; keep the surface within the viewport. Use popovers for contextual content that needs more room than a tooltip. A tooltip must never be the only way to understand a control.

---

## 12. Media and image presentation

The reference supports image/video content in posts and a dedicated full-screen media viewer.

### Inline media

Keep media within the content width, use rounded clipping consistent with the card, preserve intrinsic aspect ratio, and avoid arbitrary cropping of user uploads. For multiple assets, use a clear grid or carousel. Provide an obvious way to open the larger viewer.

### Full-screen viewer

Focus attention on the selected asset and reduce surrounding interface noise. Use a dark viewing surface, visible close/navigation controls, keyboard navigation, and position/pagination when multiple assets exist. Support zoom/pan when useful. Label previous, next, zoom, and close controls accessibly. Keep video controls usable and support captions when available.

### Loading and failure

Use stable placeholders that preserve layout. A failed image or video should show a useful fallback rather than a broken browser element.

---

## 13. Notifications, feedback, and status

### Toasts

The reference uses rounded toast surfaces with a semantic icon, title, optional message, and close action.

- Success: green semantic treatment.
- Warning: amber treatment.
- Error: destructive treatment.
- Neutral/informational: quiet neutral or violet treatment.

Keep messages concise and actionable. Do not make a toast the only record of an important error.

### Notification items

Communicate who or what caused the event, what happened, and when. Use an avatar or contextual icon, readable event text, and a small visible unread indicator. Distinguish read/unread without overwhelming the content. Make navigable notifications keyboard accessible.

### Loading, empty, and error states

Design these as part of each component:
- Loading: restrained spinner or skeleton; preserve expected layout.
- Empty: explain why the region is empty and offer a relevant next action when useful.
- Error: state what failed in plain language and offer retry where useful.
- End of content: use a quiet completion message rather than unexplained blank space.

Avoid flashing large loading indicators for brief operations.

---

## 14. Motion and transitions

The reference uses Framer Motion for content entrance/exit, dialog transitions, expanding comments, and theme-switch animation. Motion should clarify state changes, not decorate every interaction.

- Keep transitions short and purposeful.
- Prefer opacity and small positional changes.
- Animate height only when content genuinely expands or collapses.
- Avoid large overshoots, elastic movement, or constant ambient animation.
- Prevent surrounding content from jumping unexpectedly.
- Keep direct manipulation, such as dragging media, immediate.
- Navigation markers may use short scale/position transitions.
- Dialogs may use restrained entrance/exit transitions.
- Button press may use slight scale or colour feedback.
- Theme changes should update tokens consistently without prolonged transitions that reduce legibility.

Respect `prefers-reduced-motion`. Remove nonessential movement or replace it with immediate state changes/simple opacity transitions.

---

## 15. Responsive behaviour: web and desktop

The same visual language should work in browser windows, desktop application windows, tablets, and phones. Responsiveness changes composition; it does not merely scale the desktop interface down.

### Wide screens

Use a side navigation rail when it improves orientation. Keep primary content at a readable measure. Use additional width for secondary panels or multi-column discovery only when useful. Do not stretch text-heavy content across the display. Keep dialogs and media viewers proportionate.

### Medium screens

Reduce outer margins. Preserve comfortable card padding and touch targets. Collapse secondary columns before the main content becomes cramped. Keep navigation labels where they fit; otherwise use a deliberate compact state.

### Narrow screens

Use compact or bottom navigation. Stack content into a primary column. Allow filters and action groups to wrap. Keep media within the viewport. Prevent fixed navigation from covering content. Keep important actions reachable without precise pointer movement.

### Desktop application windows

- Keep navigation and content hierarchy consistent with the web version.
- Follow host-platform window controls and title-bar conventions unless using a deliberate, accessible custom title bar.
- Do not use mobile bottom navigation in a spacious desktop window.
- Support resizing and smaller-than-default window sizes.
- Ensure menus, dialogs, and popovers are not clipped.
- Use native file pickers and system affordances when they improve the task.
- Treat keyboard shortcuts as enhancements, not replacements for visible controls.

Test narrow phone, tablet, laptop, and large desktop widths. Also test resized desktop windows, browser zoom, and increased system text scaling. Choose breakpoints when content or navigation needs to change; do not impose arbitrary fixed dimensions.

---

## 16. Accessibility

Accessibility is part of the reference's stated design intent and must be preserved.

- Use semantic HTML and landmarks.
- Make every interactive element keyboard reachable.
- Provide visible focus indicators.
- Give icon-only controls accessible names.
- Associate labels and validation messages with fields.
- Manage focus correctly in dialogs and menus.
- Support keyboard operation for tabs, listboxes, popovers, and media viewers.
- Maintain sufficient contrast in both themes.
- Never communicate state through colour alone.
- Provide meaningful alt text for informative imagery.
- Provide captions for video when available.
- Respect reduced-motion preferences.
- Keep touch targets comfortably sized.
- Do not disable browser zoom.
- Ensure enlarged text and assistive technologies work with responsive layouts.

Use an accessibility-focused component library or well-tested primitives. The reference uses React Aria; it is not mandatory, but equivalent behaviour is.

---

## 17. Iconography

The reference uses a bespoke family of consistent stroke-based SVG icons.

- Prefer simple, recognisable line icons.
- Keep stroke weight and optical size consistent.
- Use the same icon for the same action throughout the product.
- Reserve brand colour for active or primary states.
- Avoid mixing filled, outlined, and multicolour icon families without a deliberate system.
- Do not use emoji as substitutes for core interface icons.
- Hide decorative icons from assistive technology; label the containing control.

---

## 18. Interaction principles

Every control must provide an understandable response.

- Navigation updates the active destination.
- Likes, follows, and toggles visibly reflect their state.
- Menus open from their trigger and close predictably.
- Forms show validation near the relevant field.
- Submission controls show pending and completion states.
- Destructive actions communicate consequences and request confirmation when difficult to reverse.
- Drag-and-drop provides visible feedback and a non-drag alternative where practical.
- Infinite loading must not lose the user's position or cause sudden scroll jumps.
- New content should be discoverable without interrupting reading.

Use optimistic feedback only when the application can recover gracefully from a failed operation.

---

## 19. Tokens and component architecture

Centralise semantic tokens for:
- Theme and semantic colours.
- Typography families, weights, and scale.
- Spacing.
- Border widths and radii.
- Elevation.
- Focus-ring treatment.
- Motion durations and easing.
- Responsive layout rules.

Create reusable primitives for buttons, icon buttons, text inputs, text areas, badges, avatars, cards, tabs, menus, popovers, dialogs, toasts, and loading/empty/error states.

Components should expose meaningful semantic variants, not one-off page-specific styles. Keep content components composable: a post-like card should be assembled from identity, content, media, and action regions rather than becoming an isolated monolith.

---

## 20. Product-specific adaptation

This specification describes Munia's visual language, not a requirement to recreate its social-network feature set.

- Retain the violet-led semantic palette unless the product has a strong reason for another brand colour.
- Retain rounded, soft surfaces and clear content grouping.
- Retain typography and hierarchy principles.
- Adapt navigation to the product's information architecture.
- Use profile, feed, comment, and media patterns only when the product has equivalent content relationships.
- Do not add social features merely because the reference contains them.
- Do not force every screen into a card layout.
- Do not generalise context-specific or identity-coded visual treatments into universal design rules.
- Keep the interface coherent when the product has no avatars, feeds, posts, or profiles.

The result should be recognisably Munia-inspired without copying product-specific content or imposing irrelevant structures.

---

## 21. Quality checklist

An implementation aligns with this specification when:
- The violet accent is recognisable but not overused.
- Light and dark themes use coordinated semantic tokens.
- Typography has a consistent hierarchy.
- Rounded surfaces, borders, and shadows feel like one system.
- Main content is more prominent than application chrome.
- Navigation clearly indicates the active destination.
- Cards have consistent spacing and content structure.
- Buttons, inputs, menus, and dialogs share coherent states.
- User identity and media are presented without distortion.
- Loading, empty, error, and success states are designed.
- Motion clarifies interaction and respects reduced-motion settings.
- Layouts adapt from narrow to wide viewports.
- Desktop windows remain usable when resized.
- Keyboard navigation, focus, labels, and contrast are verified.
- No fixed page structure or irrelevant product feature has been imposed.

## 22. Implementation instruction

Treat this file as the visual and interaction source of truth. Before building a screen, identify its content hierarchy and the user's primary task. Select only patterns that fit. Reuse shared tokens and component variants. Do not invent a second visual language for individual pages.

When a requirement conflicts with this specification, preserve usability, accessibility, and the product's actual task first, then adapt the Munia-inspired styling around it. Do not sacrifice legibility or interaction clarity for superficial resemblance.
