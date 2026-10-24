# USCC Campaign Studio Design System

## 1. Assumptions and system architecture

### Assumptions
- This is a campaign operations and intake product used by marketer, campaign managers, delivery teams, and approvers.
- The primary workspace is an operations board for lifecycle management; the secondary experience is a guided campaign creation flow.
- The application must support both operational speed and operational clarity.
- A single shared system supports two coordinated themes: `Operations Board` (dark) and `Guided Studio` (light).
- `Ask Little Joe` is a demo AI assistant that explains context, proposes next steps, and requires explicit review before a change is applied.
- The design system is implementation-ready for React + TypeScript + CSS custom properties.

### System architecture
The system uses a layered token model with three levels:

1. Primitive tokens: raw foundations such as colors, spacing, sizes, radii, fonts, and durations.
2. Semantic tokens: purpose-based values such as canvas, surface, text, border, action, focus, and status.
3. Component tokens: UI-specific values for buttons, cards, navigation, inputs, tables, and AI messages.

This solves the theme problem cleanly:
- Components reference semantic or component tokens.
- Themes change token values without changing component logic.
- The same components work in both dark and light environments.
- Values are documented, versioned, and reviewable.

### Theme model
- Theme A: `operations-dark`
- Theme B: `studio-light`

The root attribute is:

```html
<div data-theme="operations-dark">...</div>
<div data-theme="studio-light">...</div>
```

This approach makes theme switching predictable for product engineers, documentation authors, and designers.

---

## 2. Design system principles

### 1) Make the next action clear
A campaign plan is not just a list of tasks; it is a workflow that tells people what to do next.

How it affects design:
- Primary, high-confidence next actions are emphasized in layout and interaction patterns.
- Dead ends are minimized by surfacing required fields and blockers before action buttons.
- Empty states do not simply say “no data”; they explain what to do next.
- Example: in a blocked campaign, the CTA is “Review blocker” or “Request creative hand-off” instead of a generic “Open campaign.”

### 2) Preserve context while users work
Campaign work is complex and cross-cutting. People need to keep the same record and same process in view while they act.

How it affects design:
- Persistent filters, selected campaign context, and the status bar stay visible.
- The AI assistant keeps campaign context attached to the correct campaign.
- Forms preserve unsaved input when users switch steps or navigate across views.
- Example: the assistant in a right-side panel remains tied to the selected campaign, not to the last prompt alone.

### 3) Explain issues before proposing actions
The product should help people understand why something is blocked or at risk before recommending a solution.

How it affects design:
- Status surfaces include concise explanation: “Creative hand-off pending” and “Audience requirements incomplete.”
- AI suggestions are framed as recommendations, not certainty.
- Action previews show the current value, proposed value, and impact before confirmation.
- Example: “Creative asset review is still outstanding, which blocks channel execution.”

### 4) Make dense information easy to compare
Campaign operations creates dense tables, long lists, and many related fields.

How it affects design:
- Table columns are aligned and use tabular numerals.
- Cards prioritize the most important fields: ID, title, channel, owner, deployment date, and blocker.
- Filter workflows and array layouts use consistent ordering and visible grouping.
- Example: campaign cards share the same structure across columns so users can compare quickly.

### 5) Keep AI suggestions distinguishable from saved data
AI output must never feel like it is the authoritative source record.

How it affects design:
- AI messages use a clear assistant identity and distinct surface treatment.
- Suggested values and recommendations are visually separated from persisted campaign data.
- Proposed changes are shown in a dedicated review state before confirmation.
- Example: a recommended “Move campaign to Execution Ready” appears as AI suggestion, not as an already-saved object.

### 6) Use consistent patterns across themes
The same system needs to feel coherent even when the mood and surface language differ.

How it affects design:
- Shared token names, component shapes, form logic, and interaction states are consistent across themes.
- The dark theme accentuates operational speed; the light theme emphasizes calm guidance.
- Differences are in tone, not in conceptual model.
- Example: both themes use the same button states, field patterns, and confirmation flows.

### 7) Build accessibility into every component
Accessibility is not a separate layer; it is part of the baseline design system.

How it affects design:
- All interactive targets meet or exceed minimum sizing.
- Contrast is checked for text, status surfaces, and focus states.
- Keyboard access is a first-class requirement.
- Screen-reader associations, status announcements, and focus management are built into every pattern.
- Example: validation messages are connected to form fields and announced as errors without relying on color alone.

---

## 3. Shared foundations

### Typography
Use Manrope for headings and DM Sans for body text and controls.
Fallback stacks:
- Headings: `"Manrope", "Avenir Next", "Segoe UI", sans-serif`
- Body: `"DM Sans", "Segoe UI", "Helvetica Neue", sans-serif`
- Monospace (where used): `"SFMono-Regular", "Consolas", monospace`

Named roles:
- Display: 40/48px, 700
- Page title: 32/40px, 700
- Section title: 22/30px, 700
- Panel title: 18/26px, 600
- Card title: 14/21px, 600
- Body: 14/22px, 400
- Comfortable body: 15/24px, 400
- Compact body: 12/18px, 400
- Control label: 13/18px, 600
- Metadata: 11/17px, 400
- Eyebrow: 10/15px, 700, letter-spacing 1.2px

Responsive heading behavior:
- On desktop, use the defined role scale.
- On tablet, page titles may reduce to 28/36px.
- On mobile, section titles compress to 18/24px; body remains readable and not under 14px.
- Use tabular numerals for counts, dates, capacity, and numeric comparisons.

### Spacing
Base unit: 4px.
Scale: `4, 8, 12, 16, 20, 24, 32, 40, 48, 64`

Recommended uses:
- Inline gaps: 4, 8, 12
- Control padding: 8, 12, 16
- Card padding: 16, 20
- Form spacing: 12, 16, 20, 24
- Section spacing: 24, 32, 40
- Page gutters: 24, 32, 40

### Shape and border
- Control radius: 8px
- Card and panel radius: 12px
- Composer radius: 16px
- Modal radius: 16px
- Badge radius: 4–6px
- Pill radius: chips and filters
- Viewport-attached drawers: square outer edges

Border treatments:
- Subtle border: low-contrast separation for surfaces
- Default border: standard control and row boundaries
- Strong border: important state grouping and selected elements
- Selected border: accent-tinted border for focused selection
- Error border: danger status for validation states
- Focus border: 2px ring or equivalent high-visibility treatment

### Elevation
Small elevation scale:
- Base surfaces: no shadow or minimal ring
- Dropdowns/popovers: 8px blur, subtle shadow
- Drawers: 16px blur, layered offset
- Dialogs: 20px blur, moderate shadow
- Notifications: 24px blur, subtle contrast

Use theme-specific shadow values rather than a universal black shadow.

### Iconography
- One consistent SVG icon family across all themes.
- Standard sizes: 16, 20, 24px.
- Stroke width: 1.5–2px depending on size.
- Icons align to the baseline of labels and controls.
- When meaning is ambiguous, pair an icon with a label.
- Icon-only actions require an accessible name.

### Motion
Duration values:
- Fast: 120–160ms
- Standard: 180–240ms

Easing tokens:
- Standard ease: `cubic-bezier(0.2, 0, 0.1, 1)`
- Emphasized ease: `cubic-bezier(0.2, 0, 0, 1)`

Rules:
- Motion communicates state and spatial relationships.
- Respect `prefers-reduced-motion`.
- Avoid decorative looping animation.
- Do not animate critical content or status message appearance in a way that blocks comprehension.

### Density
Support two densities:
- Comfortable: default for most interactions
- Compact: for dense tables and operation boards

Density adjustments should change padding and row height, not the essential text size.

---

## 4. Layout system

### Core dimensions
- Desktop sidebar: 200–220px
- Header: 64–72px
- Content gutters: 24–40px
- Focused form width: 640–760px
- General content maximum: 1280–1440px
- AI companion width: 360–420px
- Board columns: 260–320px
- Column gap: 16–20px

### Breakpoints
- Small: `< 640px`
- Medium: `640–1023px`
- Large: `1024–1439px`
- XL: `1440px+`

Behavior by breakpoint:
- Small: collapse nav to icon rail or drawer; preserve filters in a top sheet; move AI companion into a bottom sheet or tab; keep CTA region visible.
- Medium: keep nav collapsed; show board columns with horizontal scroll; stack side panels below content when needed.
- Large: use the full dual-panel layout with persistent right-side AI assistant.
- XL: allow wider data grids and expanded campaign detail drawers while keeping content centered at 1280–1440px.

### Supported layouts
1. Dashboard with summaries and priorities
2. Board with horizontally scrollable columns
3. Campaign table with filters
4. Guided campaign form
5. Workspace with persistent right-side AI companion
6. AI answer page with evidence and actions

### Small-screen rules
- Collapse navigation.
- Preserve access to filters.
- Keep critical actions visible.
- Move assistant to a dedicated tab or expandable panel.
- Preserve draft and conversation state when switching views.
- Avoid page-level horizontal overflow.
- Allow intentional horizontal scrolling inside boards and tables.

---

## 5. Theme A: Operations Board — dark

### Design character
Focused, precise, composed, and dependable.

### Palette
- Canvas: `#101719`
- Navigation: `#131C1F`
- Default surface: `#192225`
- Raised surface: `#202C2F`
- Hover surface: `#253337`
- Selected surface: `#25392E`
- Subtle border: `#2B383A`
- Strong border: `#4A5D5A`
- Primary text: `#E7EEEB`
- Secondary text: `#B2C0BB`
- Muted text: `#8FA49D`
- Inverse text: `#17271C`
- Primary accent: `#B6ED82`
- Accent hover: `#C8F49E`
- Accent pressed: `#9FD66B`
- Accent subtle: `#25392E`
- Success foreground: `#A8DDB7`, background: `#20372B`
- Warning foreground: `#F6BC85`, background: `#4A3225`
- Danger foreground: `#F3A5AC`, background: `#45282E`
- Information foreground: `#A7C8F3`, background: `#25364B`

### Rules
- Avoid pure black backgrounds.
- Avoid neon accents.
- Avoid decorative glows and heavy gradients.
- Keep pressure on borders and surface changes instead of dramatic shadows.
- Do not overcolor lifecycle stages; rely on labels and structure as much as color.

### Usage guidance
Use the dark theme for operational work and board comparison. It supports dense scanning and fast triage with calm, restrained accent color.

---

## 6. Theme B: Guided Studio — light

### Design character
Calm, welcoming, thoughtful, and capable.

### Palette
- Canvas: `#F8F6F1`
- Navigation: `#F1EFE7`
- Default surface: `#FFFEFA`
- Raised surface: `#FFFFFF`
- Hover surface: `#F3F3EB`
- Selected surface: `#E8EEE2`
- Subtle border: `#E3E2D8`
- Strong border: `#B5BCAF`
- Primary text: `#303B34`
- Secondary text: `#626D60`
- Muted text: `#727A6B`
- Inverse text: `#FFFFFF`
- Primary accent: `#3D6650`
- Accent hover: `#315540`
- Accent pressed: `#274735`
- Accent subtle: `#E8EEE2`
- Success foreground: `#286346`, background: `#E7F1E8`
- Warning foreground: `#8C5C18`, background: `#FFF3DB`
- Danger foreground: `#A5353F`, background: `#FBECEF`
- Information foreground: `#355D78`, background: `#EAF1F6`
- Guidance surface: `#ECEEDE`
- Guidance text: `#536247`

### Rules
- Avoid stark white dashboards.
- Avoid excessive floating cards.
- Avoid decorative pastels without meaningful use.
- Avoid purple gradients and oversized AI symbols.
- Keep motion subtle and purposeful.

### Usage guidance
Use the light theme for guided authoring, intake, briefs, and review steps. It creates a sense of clarity and reassurance while preserving a businesslike tone.

---

## 7. Token system

### Primitive tokens
These are raw values.

```json
{
  "primitive": {
    "color": {
      "palette": {
        "charcoal": { "900": "#101719", "800": "#131C1F", "700": "#192225", "600": "#202C2F", "500": "#253337", "400": "#25392E" },
        "forest": { "900": "#274735", "800": "#315540", "700": "#3D6650", "600": "#536247" },
        "lime": { "500": "#B6ED82", "600": "#C8F49E", "700": "#9FD66B" },
        "sage": { "100": "#E8EEE2", "200": "#ECEEDE" },
        "success": { "100": "#E7F1E8", "500": "#286346" },
        "warning": { "100": "#FFF3DB", "500": "#8C5C18" },
        "danger": { "100": "#FBECEF", "500": "#A5353F" },
        "info": { "100": "#EAF1F6", "500": "#355D78" }
      },
      "fontSize": {
        "display": "40px",
        "pageTitle": "32px",
        "sectionTitle": "22px",
        "panelTitle": "18px",
        "cardTitle": "14px",
        "body": "14px",
        "comfortBody": "15px",
        "compactBody": "12px",
        "controlLabel": "13px",
        "metadata": "11px",
        "eyebrow": "10px"
      },
      "space": ["4px", "8px", "12px", "16px", "20px", "24px", "32px", "40px", "48px", "64px"],
      "radius": { "control": "8px", "card": "12px", "composer": "16px", "modal": "16px", "badge": "6px" },
      "duration": { "fast": "140ms", "standard": "200ms" }
    }
  }
}
```

### Semantic tokens
Purpose-based tokens create consistency across both themes.

Examples:
- `color.background.canvas`
- `color.surface.default`
- `color.surface.raised`
- `color.surface.hover`
- `color.surface.selected`
- `color.border.subtle`
- `color.border.strong`
- `color.text.primary`
- `color.text.secondary`
- `color.text.muted`
- `color.action.primary.background`
- `color.action.primary.text`
- `color.status.success.foreground`
- `color.status.success.background`
- `color.status.warning.foreground`
- `color.status.warning.background`
- `color.ai.surface`
- `color.ai.text`
- `color.focus.ring`

### Component tokens
Examples:
- `button.primary.background.default`
- `button.primary.background.hover`
- `button.primary.background.pressed`
- `button.primary.text`
- `card.background.default`
- `card.border.default`
- `table.header.background`
- `nav.item.background.selected`
- `assistant.message.user.background`
- `assistant.message.ai.background`
- `input.background.default`
- `input.border.default`

### Naming rules
- Use lowercase dot notation.
- Keep token names stable and semantic, not theme-specific.
- Prefer purpose-based names over raw color names.
- Use component names only when the token is specific to a component.
- Never expose arbitrary hex strings directly in component code.

### Token aliases and references
- Semantic tokens may reference primitive tokens; component tokens reference semantic tokens.
- Final tokens should resolve to a single value without unresolved loops.
- Example: `color.action.primary.background` resolves to theme-specific accent values.

---

## 8. State model

Applies to all interactive and informational components.

Default, hover, pressed, focused, selected, disabled, read-only, loading, empty, error, and success states are all designed explicitly.

Rules:
- Disabled and read-only are not interchangeable.
- Loading states show progress and avoid duplicate submission.
- Empty states explain the condition and a recommended next action.
- Error states preserve user input and provide a path to recovery.
- Success states appear only after an action successfully completes.

### Focus treatment
- Visible focus ring with strong contrast against both themes.
- Needs to work with keyboard navigation and high-zoom display.

### Interaction states summary
- Default: base state
- Hover: subtle background or border shift
- Pressed: tighter visual feedback, same state group
- Focused: high-contrast ring with clear keyboard pattern
- Selected: accent border or tinted background
- Disabled: faded, non-interactive, no hover feedback
- Read-only: visible but non-editable input state
- Loading: spinner or progress treatment with preserved data
- Empty: explanatory message and next action
- Error: red or danger treatment plus actionable guidance
- Success: green or positive treatment after completion

---

## 9. Components

### Navigation
#### Application shell
Purpose: hold navigation, header, page content, and global AI access.

Anatomy:
- Sidebar or top nav
- Current workspace context
- Primary page-level header
- Toolbar or action cluster
- Main content area
- Persistent AI panel in large layouts

States:
- default, active, hover, selected, collapsed, mobile drawer

#### Sidebar item and group
Purpose: orient users across modules and business-unit contexts.

Rules:
- Active items must be clear without relying on color alone.
- Groups should be scannable and compact.
- Icons are secondary to labels.

#### Breadcrumb
Purpose: show where the user is within a campaign, portfolio, or workflow.

#### Page header
Purpose: provide title, context, page actions, and status summary.

#### Tabs
Purpose: switch between views within a context.

#### Segmented control
Purpose: choose between board/list or compact modes.

#### Pagination
Purpose: handle long tables while preserving filter context.

### Actions
#### Primary button
Purpose: main action for the current task.

Tokens:
- `color.action.primary.background`
- `color.action.primary.text`
- `color.action.primary.border`

States:
- default, hover, pressed, focus, disabled, loading

#### Secondary button
Purpose: support tasks without primary emphasis.

#### Tertiary button
Purpose: lower-emphasis row actions or text actions.

#### Destructive button
Purpose: irreversible or risky actions.

#### Icon button
Purpose: compact control for one-step actions.

Accessibility:
- always include a label or accessible name

#### Split button
Use only when a single action with a secondary menu is justified, e.g. “Submit” + “Save draft”.

#### Text link
Purpose: inline navigation or low-emphasis task entry.

### Forms
#### Field label
Purpose: clearly define what the field requires and whether it is optional.

Rules:
- Required fields show a clear indicator.
- Optional fields are not mistaken for optional states.

#### Text input, textarea, select, combobox, date input
Purpose: capture structured information.

States:
- default, hover, focus, error, read-only, disabled

#### Checkbox, radio group, switch
Purpose: boolean or single-choice selection.

Rules:
- Use switches only for immediate enable/disable states, not for multi-step or destructive preferences.
- Use radio groups for mutually exclusive values.

#### File upload
Purpose: attach assets, briefs, source files, and creative hand-offs.

#### Helper text and validation message
Purpose: explain requirements and errors.

Rules:
- Helper text is contextual, not alarming.
- Validation messages must clearly explain what needs to change.

#### Unsaved changes notice
Purpose: protect user work during navigation.

Rules:
- Alert before leaving a form with unsaved edits.
- Preserve draft state if the user decides to continue.

### Data display
#### Campaign card
Purpose: present a campaign in a board or list.

Required info:
- Campaign ID and name
- Business unit
- Owner
- Channel
- Deployment date
- Stage
- Health
- Blocker summary
- Next action

Variants:
- default, selected, hovered, blocked, overdue, completed, loading

#### Campaign list row
Purpose: present a compact row in a table or list view.

#### Data table
Purpose: heavy comparison and audit data.

#### Metric summary
Purpose: show numbers that matter quickly: active campaigns, blocked campaigns, due this week, etc.

#### Owner avatar
Purpose: identify ownership quickly.

#### Channel badge
Purpose: indicate marketing channel in a small, compact style.

#### Lifecycle badge
Purpose: show the campaign stage without implying health.

#### Campaign health indicator
Purpose: show whether a campaign is on track, needs attention, blocked, or on hold.

This is separate from lifecycle stage.

#### Blocker summary
Purpose: make blockers visible without burying them in details.

#### Deployment date
Purpose: show the date and highlight risk when near or passed due.

#### Progress indicator
Purpose: reflect completion of an item or handoff.

#### Empty state
Purpose: help users recover from no results or no records.

#### Loading skeleton
Purpose: indicate item loading without ugly flicker.

### Feedback and overlays
#### Inline alert, banner, toast, tooltip, dropdown, popover, detail drawer, confirmation dialog, error recovery panel
These reinforce state transitions, navigation, and recovery.

Rules:
- Dialogs must trap focus and return focus to the trigger.
- Tooltips should not contain critical information required to complete a task.
- Error recovery panels should recommend the next action.

### AI components
#### Assistant identity
Purpose: clearly mark AI-generated output.

#### Suggested prompt
Purpose: help users ask a good question quickly.

#### Prompt composer
Purpose: capture user input and additional context.

#### User message and assistant message
Purpose: distinguish user-generated and AI-generated content.

#### Thinking indicator
Purpose: show processing without false certainty.

#### Context chip
Purpose: indicate which campaign or brief the AI is addressing.

#### Source reference
Purpose: show the record or content that informed an answer.

#### Recommendation card
Purpose: suggest a next action or change.

#### Proposed change preview
Purpose: show what will change before confirmation.

#### Action confirmation
Purpose: require explicit approval for an AI-backed update.

#### Persistent companion panel
Purpose: keep AI assistance available while the user works.

---

## 10. Campaign board patterns

The board shows lifecycle columns with the following data:
- Lifecycle column
- Campaign count
- Campaign title and ID
- Owner
- Channel
- Deployment date
- Health
- Blocker
- Next action

### Campaign board states
- Selected campaign
- Hovered campaign
- Blocked campaign
- Overdue milestone
- Completed campaign

### Board controls
- Search
- Owner filter
- Business unit filter
- Channel filter
- Date range
- Active filters
- Clear filters
- Board/list switch

### Board interactions
- Filters persist while a user navigates between board and table views.
- A selected campaign remains selected across filter updates when it still matches the result set.
- A blocked campaign is clearly indicated through a status label and a blocker summary.
- Overdue milestones can be marked both by date and by a visible warning state.

### Drag-and-drop behavior
If drag-and-drop is included, provide parallel alternatives:
- keyboard reordering
- menu actions for move to stage
- invalid transition explanation
- destination preview before commit
- prerequisites validation before changing stage

---

## 11. Guided Studio patterns

### Creation flow
Brief → Audience → Channels → Review → Submit

This flow maps to the broader campaign lifecycle but is not the same as lifecycle stage.

Important distinction:
- Form-step progress indicates completion of a guided flow.
- Lifecycle stage indicates whether the campaign is in Draft, Submitted, Prioritized, Requirements, or Ready.

### Step requirements
Each step must include:
- Purpose
- Required and optional fields
- Help text
- Saved status
- Validation
- Back and continue actions
- Missing-information summary
- Contextual assistant access

### Guidance behavior
- Users can revisit steps without losing data.
- Draft saving and resuming work are supported.
- Final submission requirements are visible before click.
- A step is not marked complete until required information is valid.

---

## 12. Ask Little Joe: AI interaction system

### Modes
1. AI-first landing
2. Focused answer page
3. Persistent right-side companion

### Companion behavior
- Selecting a campaign updates the current AI context.
- Existing conversation history remains intact.
- Every answer indicates the campaign it refers to.
- AI actions remain attached to the campaign they were generated for.
- Switching campaigns must not silently retarget an earlier action.
- Unfinished drafts stay available when navigating.

### Action flow
Understand → Explain → Propose → Preview → Confirm → Report result

### Example interaction
User asks: “Which campaigns need attention?”

Little Joe should:
- Summarize the number of affected campaigns.
- Identify the blocker and why it matters.
- Show the campaign ID, owner, due date, and stage.
- Link to the relevant record.
- Recommend a concrete next step.
- Offer “Review & resolve.”

### Review state
The review shows:
- Campaign being updated
- Current value
- Proposed value
- Impact of the change
- Explicit confirmation action

After confirmation:
- show the actual save result
- update campaign status displays
- retain explanation in conversation history
- offer the next relevant action

### AI states
- Idle
- Receiving question
- Thinking
- Answering
- Needs clarification
- No matching records
- Missing context
- Uncertain answer
- Service unavailable
- Action proposed
- Awaiting confirmation
- Applying update
- Update successful
- Update failed

### Disclosure and honesty
- Use honest capability labels.
- If a prototype uses scripted responses, label it as demo AI.
- Do not imply live integrations, sending, saving, or execution unless those capabilities are implemented.
- Do not invent confidence percentages or source citations.

---

## 13. Content design

Use concise, specific, and calm language.

Preferred examples:
- “Creative hand-off is pending.”
- “Review the assets before clearing this blocker.”
- “Your draft is saved.”
- “Add a deployment date to continue.”

Avoid:
- generic failure language without recovery guidance
- unexplained internal abbreviations
- repeated greetings
- overenthusiastic celebration
- claiming an action happened when it was only suggested

### Button label conventions
- Use verb + object structure: “Review brief”, “Submit campaign”, “Save draft”
- Use consistent labels across the product.
- Pair with context so users understand what will happen next.

### Error pattern structure
- What is wrong
- Why it matters
- What the user can do next

Example:
- “Audience size is missing.”
- “This campaign cannot be submitted without an audience estimate.”
- “Add an audience size to continue.”

### Empty-state structure
- What is missing
- Why it matters
- Recommended action

### Date and time format
- Use locale-aware formatting.
- Prefer `Mar 12, 2027` or `12 Mar 2027` as readable date style for enterprise dashboards.
- Preserve months and days consistently across the system.

### Pluralization
- Use clear plural and singular rules.
- Example: `1 campaign`, `3 campaigns`; `0 blockers`.

### Truncation rules
- Truncate long names in cards and tables at predictable width.
- Preserve important identifiers like campaign ID, even when the name is truncated.

### Tooltip usage
- Tooltips are for secondary context, not critical instructions.
- Keep them short and direct.

### AI disclosure wording
- “Little Joe can suggest next steps. Review before applying any change.”
- “Demo AI: scripted responses only.”

---

## 14. Accessibility

Target WCAG 2.2 AA.

### Contrast requirements
- Normal text: at least 4.5:1
- Large text and meaningful UI boundaries: at least 3:1
- Focus ring: high visibility against all surfaces

### Additional requirements
- Ensure keyboard completion of primary flows.
- Maintain logical tab order and keyboard focus.
- Support zoom and text resizing without content loss.
- Provide labels and programs for screen readers.
- Associate validation messages with the correct control.
- Manage dialog focus properly.
- Respect reduced-motion preferences.
- Do not rely on color alone to convey status or critical information.
- Do not hide essential information behind hover.

### Streaming AI accessibility
- Avoid announcing every token as it arrives.
- Announce when the response is ready or when an action is proposed.
- Allow users to review earlier messages without forced auto-scroll.

---

## 15. Example campaign data

Sample campaign record used throughout the system:
- Campaign ID: `MPP-20031`
- Campaign name: `Core Inactive`
- Business unit: `CRS`
- Channel: `Email`
- Owner: `Maya Patel`
- Stage: `Channel Requirements`
- Health: `Needs attention`
- Blocker: `Creative hand-off pending`
- Deployment date: `March 12, 2027`

This is sample data and should be treated as illustrative, not as a live record.

---

## 16. Implementation guidance

### Recommended stack
- React
- TypeScript
- CSS custom properties
- Semantic HTML
- Reusable SVG icon library

### CSS variable strategy
Use a root theme attribute and map tokens for each theme:

```css
:root {
  --color-background-canvas: #101719;
  --color-surface-default: #192225;
  --color-text-primary: #E7EEEB;
  --color-action-primary-background: #B6ED82;
  --color-status-warning-foreground: #F6BC85;
  --font-body: "DM Sans", "Segoe UI", sans-serif;
  --font-heading: "Manrope", "Avenir Next", sans-serif;
}

[data-theme="studio-light"] {
  --color-background-canvas: #F8F6F1;
  --color-surface-default: #FFFEFA;
  --color-text-primary: #303B34;
  --color-action-primary-background: #3D6650;
}
```

### TypeScript example
```ts
export type ThemeName = "operations-dark" | "studio-light";

export interface DesignTokenSet {
  color: Record<string, unknown>;
  space: Record<string, string>;
  radius: Record<string, string>;
  motion: Record<string, string>;
}

export interface ButtonProps {
  variant?: "primary" | "secondary" | "tertiary" | "destructive";
  size?: "sm" | "md" | "lg";
  disabled?: boolean;
  loading?: boolean;
  children: React.ReactNode;
}
```

### Accessible component example
```tsx
<Button
  variant="primary"
  aria-label="Submit campaign"
  disabled={isSubmitting}
  loading={isSubmitting}
>
  Submit campaign
</Button>
```

### AI action review pattern
Every AI-generated action must pass through review:
- explain the change
- show current vs proposed value
- require confirmation
- show result only after success

---

## 17. Pattern library overview

### Board pattern
A board gives users a sense of progression and backlog while maintaining visibility of blockers and deadlines.

### Table pattern
A table gives users precise comparison across many campaigns, with filters and sorting at the top.

### Guided form pattern
A guided studio pattern helps authors fill in structured information without losing track of what remains incomplete.

### AI answer pattern
AI answers are not sources of truth; they are interpretive overlays with evidence and recommended actions.

---

## 18. Example screens

### 1. Operations Board in dark theme
Show:
- sidebar navigation
- header with search and filters
- board with columns for lifecycle stages
- campaign cards with owner, channel, date, health, and blocker
- right-side AI panel in a wide workspace

### 2. Guided Studio landing in light theme
Show:
- warm off-white surfaces
- green action buttons
- clear form sections and guidance surfaces
- layout optimized for writing and review

### 3. Guided campaign creation
Show:
- Brief step
- Audience step
- Channels step
- Review step
- Draft save status and validation messages

### 4. Campaign review and submission
Show:
- content sections with readiness metrics
- missing-information summary
- clearly surfaced required fields
- approval actions that are separate from automatic updates

### 5. Campaigns needing attention
Show:
- a filtered view or board that highlights blocked and at-risk campaigns
- explanation of blocker
- recommended next step

### 6. Workspace with right-side Little Joe companion
Show:
- active campaign selected
- AI panel pinned to the right edge
- conversation thread with context chips and source links

---

## 19. Component showcase and implementation checklist

### Checklist before release
- Verify semantic tokens exist for both themes.
- Check interactive states across both themes.
- Validate critical contrast across key surfaces.
- Confirm keyboard completion of primary workflows.
- Verify responsive layouts at small, medium, and large breakpoints.
- Confirm lifecycle stage and health remain separate concepts.
- Verify AI context remains attached to the correct campaign.
- Confirm errors preserve user input.
- Ensure AI actions require explicit review.
- Clearly label scripted demo behavior and unimplemented integrations.

### Do / do not guidance
Do:
- keep status clear and contextual
- use a strong visual hierarchy
- support dense comparison in board and table patterns
- preserve AI context and explicit review

Do not:
- merge lifecycle and health into one status
- rely on color alone for important information
- hide required fields in complex interactions
- imply live AI execution when it is not implemented

---

## 20. Governance

### Naming conventions
- Use lowercase dot notation for tokens.
- Use semantic language for core values.
- Use component names only where necessary.
- Keep naming patterns stable across themes.

### Ownership
- Design system owner: product design + design ops
- Frontend implementation owner: UI engineering
- AI design review: PM + design + engineering

### Contribution checklist
- Document new tokens and their reasons.
- Update both dark and light theme values if a token changes.
- Validate contrast and keyboard access.
- Add usage guidance and do/not examples.
- Document any new dependency or pattern.

### Versioning and deprecation
- Track design-system versions with release notes.
- Deprecate components with a clear migration path.
- Preserve old versions for existing product surfaces when needed.

### Accessibility review
- New components require pattern review and accessibility testing.
- Interaction states must be validated for keyboard and screen-reader behavior.

---

## 21. Summary

The USCC Campaign Studio design system balances operational density with calm guidance. The dark theme supports efficient campaign oversight and rapid triage. The light theme supports guided, thoughtful configuration and review. A single token architecture and shared component logic keep the system coherent across both experiences while allowing each theme to express its own tone.

This is intentionally not a mood board. It is a product system with reusable rules, clear states, accessible interactions, and realistic examples built for actual campaign operations work.