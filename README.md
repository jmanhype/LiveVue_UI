# LiveVue UI

A comprehensive UI component library built on top of [LiveVue](https://github.com/Valian/live_vue), providing accessible, customizable Vue components that integrate seamlessly with Phoenix LiveView.

## Features

- **Accessible Components**: Built on [Reka UI](https://reka-ui.com/), ensuring ARIA-compliant, keyboard-navigable components
- **Phoenix LiveView Integration**: Seamless server-side rendering and reactivity
- **Tailwind CSS Styling**: Beautiful, customizable designs out of the box
- **TypeScript Support**: Fully typed Vue components for better DX
- **Easy Setup**: Simple Mix task to get started quickly

## Installation

1. Add `live_vue_ui` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:live_vue_ui, "~> 0.1.0"}
  ]
end
```

2. Ensure you have LiveVue set up in your project. If not, run:

```bash
mix live_vue.setup
```

3. Run the LiveVue UI setup task:

```bash
mix live_vue_ui.setup
```

This will:
- Install necessary npm packages (@reka-ui/dialog, @reka-ui/dropdown-menu, etc.)
- Configure your Vue app to use LiveVue UI components
- Set up the required asset pipeline configuration

## Usage

### Importing Components

In your LiveView module, import the components:

```elixir
defmodule MyAppWeb.MyLive do
  use MyAppWeb, :live_view
  import LiveVueUI.Components

  # ... your LiveView code
end
```

### Button Component

The button component provides a fully styled, accessible button with multiple variants and sizes.

```elixir
<.button>Click me</.button>

<.button variant={:secondary} size={:lg}>
  Large Secondary Button
</.button>

<.button variant={:outline} phx-click="save">
  Save Changes
</.button>

<.button disabled={true}>
  Disabled Button
</.button>
```

**Props:**
- `variant`: `:primary` | `:secondary` | `:outline` | `:ghost` (default: `:primary`)
- `size`: `:sm` | `:md` | `:lg` (default: `:md`)
- `disabled`: `boolean` (default: `false`)
- `class`: Additional CSS classes
- All standard Phoenix attributes (`phx-click`, `phx-value-*`, etc.)

### Modal Component

The modal component provides an accessible dialog with backdrop, title, content, and footer.

```elixir
<.modal
  title="Confirm Action"
  open={@show_modal}
  on_close="close_modal"
>
  Are you sure you want to proceed?

  <:footer>
    <.button variant={:outline} phx-click="close_modal">
      Cancel
    </.button>
    <.button phx-click="confirm_action">
      Confirm
    </.button>
  </:footer>
</.modal>
```

**Props:**
- `title`: `string` (required) - The modal title
- `open`: `boolean` (default: `false`) - Control modal visibility
- `on_close`: `string` | `Phoenix.LiveView.JS` - Event or JS command when modal closes
- `max_width`: `"sm"` | `"md"` | `"lg"` | `"xl"` | `"2xl"` | `"full"` (default: `"md"`)

**Slots:**
- Default slot: Modal content
- `footer`: Custom footer content (optional)

## Available Components

Currently implemented:
- **Button**: Customizable button with multiple variants
- **Modal**: Accessible dialog/modal component

Coming soon:
- Dropdown Menu
- Tabs
- Tooltip
- Popover
- Accordion
- Alert Dialog

## Architecture

LiveVue UI bridges Vue components with Phoenix LiveView:

```
Phoenix LiveView (Elixir)
    “
LiveVueUI.Components (Elixir function components)
    “
LiveVue (Bridge)
    “
Vue Components (TypeScript/Vue 3)
    “
Reka UI (Accessible UI primitives)
```

## Development

### Running Tests

```bash
mix test
```

### Building Assets

```bash
cd assets
npm install
npm run build
```

### Generating Documentation

```bash
mix docs
```

## Examples

Check out the [example Phoenix app](./example) for a full demonstration of all components.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT License - see [LICENSE.md](LICENSE.md) for details.

## Credits

- Built on [LiveVue](https://github.com/Valian/live_vue) by Valian
- Uses [Reka UI](https://reka-ui.com/) for accessible Vue components
- Inspired by [shadcn/ui](https://ui.shadcn.com/) and [Radix UI](https://www.radix-ui.com/)
