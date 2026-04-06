---
name: shopify-polaris
description: >
  Shopify Polaris web components reference for Shopify App Home. Use automatically
  when writing HTML or Remix code for a Shopify app, or when the user mentions
  <s-button>, <s-modal>, <s-text-field>, Polaris, or any s-* component.
  Covers all 46 components: props, events, slots, and usage patterns.
---

# Shopify Polaris Web Components

This skill gives you complete knowledge of the **Shopify Polaris web component library** — the `<s-*>` custom elements used in Shopify App Home UIs.

**Base docs:** `https://shopify.dev/docs/api/app-home/web-components`
**CDN script:** `<script src="https://cdn.shopify.com/shopifycloud/polaris.js"></script>`

---

## Core Rules

1. **Always use the `s-` prefix** — `<s-button>`, `<s-text-field>`, `<s-modal>`, etc.
2. **`commandFor` + `command`** wires buttons to modals/popovers declaratively — no JS needed.
3. **`<s-stack direction="inline">`** = horizontal flex. **`direction="block"`** = vertical.
4. **`<s-page>` wraps all app views** — provides title, back action, primary action chrome.
5. **`<s-section>` groups form inputs** — card-like container with optional title.
6. **`tone="critical"`** for destructive actions; `tone="success"` for confirmations.
7. **Icon-only buttons MUST have `accessibilityLabel`.**
8. **Props are camelCase in JSX**, kebab-case in raw HTML attributes.

---

## Setup

```html
<head>
  <meta name="shopify-api-key" content="%SHOPIFY_API_KEY%" />
  <script src="https://cdn.shopify.com/shopifycloud/polaris.js"></script>
</head>
```

Remix (`app/root.tsx`):
```tsx
<script src="https://cdn.shopify.com/shopifycloud/polaris.js" />
```

---

## Component Reference

### ACTIONS

#### `<s-button>`
Triggers actions, form submissions, navigation.

| Prop | Type | Default | Notes |
|---|---|---|---|
| `variant` | `"auto"` \| `"primary"` \| `"secondary"` \| `"tertiary"` | `"auto"` | Visual hierarchy |
| `tone` | `"auto"` \| `"critical"` \| `"neutral"` | `"auto"` | Semantic color |
| `icon` | string (icon name) | — | e.g. `"plus"`, `"delete"`, `"save"` |
| `disabled` | boolean | `false` | |
| `loading` | boolean | `false` | Shows spinner, prevents clicks |
| `type` | `"button"` \| `"submit"` \| `"reset"` | `"button"` | |
| `href` | string | — | Makes button navigate like a link |
| `target` | `"auto"` \| `"_blank"` \| `"_self"` \| `"_parent"` \| `"_top"` | `"auto"` | |
| `download` | string | — | Triggers file download |
| `accessibilityLabel` | string | — | **Required for icon-only buttons** |
| `commandFor` | string | — | ID of component to control |
| `command` | `"--auto"` \| `"--show"` \| `"--hide"` \| `"--toggle"` | `"--auto"` | |
| `interestFor` | string | — | ID of popover/tooltip to show on hover |

Events: `click`, `focus`, `blur` | Slot: `children`

```html
<s-button variant="primary">Add Product</s-button>
<s-button variant="primary" tone="critical">Delete</s-button>
<s-button icon="plus">Add product</s-button>
<s-button loading variant="primary">Saving...</s-button>
<s-button type="submit" variant="primary">Save</s-button>
<s-button commandFor="my-modal" command="--show">Open modal</s-button>
<s-button icon="duplicate" variant="tertiary" accessibilityLabel="Duplicate"></s-button>
```

#### `<s-clickable>`
Wraps arbitrary content to make it interactive. Use when `<s-button>` or `<s-link>` aren't enough.
Props: `href`, `target`, `disabled`, `accessibilityLabel`, `accessibilityRole`
Events: `click`, `focus`, `blur`

#### `<s-link>`
Interactive text for navigation within content/paragraphs.
Props: `href`, `target`, `download`, `tone` (`"auto"` \| `"critical"` \| `"neutral"`), `monochrome`
Events: `click`, `focus`, `blur`
```html
<s-link href="/products">View products</s-link>
<s-link href="https://help.shopify.com" target="_blank">Help docs</s-link>
```

#### `<s-menu>`
Dropdown action list for a resource.
Props: `label`, `icon` | Events: `click` | Slot: `children` (buttons/links)
```html
<s-menu label="More actions">
  <s-button variant="tertiary">Edit</s-button>
  <s-button variant="tertiary" tone="critical">Delete</s-button>
</s-menu>
```

#### `<s-button-group>`
Groups related buttons in a structured layout.
Props: `variant` (`"segmented"` \| `"default"`) | Slot: `children`
```html
<s-button-group>
  <s-button>Save</s-button>
  <s-button variant="secondary">Cancel</s-button>
</s-button-group>
```

#### `<s-clickable-chip>`
Interactive labels/tags users can click or remove.
Props: `disabled`, `removable` | Events: `click`, `remove`
```html
<s-clickable-chip>Electronics</s-clickable-chip>
<s-clickable-chip removable>Sale items</s-clickable-chip>
```

---

### FEEDBACK AND STATUS

#### `<s-badge>`
Status/count indicator on a resource.

| Prop | Values |
|---|---|
| `tone` | `"info"` \| `"success"` \| `"warning"` \| `"critical"` \| `"new"` \| `"attention"` \| `"read-only"` \| `"enabled"` \| `"disabled"` |
| `progress` | `"complete"` \| `"incomplete"` \| `"partially-complete"` |
| `size` | `"small"` \| `"medium"` (default) |

```html
<s-badge tone="success">Active</s-badge>
<s-badge tone="critical">Error</s-badge>
<s-badge tone="warning" progress="incomplete">Draft</s-badge>
```

#### `<s-banner>`
Prominent message strip for important info or required actions.
Props: `tone` (`"info"` \| `"success"` \| `"warning"` \| `"critical"`), `title`, `dismissible`
Events: `dismiss` | Slots: `children`, `action`
```html
<s-banner tone="success" title="Saved">Your changes have been saved.</s-banner>
<s-banner tone="critical" title="Error" dismissible>Something went wrong.</s-banner>
```

#### `<s-spinner>`
Animated loading indicator.
Props: `size` (`"small"` \| `"large"`), `accessibilityLabel` (default: `"Loading"`)
```html
<s-spinner size="small"></s-spinner>
```

---

### FORMS

#### `<s-text-field>` ⭐ Most-used form element
Single-line text input.

| Prop | Type | Notes |
|---|---|---|
| `label` | string | Required |
| `value` | string | |
| `type` | `"text"` \| `"email"` \| `"number"` \| `"password"` \| `"search"` \| `"tel"` \| `"url"` | |
| `placeholder` | string | |
| `disabled` | boolean | |
| `readOnly` | boolean | |
| `error` | string | Inline error message |
| `helpText` | string | Helper text below field |
| `prefix` | string | Content before input (e.g. `"$"`) |
| `suffix` | string | Content after input (e.g. `"USD"`) |
| `clearButton` | boolean | |
| `maxLength` | number | |
| `name` | string | |

Events: `change`, `input`, `focus`, `blur`, `clear`
```html
<s-text-field label="Product title" name="title"></s-text-field>
<s-text-field label="Price" prefix="$" type="number" name="price"></s-text-field>
<s-text-field label="Email" type="email" error="Enter a valid email"></s-text-field>
```

#### `<s-text-area>`
Multi-line text input.
Props: same as `<s-text-field>` + `rows`, `autoSize`, `maxLength`
Events: `change`, `input`, `focus`, `blur`

#### `<s-select>`
Dropdown single-option picker.
Props: `label`, `options` (JSON array of `{label, value, disabled?}`), `value`, `disabled`, `error`, `helpText`, `placeholder`
Events: `change`
```html
<s-select
  label="Country"
  options='[{"label":"Canada","value":"CA"},{"label":"United States","value":"US"}]'
  value="CA"
></s-select>
```

#### `<s-checkbox>`
Props: `label` (required), `checked`, `indeterminate`, `disabled`, `error`, `helpText`, `name`, `value`
Events: `change`
```html
<s-checkbox label="Accept terms" name="terms"></s-checkbox>
<s-checkbox label="Subscribe" checked error="Required"></s-checkbox>
```

#### `<s-switch>`
Toggle on/off control.
Props: `label` (required), `checked`, `disabled`, `helpText`
Events: `change`
```html
<s-switch label="Enable notifications" checked></s-switch>
```

#### `<s-choice-list>`
Radio/checkbox group for single or multiple selection.
Props: `title`, `choices` (JSON array of `{label, value, helpText?}`), `selected` (JSON array), `allowMultiple`
Events: `change`

#### `<s-number-field>`
Props: `label`, `value`, `min`, `max`, `step`, `disabled`, `error`, `helpText`
Events: `change`, `input`

#### `<s-money-field>`
Monetary input with currency formatting.
Props: `label`, `value`, `currency` (e.g. `"USD"`), `disabled`, `error`, `min`, `max`
Events: `change`, `input`

#### `<s-email-field>`
Props: `label`, `value`, `placeholder`, `disabled`, `error`, `helpText`, `autoComplete`
Events: `change`, `input`, `focus`, `blur`

#### `<s-url-field>`
Props: `label`, `value`, `placeholder`, `disabled`, `error`, `helpText`
Events: `change`, `input`, `focus`, `blur`

#### `<s-password-field>`
Masked input with visibility toggle.
Props: `label`, `value`, `disabled`, `error`, `autoComplete`
Events: `change`, `input`, `focus`, `blur`

#### `<s-search-field>`
Props: `label`, `value`, `placeholder`, `disabled`, `clearButton`
Events: `change`, `input`, `clear`, `focus`, `blur`
```html
<s-search-field label="Search products" placeholder="Search..."></s-search-field>
```

#### `<s-date-field>`
Props: `label`, `value` (ISO date string), `disabled`, `error`, `min`, `max`
Events: `change`

#### `<s-date-picker>`
Calendar-based date selector.
Props: `month` (0–11), `year`, `selected` (string or `{start, end}`), `allowRange`, `disableDatesBefore`, `disableDatesAfter`, `disableSpecificDates`
Events: `change`, `monthChange`

#### `<s-color-field>`
Color selector via picker or hex text input.
Props: `label`, `value` (hex), `disabled`, `error`
Events: `change`, `input`

#### `<s-color-picker>`
Visual color palette.
Props: `color` (`{hue, saturation, brightness, alpha?}`), `allowAlpha`
Events: `change`

#### `<s-drop-zone>`
Drag-and-drop file upload.
Props: `accept`, `allowMultiple`, `disabled`, `label`, `type` (`"file"` \| `"image"`), `outline`, `overlay`
Events: `drop`, `dropAccepted`, `dropRejected`, `dragOver`, `dragEnter`, `dragLeave`, `fileDialogClose`

---

### LAYOUT AND STRUCTURE

#### `<s-stack>` ⭐ Most-used layout primitive
Flexbox container for horizontal/vertical layouts.

| Prop | Values | Default |
|---|---|---|
| `direction` | `"inline"` (horizontal) \| `"block"` (vertical) | `"block"` |
| `gap` | `"none"` \| `"extra-tight"` \| `"tight"` \| `"base"` \| `"loose"` \| `"extra-loose"` | — |
| `wrap` | boolean | — |
| `align` | `"start"` \| `"center"` \| `"end"` \| `"space-between"` \| `"space-around"` \| `"space-evenly"` | — |
| `blockAlign` | `"start"` \| `"center"` \| `"end"` \| `"baseline"` \| `"stretch"` | — |

```html
<!-- Horizontal row of buttons -->
<s-stack direction="inline" gap="base">
  <s-button>Cancel</s-button>
  <s-button variant="primary">Save</s-button>
</s-stack>

<!-- Vertical form fields -->
<s-stack direction="block" gap="loose">
  <s-text-field label="First name"></s-text-field>
  <s-text-field label="Last name"></s-text-field>
</s-stack>
```

#### `<s-page>`
Root wrapper for all app views. Provides title bar, back action, and primary action chrome.
Props: `title`, `subtitle`, `backAction` (`{content, url}`), `primaryAction`, `secondaryActions`, `pagination`
Slots: `children`, `primaryAction`, `secondaryActions`
```html
<s-page title="Products">
  <!-- page content here -->
</s-page>
```

#### `<s-section>`
Card-like container grouping related content.
Props: `title`, `variant` (`"default"` \| `"slim"`)
Slots: `children`, `actions`
```html
<s-section title="Product details">
  <s-text-field label="Title" name="title"></s-text-field>
</s-section>
```

#### `<s-box>`
Low-level flexible container for custom layouts.
Props: `background`, `borderColor`, `borderRadius`, `borderWidth`, `color`, `minHeight`, `maxWidth`, `padding`, `paddingBlock`, `paddingInline`, `shadow`, `overflowX`, `overflowY`, `as`

#### `<s-grid>`
CSS grid layout for responsive multi-column designs.
Props: `columns`, `gap`, `areas`
```html
<s-grid columns="3" gap="base">
  <s-box>Item 1</s-box>
  <s-box>Item 2</s-box>
  <s-box>Item 3</s-box>
</s-grid>
```

#### `<s-divider>`
Visual separator.
Props: `borderColor`, `borderWidth` (`"1"` through `"5"`)
```html
<s-divider></s-divider>
```

#### `<s-table>`
Data table with rows and columns.
Props: `headings` (JSON array), `rows` (JSON array)

#### `<s-ordered-list>` / `<s-unordered-list>`
Numbered and bulleted lists. Slot: `children` (`<li>` elements)

#### `<s-query-container>`
CSS container query context for responsive child components.
Props: `as`

---

### OVERLAYS

#### `<s-modal>`
Focused overlay that blocks page interaction until dismissed.

| Prop | Type | Notes |
|---|---|---|
| `id` | string | **Required** — referenced by `commandFor` |
| `open` | boolean | |
| `title` | string | **Required** |
| `size` | `"small"` \| `"base"` \| `"large"` \| `"fullScreen"` | |

Events: `show`, `hide` | Slots: `children` (body), `footer`

```html
<!-- Trigger -->
<s-button commandFor="delete-modal" command="--show" tone="critical">Delete</s-button>

<!-- Modal -->
<s-modal id="delete-modal" title="Delete product?">
  <s-paragraph>This action can't be reversed.</s-paragraph>
  <div slot="footer">
    <s-stack direction="inline" gap="tight">
      <s-button commandFor="delete-modal" command="--hide">Cancel</s-button>
      <s-button variant="primary" tone="critical">Delete</s-button>
    </s-stack>
  </div>
</s-modal>
```

#### `<s-popover>`
Non-blocking overlay anchored to a trigger element.
Props: `id` (required), `open`
Events: `show`, `hide` | Slot: `children`
```html
<s-button commandFor="actions-popover">More actions</s-button>
<s-popover id="actions-popover">
  <s-stack direction="block">
    <s-button variant="tertiary">Export</s-button>
    <s-button variant="tertiary">Import</s-button>
  </s-stack>
</s-popover>
```

---

### MEDIA AND VISUALS

#### `<s-icon>`
Renders a Polaris icon by name.
Props: `source` (icon name, required), `tone` (`"base"` \| `"subdued"` \| `"info"` \| `"success"` \| `"warning"` \| `"critical"` \| `"emphasis"` \| `"magic"`), `accessibilityLabel`
```html
<s-icon source="settings"></s-icon>
<s-icon source="check-circle" tone="success"></s-icon>
```

#### `<s-avatar>`
Profile image or initials display.
Props: `name`, `source` (image URL), `size` (`"extra-small"` \| `"small"` \| `"medium"` \| `"large"` \| `"xl"` \| `"2xl"`), `shape` (`"round"` \| `"square"`)
```html
<s-avatar name="John Doe" size="medium"></s-avatar>
```

#### `<s-image>`
Responsive image.
Props: `source` (URL, required), `alt`, `width`, `height`, `crossOrigin`

#### `<s-thumbnail>`
Small preview image for products.
Props: `source`, `alt`, `size` (`"small"` \| `"medium"` \| `"large"`)
```html
<s-thumbnail source="/product.jpg" alt="Product" size="small"></s-thumbnail>
```

---

### TYPOGRAPHY AND CONTENT

#### `<s-text>` ⭐
Inline text with visual style control.

| Prop | Values |
|---|---|
| `as` | HTML tag (default: `"span"`) |
| `variant` | `"bodyLg"` \| `"bodyMd"` \| `"bodySm"` \| `"headingXl"` \| `"headingLg"` \| `"headingMd"` \| `"headingSm"` \| `"headingXs"` |
| `tone` | `"base"` \| `"subdued"` \| `"success"` \| `"critical"` \| `"caution"` \| `"magic"` \| `"text-inverse"` |
| `fontWeight` | `"regular"` \| `"medium"` \| `"semibold"` \| `"bold"` |
| `truncate` | boolean |
| `alignment` | `"start"` \| `"center"` \| `"end"` \| `"justify"` |
| `textDecorationLine` | `"line-through"` \| `"none"` |

```html
<s-text variant="headingMd">Product title</s-text>
<s-text tone="subdued" variant="bodySm">SKU: 12345</s-text>
<s-text fontWeight="semibold">$29.99</s-text>
<s-text tone="critical">Out of stock</s-text>
```

#### `<s-heading>`
Hierarchical page/section titles.
Props: `as` (`"h1"`–`"h6"`, `"p"`, `"legend"`, `"dt"`), `variant` (`"headingXl"` \| `"headingLg"` \| `"headingMd"` \| `"headingSm"` \| `"headingXs"`), `alignment`
```html
<s-heading as="h1" variant="headingXl">Orders</s-heading>
```

#### `<s-paragraph>`
Block of text; supports inline `<s-button>`, `<s-link>`, `<s-text>` children.
Props: `tone` (`"base"` \| `"subdued"` \| `"success"` \| `"critical"` \| `"caution"` \| `"magic"`)
```html
<s-paragraph tone="subdued">Last updated 2 days ago.</s-paragraph>
```

#### `<s-tooltip>`
Helpful info on hover/focus.
Props: `content` (string), `active`, `preferredPosition` (`"above"` \| `"below"` \| `"mostSpace"`), `dismissOnMouseOut`
Slot: `children` (the element to attach the tooltip to)
```html
<s-tooltip content="This action cannot be undone">
  <s-button tone="critical">Delete all</s-button>
</s-tooltip>
```

#### `<s-chip>`
Non-interactive label/tag.
Props: `tone` (`"base"` \| `"info"` \| `"success"` \| `"warning"` \| `"critical"`)
```html
<s-chip tone="success">In stock</s-chip>
```

---

## Common UI Patterns

### Full page with form sections
```html
<s-page title="Add product">
  <s-section title="Product details">
    <s-stack direction="block" gap="base">
      <s-text-field label="Title" name="title" placeholder="Short sleeve t-shirt"></s-text-field>
      <s-text-area label="Description" name="description"></s-text-area>
    </s-stack>
  </s-section>
  <s-section title="Pricing">
    <s-money-field label="Price" currency="USD" name="price"></s-money-field>
  </s-section>
</s-page>
```

### Confirmation modal (declarative, no JS)
```html
<s-button commandFor="delete-modal" command="--show" tone="critical">Delete product</s-button>

<s-modal id="delete-modal" title="Delete product?">
  <s-paragraph>This action can't be reversed.</s-paragraph>
  <div slot="footer">
    <s-stack direction="inline" gap="tight">
      <s-button commandFor="delete-modal" command="--hide">Cancel</s-button>
      <s-button variant="primary" tone="critical">Delete</s-button>
    </s-stack>
  </div>
</s-modal>
```

### Resource row with badge and actions
```html
<s-stack direction="inline" gap="base" align="space-between">
  <s-stack direction="inline" gap="tight">
    <s-thumbnail source="/img.jpg" alt="Product" size="small"></s-thumbnail>
    <s-stack direction="block" gap="none">
      <s-text fontWeight="semibold">Running Shoes</s-text>
      <s-text tone="subdued" variant="bodySm">SKU: RS-001</s-text>
    </s-stack>
  </s-stack>
  <s-stack direction="inline" gap="tight">
    <s-badge tone="success">Active</s-badge>
    <s-menu label="Actions">
      <s-button variant="tertiary">Edit</s-button>
      <s-button variant="tertiary" tone="critical">Delete</s-button>
    </s-menu>
  </s-stack>
</s-stack>
```

### Filter / search bar
```html
<s-stack direction="inline" gap="tight">
  <s-search-field label="Search" placeholder="Search products..."></s-search-field>
  <s-select
    label="Status"
    options='[{"label":"All","value":""},{"label":"Active","value":"active"},{"label":"Draft","value":"draft"}]'
  ></s-select>
</s-stack>
```

### More actions popover
```html
<s-button commandFor="more-popover" icon="menu-horizontal" variant="tertiary" accessibilityLabel="More actions"></s-button>
<s-popover id="more-popover">
  <s-stack direction="block">
    <s-button variant="tertiary">Export</s-button>
    <s-button variant="tertiary">Duplicate</s-button>
    <s-button variant="tertiary" tone="critical">Archive</s-button>
  </s-stack>
</s-popover>
```

---

## Fetching Live Docs

When you need full prop lists, all examples, or edge case details for a specific component, fetch the live docs:

```
https://shopify.dev/docs/api/app-home/web-components/{category}/{slug}
```

| Component | Slug |
|---|---|
| Button | `actions/button` |
| Clickable | `actions/clickable` |
| Link | `actions/link` |
| Menu | `actions/menu` |
| Button Group | `actions/button-group` |
| Clickable Chip | `actions/clickable-chip` |
| Badge | `feedback-and-status-indicators/badge` |
| Banner | `feedback-and-status-indicators/banner` |
| Spinner | `feedback-and-status-indicators/spinner` |
| Checkbox | `forms/checkbox` |
| Select | `forms/select` |
| Switch | `forms/switch` |
| Choice List | `forms/choice-list` |
| Color Field | `forms/color-field` |
| Color Picker | `forms/color-picker` |
| Date Field | `forms/date-field` |
| Date Picker | `forms/date-picker` |
| Drop Zone | `forms/drop-zone` |
| Email Field | `forms/email-field` |
| Money Field | `forms/money-field` |
| Number Field | `forms/number-field` |
| Password Field | `forms/password-field` |
| Search Field | `forms/search-field` |
| Text Area | `forms/text-area` |
| Text Field | `forms/text-field` |
| URL Field | `forms/url-field` |
| Box | `layout-and-structure/box` |
| Divider | `layout-and-structure/divider` |
| Grid | `layout-and-structure/grid` |
| Ordered List | `layout-and-structure/ordered-list` |
| Page | `layout-and-structure/page` |
| Query Container | `layout-and-structure/query-container` |
| Section | `layout-and-structure/section` |
| Stack | `layout-and-structure/stack` |
| Table | `layout-and-structure/table` |
| Unordered List | `layout-and-structure/unordered-list` |
| Modal | `overlays/modal` |
| Popover | `overlays/popover` |
| Avatar | `media-and-visuals/avatar` |
| Icon | `media-and-visuals/icon` |
| Image | `media-and-visuals/image` |
| Thumbnail | `media-and-visuals/thumbnail` |
| Chip | `typography-and-content/chip` |
| Heading | `typography-and-content/heading` |
| Paragraph | `typography-and-content/paragraph` |
| Text | `typography-and-content/text` |
| Tooltip | `typography-and-content/tooltip` |
