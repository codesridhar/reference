# Campaign Studio — three UX concepts

Open index.html in a browser. Use the top switcher to explore all three concepts:

1. Daily workspace — task-first dashboard with priorities, campaign review, and contextual copilot.
2. Operations board — dark campaign board with search, owner filters, and list view.
3. Guided studio — calm campaign creation and resume experience.

No installation or build step is required. To serve locally: `python3 -m http.server 4173` from this folder, then open http://localhost:4173.

Interactions include creating drafts, editing objectives and channels, resolving creative blockers, advancing campaign stages, filtering campaigns, and scripted assistant responses. Changes persist in localStorage within the browser. AI is simulated; no requests are sent to a model or backend. Google Fonts is optional; local font fallbacks apply offline. All campaign records are sample data.

To reset sample data, clear the browser localStorage key `campaign-prototype`.
