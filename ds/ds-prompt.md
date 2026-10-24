Act as a principal product designer and design systems architect.

Create a complete, implementation-ready design system for USCC Campaign Studio, an enterprise marketing campaign management application with an integrated AI assistant called “Ask Little Joe.”

Develop one shared design system with two coordinated themes:

1. Operations Board — dark theme.
2. Guided Studio — light theme.

Produce a working component library, design tokens, documentation, and realistic example screens. Make the output detailed enough for designers and frontend engineers to build consistent experiences without inventing missing rules.

PRODUCT CONTEXT

Campaign Studio helps marketers and campaign delivery teams manage:
- Campaign intake and sizing.
- Campaign briefs.
- Audience requirements.
- Channel requirements.
- Capacity and prioritization.
- Creative hand-offs.
- Delivery and deployment.
- Campaign status and blockers.

Primary users:
- Marketers creating and reviewing campaigns.
- Campaign managers coordinating work.
- Delivery teams completing requirements and hand-offs.
- Approvers reviewing readiness and submission.

Campaign lifecycle:
Draft → Submitted → Prioritized → Audience Requirements →
Channel Requirements → Execution Ready → Deployed → Completed.

Track campaign health separately from lifecycle stage:
On track, needs attention, blocked, and on hold.

A campaign can be in “Channel Requirements” and also be “Blocked.”
Do not combine these concepts into a single status field.

Sample campaign:
Campaign ID: MPP-20031
Campaign name: Core Inactive
Business unit: CRS
Channel: Email
Owner: Maya Patel
Stage: Channel Requirements
Health: Needs attention
Blocker: Creative hand-off pending
Deployment date: March 12, 2027

Treat all example records as sample data.

DESIGN SYSTEM PRINCIPLES

Define practical principles with examples:
1. Make the next action clear.
2. Preserve context while users work.
3. Explain issues before proposing actions.
4. Make dense information easy to compare.
5. Keep AI suggestions distinguishable from saved data.
6. Use consistent patterns across themes.
7. Build accessibility into every component.

Explain how each principle affects layout, components, content,
and interactions.

SHARED SYSTEM ARCHITECTURE

Use three token layers:

A. Primitive tokens
Raw color palettes, spacing values, font sizes, radii, and durations.

B. Semantic tokens
Purpose-based decisions such as surface, text, border,
action, status, focus, and selection.

C. Component tokens
Specific mappings for buttons, campaign cards, tables,
navigation, assistant messages, and form controls.

Components must reference semantic or component tokens.
Do not hardcode theme-specific colors inside components.

Use consistent token names across both themes.

Example:
Primitive:
color.palette.forest.700

Semantic:
color.action.primary.background

Component:
button.primary.background.default

Document aliases, token types, naming conventions, and units.

THEME A: OPERATIONS BOARD — DARK

Design character:
Focused, precise, composed, and dependable.

Use deep charcoal backgrounds with subtle green undertones,
warm white text, restrained lime accents, and clear surface separation.

Starting palette:
Canvas: #101719
Navigation: #131C1F
Default surface: #192225
Raised surface: #202C2F
Hover surface: #253337
Selected surface: #25392E

Subtle border: #2B383A
Strong border: #4A5D5A

Primary text: #E7EEEB
Secondary text: #B2C0BB
Muted text: #8FA49D
Inverse text: #17271C

Primary accent: #B6ED82
Accent hover: #C8F49E
Accent pressed: #9FD66B
Accent subtle: #25392E

Success:
Foreground #A8DDB7
Background #20372B

Warning:
Foreground #F6BC85
Background #4A3225

Danger:
Foreground #F3A5AC
Background #45282E

Information:
Foreground #A7C8F3
Background #25364B

Validate these combinations before finalizing them.
Adjust values where needed for accessible contrast.

Avoid:
Pure black backgrounds.
Neon accents.
Decorative glows.
Heavy gradients.
Excessive shadows.
Overly colorful workflow stages.

Use borders and surface contrast to establish hierarchy.

THEME B: GUIDED STUDIO — LIGHT

Design character:
Calm, welcoming, thoughtful, and capable.

Use warm off-white surfaces, forest-green actions,
soft sage guidance surfaces, and generous whitespace.

Starting palette:
Canvas: #F8F6F1
Navigation: #F1EFE7
Default surface: #FFFEFA
Raised surface: #FFFFFF
Hover surface: #F3F3EB
Selected surface: #E8EEE2

Subtle border: #E3E2D8
Strong border: #B5BCAF

Primary text: #303B34
Secondary text: #626D60
Muted text: #727A6B
Inverse text: #FFFFFF

Primary accent: #3D6650
Accent hover: #315540
Accent pressed: #274735
Accent subtle: #E8EEE2

Success:
Foreground #286346
Background #E7F1E8

Warning:
Foreground #8C5C18
Background #FFF3DB

Danger:
Foreground #A5353F
Background #FBECEF

Information:
Foreground #355D78
Background #EAF1F6

Guidance surface: #ECEEDE
Guidance text: #536247

Validate these combinations before finalizing them.

Avoid:
Stark white dashboards.
Excessive floating cards.
Pastel decoration without meaning.
Purple gradients.
Oversized AI symbols.
Unnecessary animation.

SHARED FOUNDATIONS

Typography:
Use Manrope for headings and DM Sans for body text and controls.
Provide appropriate fallback font stacks.

Create named typography roles:
Display: 40/48px, weight 700.
Page title: 32/40px, weight 700.
Section title: 22/30px, weight 700.
Panel title: 18/26px, weight 600.
Card title: 14/21px, weight 600.
Body: 14/22px, weight 400.
Comfortable body: 15/24px, weight 400.
Compact body: 12/18px, weight 400.
Control label: 13/18px, weight 600.
Metadata: 11/17px, weight 400.
Eyebrow: 10/15px, weight 700, letter spacing 1.2px.

Define responsive heading sizes.
Use tabular numerals for counts and comparable numeric data.
Keep essential information readable in compact layouts.

Spacing:
Use a 4px base unit.
Scale: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64.

Explain which values apply to:
Inline gaps.
Control padding.
Card padding.
Form spacing.
Section spacing.
Page gutters.

Shape:
Control radius: 8px.
Card and panel radius: 12px.
Composer radius: 16px.
Modal radius: 16px.
Badge radius: 4–6px.
Pill radius: for chips and filters.
Viewport-attached drawers: square outer edges.

Borders:
Define subtle, default, strong, selected, error, and focus treatments.
Use 1px borders for most component boundaries.

Elevation:
Define a small elevation scale for:
Base surfaces.
Dropdowns and popovers.
Drawers.
Dialogs.
Notifications.

Use theme-specific shadows where necessary.

Iconography:
Use one consistent SVG icon family.
Default sizes: 16, 20, and 24px.
Define stroke weight and alignment.
Pair icons with labels when meaning is unfamiliar.
Give icon-only controls accessible names.

Motion:
Fast: 120–160ms.
Standard: 180–240ms.
Define easing tokens.
Use motion to communicate state and spatial relationships.
Respect prefers-reduced-motion.
Avoid continuous decorative animation.

Density:
Provide comfortable and compact variants.
Density may change padding and row height.
Do not reduce essential type size or target accessibility.

LAYOUT SYSTEM

Define:
Desktop sidebar: 200–220px.
Header: 64–72px.
Content gutters: 24–40px.
Focused form width: 640–760px.
General content maximum: 1280–1440px.
AI companion width: 360–420px.
Board columns: 260–320px.
Column gaps: 16–20px.

Provide explicit breakpoint rules and explain behavior at each breakpoint.

Support these layouts:
1. Dashboard with summaries and priorities.
2. Board with horizontally scrollable columns.
3. Campaign table with filters.
4. Guided campaign form.
5. Workspace with persistent right-side AI companion.
6. AI answer page with campaign evidence and actions.

On small screens:
Collapse navigation.
Preserve access to filters.
Keep critical actions visible.
Move the assistant into a dedicated tab or expandable panel.
Preserve draft and conversation state when switching views.
Avoid page-level horizontal overflow.
Allow intentional scrolling inside boards and wide tables.

COMPONENT LIBRARY

For every component, document:
Purpose.
Anatomy.
Variants.
Sizes.
States.
Token mappings.
Content rules.
Accessibility.
Keyboard interaction.
Responsive behavior.
Usage examples.
When not to use it.

Create these components:

Navigation:
- Application shell.
- Sidebar item and group.
- Breadcrumb.
- Page header.
- Tabs.
- Segmented control.
- Pagination.

Actions:
- Primary button.
- Secondary button.
- Tertiary button.
- Destructive button.
- Icon button.
- Split button where justified.
- Text link.

Forms:
- Text input.
- Textarea.
- Select.
- Searchable combobox.
- Date input.
- Checkbox.
- Radio group.
- Switch.
- File upload.
- Field label.
- Helper text.
- Validation message.
- Form section.
- Unsaved changes notice.

Data display:
- Campaign card.
- Campaign list row.
- Data table.
- Metric summary.
- Owner avatar.
- Channel badge.
- Lifecycle badge.
- Campaign health indicator.
- Blocker summary.
- Deployment date.
- Progress indicator.
- Empty state.
- Loading skeleton.

Feedback and overlays:
- Inline alert.
- Banner.
- Toast.
- Tooltip.
- Dropdown menu.
- Popover.
- Campaign detail drawer.
- Confirmation dialog.
- Error recovery panel.

AI:
- Assistant identity.
- Suggested prompt.
- Prompt composer.
- User message.
- Assistant message.
- Thinking indicator.
- Context chip.
- Source reference.
- Recommendation card.
- Proposed change preview.
- Action confirmation.
- Persistent companion panel.

STATE REQUIREMENTS

Define applicable states:
Default.
Hover.
Pressed.
Focused.
Selected.
Disabled.
Read-only.
Loading.
Empty.
Error.
Success.

Do not assume disabled and read-only are interchangeable.

For asynchronous actions:
Show progress.
Prevent accidental duplicate submission.
Preserve user input on failure.
Provide an actionable recovery path.
Only show success after the operation succeeds.

CAMPAIGN BOARD PATTERNS

The board must show:
Lifecycle column.
Campaign count.
Campaign title and ID.
Owner.
Channel.
Deployment date.
Health.
Blocker.
Next action.

Differentiate:
Selected campaign.
Hovered campaign.
Blocked campaign.
Overdue milestone.
Completed campaign.

Provide:
Search.
Owner filter.
Business-unit filter.
Channel filter.
Date range.
Active filters.
Clear filters.
Board/list switch.

If drag-and-drop is included:
Provide keyboard and menu alternatives.
Explain invalid transitions.
Show the destination before committing.
Validate prerequisites before changing stage.

GUIDED STUDIO PATTERNS

Creation flow:
Brief → Audience → Channels → Review → Submit.

Map this creation flow to the broader campaign lifecycle.
Explain that form-step progress and campaign lifecycle are different concepts.

Each step must include:
Purpose.
Required and optional fields.
Help text.
Saved status.
Validation.
Back and continue actions.
Missing-information summary.
Contextual assistant access.

Allow users to revisit steps without losing data.
Support draft saving and resuming.
Make final submission requirements clear.
Do not mark a step complete until required information is valid.

ASK LITTLE JOE: AI INTERACTION SYSTEM

Little Joe should work in three presentation modes:

1. AI-first landing
A prominent composer with useful starting prompts.

2. Focused answer page
A direct answer, supporting campaign information,
source references, recommended next action,
and a follow-up composer.

3. Persistent right-side companion
Chat remains available while users work in campaigns.

Companion behavior:
Selecting a campaign updates the current context.
Existing conversation history remains intact.
Each answer indicates which campaign it refers to.
Actions remain attached to the campaign they were generated for.
Switching campaigns must not silently retarget an earlier action.
Preserve unfinished messages when users navigate.

AI action flow:
Understand → Explain → Propose → Preview → Confirm → Report result.

Example:
User asks: “Which campaigns need attention?”

Little Joe:
- Summarizes the number of affected campaigns.
- Identifies the specific blocker.
- Explains why it matters.
- Shows campaign ID, owner, due date, and stage.
- Links to the source record.
- Recommends a concrete next step.
- Offers “Review & resolve.”

The review shows:
Campaign being updated.
Current value.
Proposed value.
Impact of the change.
Explicit confirmation action.

After confirmation:
Show the actual save result.
Update related campaign status displays.
Retain the explanation in the conversation.
Offer the next relevant action.

Distinguish:
AI-generated suggestions.
User-entered text.
Saved campaign records.
Missing or unavailable information.

Define AI states:
Idle.
Receiving a question.
Thinking.
Answering.
Needs clarification.
No matching records.
Missing context.
Uncertain answer.
Service unavailable.
Action proposed.
Awaiting confirmation.
Applying update.
Update successful.
Update failed.

Use honest capability labels.
If the prototype uses scripted responses, label it as demo AI.
Do not imply live integrations, sending, saving, or execution
unless those capabilities are implemented.
Do not invent confidence percentages or source citations.

CONTENT DESIGN

Use concise, specific, calm language.

Preferred:
“Creative hand-off is pending.”
“Review the assets before clearing this blocker.”
“Your draft is saved.”
“Add a deployment date to continue.”

Avoid:
“Something went wrong” without recovery guidance.
Unexplained internal abbreviations.
Repeated greetings.
Overenthusiastic celebration.
Claims that an action has happened when it was only suggested.

Define:
Button-label conventions.
Error-message structure.
Empty-state structure.
Date and time formatting.
Pluralization.
Truncation rules.
Tooltip usage.
AI disclosure language.

ACCESSIBILITY

Target WCAG 2.2 AA.

Validate:
Text contrast.
Non-text contrast.
Focus visibility.
Keyboard operation.
Target sizes.
Zoom and text resizing.
Screen-reader labels.
Error association.
Dialog focus management.
Reduced motion.
Status announcements.

Use:
At least 4.5:1 contrast for normal text.
At least 3:1 for large text and meaningful UI boundaries.
At least 24px targets, preferably 40–44px for frequent controls.

Do not rely on color alone.
Do not hide essential information behind hover.
Do not communicate AI response progress through animation alone.

For streaming AI responses:
Avoid announcing every token.
Announce meaningful response completion or actionable status changes.
Allow users to read earlier messages without forced scrolling.

TECHNICAL OUTPUT

If a stack is not specified, use:
React.
TypeScript.
CSS custom properties.
Semantic HTML.
A reusable SVG icon library.

Keep component structure independent from theme values.

Implement theme switching using a root theme attribute:
data-theme="operations-dark"
data-theme="studio-light"

Provide representative code:

1. Primitive token definitions.
2. Semantic mappings for both themes.
3. Component token mappings.
4. TypeScript component interfaces.
5. Accessible component examples.
6. Responsive layout examples.

Export machine-readable JSON using a consistent token format.
Include token types and references.
Do not leave unresolved aliases.

DOCUMENTATION AND DELIVERABLES

Produce the following:

1. Design system overview
Purpose, users, principles, and scope.

2. Token reference
Primitive, semantic, and component layers.

3. Theme comparison
Explain what changes between themes and what remains shared.

4. Component catalog
Full anatomy, variants, states, behavior, and accessibility.

5. Pattern library
Boards, forms, tables, AI answers, and companion workflows.

6. Working component showcase
Show both themes and all important states.

7. Example screens
Operations Board in dark theme.
Guided Studio landing in light theme.
Guided campaign creation.
Campaign review and submission.
Campaigns needing attention.
Workspace with right-side Little Joe companion.

8. Implementation files
Tokens, styles, components, and sample data.

9. Usage guidance
Do/don’t examples and composition rules.

10. Governance
Naming conventions.
Component ownership.
Contribution checklist.
Versioning.
Deprecation.
Accessibility review.
Release documentation.

QUALITY CHECKS

Before finishing:
- Verify semantic tokens exist for both themes.
- Check interactive states in both themes.
- Validate critical text and control contrast.
- Confirm keyboard completion of primary workflows.
- Verify responsive layouts.
- Check that campaign lifecycle and health remain separate.
- Verify conversation context stays attached to the correct campaign.
- Confirm errors preserve user input.
- Ensure AI actions require an explicit review step.
- Clearly label demo behavior and unimplemented integrations.

Do not stop at a mood board or color palette.
Deliver a coherent design system with reusable rules,
usable components, and realistic application examples.

Start by stating your assumptions and system architecture.
Then produce foundations, tokens, components, patterns,
example screens, and implementation guidance in that order.