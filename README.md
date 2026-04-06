# shopify-polaris-claude-plugin

A [Claude Code plugin](https://code.claude.com/docs/en/plugins) that teaches Claude Code the complete **Shopify Polaris web component library** — the `<s-*>` custom elements used in [Shopify App Home](https://shopify.dev/docs/api/app-home) UIs.

Once installed, Claude Code will automatically know all 46 components, their props, events, slots, and usage patterns — without you having to paste docs or context into every session.

## What it covers

- **Actions:** `<s-button>`, `<s-link>`, `<s-menu>`, `<s-button-group>`, `<s-clickable>`, `<s-clickable-chip>`
- **Feedback:** `<s-badge>`, `<s-banner>`, `<s-spinner>`
- **Forms:** `<s-text-field>`, `<s-text-area>`, `<s-select>`, `<s-checkbox>`, `<s-switch>`, `<s-number-field>`, `<s-money-field>`, `<s-email-field>`, `<s-url-field>`, `<s-password-field>`, `<s-search-field>`, `<s-date-field>`, `<s-date-picker>`, `<s-color-field>`, `<s-color-picker>`, `<s-drop-zone>`, `<s-choice-list>`
- **Layout:** `<s-page>`, `<s-section>`, `<s-stack>`, `<s-grid>`, `<s-box>`, `<s-divider>`, `<s-table>`, `<s-ordered-list>`, `<s-unordered-list>`, `<s-query-container>`
- **Overlays:** `<s-modal>`, `<s-popover>`
- **Media:** `<s-icon>`, `<s-avatar>`, `<s-image>`, `<s-thumbnail>`
- **Typography:** `<s-text>`, `<s-heading>`, `<s-paragraph>`, `<s-tooltip>`, `<s-chip>`

## Installation

### Option A — Global (all your projects)

```bash
git clone https://github.com/your-github-username/shopify-polaris-claude-plugin.git ~/.claude/plugins/shopify-polaris
```

### Option B — Project-only (committed to your repo)

```bash
# From your project root
git clone https://github.com/your-github-username/shopify-polaris-claude-plugin.git .claude/plugins/shopify-polaris
```

Or as a git submodule (recommended for teams — keeps it version-pinned):

```bash
git submodule add https://github.com/your-github-username/shopify-polaris-claude-plugin.git .claude/plugins/shopify-polaris
git commit -m "Add Shopify Polaris Claude Code plugin"
```

### Enable the plugin

After installing, start Claude Code and run:

```
/plugin enable shopify-polaris
```

Or load it for a single session:

```bash
claude --plugin-dir ~/.claude/plugins/shopify-polaris
# or
claude --plugin-dir .claude/plugins/shopify-polaris
```

### Verify it's working

In Claude Code, run:

```
/shopify-polaris:shopify-polaris
```

Or just start writing Shopify app UI — Claude will activate the skill automatically when it detects `<s-*>` components or Shopify app context.

## Usage

The skill activates **automatically** when Claude detects you're working on Shopify app UI. You can also invoke it explicitly:

```
/shopify-polaris:shopify-polaris
```

### Examples of what Claude will now do correctly

```
You: Add a delete button that opens a confirmation modal
Claude: <writes correct <s-button commandFor="..."> + <s-modal> pattern>

You: Create a product form with title, description, and price fields
Claude: <uses <s-page>, <s-section>, <s-text-field>, <s-text-area>, <s-money-field>>

You: Show a success banner after saving
Claude: <s-banner tone="success" title="Saved">...</s-banner>
```

## Updating

```bash
# If installed globally
cd ~/.claude/plugins/shopify-polaris && git pull

# If installed as a submodule
git submodule update --remote .claude/plugins/shopify-polaris
git commit -m "Update Shopify Polaris plugin"
```

## Plugin structure

```
shopify-polaris-claude-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/
│   └── shopify-polaris/
│       └── SKILL.md         # All component docs + patterns
├── README.md
└── LICENSE
```

This follows the official [Claude Code plugin format](https://code.claude.com/docs/en/plugins).

## Contributing

PRs welcome — especially for:
- New components as Shopify adds them
- More usage patterns and recipes
- Better auto-invocation trigger phrases in the frontmatter description

## License

MIT
