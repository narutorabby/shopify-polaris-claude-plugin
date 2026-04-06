# shopify-polaris-claude-plugin

A Claude Code skill that teaches Claude Code the complete **Shopify Polaris web component library** — the `<s-*>` custom elements used in [Shopify App Home](https://shopify.dev/docs/api/app-home) UIs.

Once installed, Claude Code will automatically know all 46 components, their props, events, slots, and usage patterns — without you having to paste docs or context into every session.

## What it covers

- **Actions:** `<s-button>`, `<s-link>`, `<s-menu>`, `<s-button-group>`, `<s-clickable>`, `<s-clickable-chip>`
- **Feedback:** `<s-badge>`, `<s-banner>`, `<s-spinner>`
- **Forms:** `<s-text-field>`, `<s-text-area>`, `<s-select>`, `<s-checkbox>`, `<s-switch>`, `<s-number-field>`, `<s-money-field>`, `<s-email-field>`, `<s-url-field>`, `<s-password-field>`, `<s-search-field>`, `<s-date-field>`, `<s-date-picker>`, `<s-color-field>`, `<s-color-picker>`, `<s-drop-zone>`, `<s-choice-list>`
- **Layout:** `<s-page>`, `<s-section>`, `<s-stack>`, `<s-grid>`, `<s-box>`, `<s-divider>`, `<s-table>`, `<s-ordered-list>`, `<s-unordered-list>`, `<s-query-container>`
- **Overlays:** `<s-modal>`, `<s-popover>`
- **Media:** `<s-icon>`, `<s-avatar>`, `<s-image>`, `<s-thumbnail>`
- **Typography:** `<s-text>`, `<s-heading>`, `<s-paragraph>`, `<s-tooltip>`, `<s-chip>`

---

## Installation

### Option A — Global (works across all your projects)

```bash
git clone https://github.com/narutorabby/shopify-polaris-claude-plugin.git ~/.claude/skills/shopify-polaris
```

That's it. No extra steps. Claude Code automatically picks up any skill placed in `~/.claude/skills/`.

### Option B — Project-only (commit it to your repo)

```bash
# From your Shopify project root:
git clone https://github.com/narutorabby/shopify-polaris-claude-plugin.git .claude/skills/shopify-polaris
```

Or as a git submodule (recommended for teams — keeps it version-pinned):

```bash
git submodule add https://github.com/narutorabby/shopify-polaris-claude-plugin.git .claude/skills/shopify-polaris
git commit -m "Add Shopify Polaris Claude Code skill"
```

---

## Usage

The skill activates **automatically** when Claude detects you're working on Shopify app UI — no commands needed. You can also invoke it explicitly with a slash command:

```
/shopify-polaris
```

### Examples of what Claude will now do correctly

```
You: Add a delete button that opens a confirmation modal
Claude: → uses <s-button commandFor="..."> + <s-modal> correctly

You: Create a product form with title, description, and price
Claude: → uses <s-page>, <s-section>, <s-text-field>, <s-text-area>, <s-money-field>

You: Show a success banner after saving
Claude: → <s-banner tone="success" title="Saved">...</s-banner>
```

---

## Updating

```bash
# If installed globally
cd ~/.claude/skills/shopify-polaris && git pull

# If installed as a submodule
git submodule update --remote .claude/skills/shopify-polaris
git commit -m "Update Shopify Polaris skill"
```

---

## Repository structure

```
shopify-polaris-claude-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── shopify-polaris/
│       └── SKILL.md       ← all 46 components, props, patterns
├── README.md
└── LICENSE
```

---

## Contributing

PRs welcome — especially for:
- New components as Shopify adds them
- More usage patterns and recipes

## License

MIT
