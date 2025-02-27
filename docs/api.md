---
layout: default
title: API
---

<!-- Warning: AUTO-GENERATED file, do not edit. Add code comments to your Ruby instead <3 -->

# API

## Class methods

### .with_collection(collection, **args)

Render a component for each element in a collection ([documentation](/guide/collections)):

    render(ProductsComponent.with_collection(@products, foo: :bar))

### .with_collection_parameter(parameter)

Set the parameter name used when rendering elements of a collection ([documentation](/guide/collections)):

    with_collection_parameter :item

## Instance methods

### #_output_postamble → [String]

EXPERIMENTAL: Optional content to be returned after the rendered template.

### #before_render → [void]

Called before rendering the component. Override to perform operations that
depend on having access to the view context, such as helpers.

### #before_render_check → [void] (Deprecated)

Called after rendering the component.

_Use `#before_render` instead. Will be removed in v3.0.0._

### #controller → [ActionController::Base]

The current controller. Use sparingly as doing so introduces coupling
that inhibits encapsulation & reuse, often making testing difficult.

### #helpers → [ActionView::Base]

A proxy through which to access helpers. Use sparingly as doing so introduces
coupling that inhibits encapsulation & reuse, often making testing difficult.

### #render? → [Boolean]

Override to determine whether the ViewComponent should render.

### #render_in(view_context, &block) → [String]

Entrypoint for rendering components.

- `view_context`: ActionView context from calling view
- `block`: optional block to be captured within the view context

Returns HTML that has been escaped by the respective template handler.

### #request → [ActionDispatch::Request]

The current request. Use sparingly as doing so introduces coupling that
inhibits encapsulation & reuse, often making testing difficult.

### #with_variant(variant) → [self] (Deprecated)

Use the provided variant instead of the one determined by the current request.

_Will be removed in v3.0.0._

## Configuration

### #default_preview_layout

Set a custom default layout used for preview index and individual previews:

    config.view_component.default_preview_layout = "component_preview"

### #generate_stimulus_controller

Always generate a Stimulus controller alongside the component:

    config.view_component.generate_stimulus_controller = true

Defaults to `false`.

### #preview_controller

Set the controller used for previewing components:

    config.view_component.preview_controller = "MyPreviewController"

Defaults to `ViewComponentsController`.

### #preview_path (Deprecated)

_Use `preview_paths` instead. Will be removed in v3.0.0._

### #preview_paths

Set the location of component previews:

    config.view_component.preview_paths << "#{Rails.root}/lib/component_previews"

### #preview_route

Set the entry route for component previews:

    config.view_component.preview_route = "/previews"

Defaults to `/rails/view_components` when `show_previews` is enabled.

### #render_monkey_patch_enabled

Set if render monkey patches should be included or not in Rails <6.1:

    config.view_component.render_monkey_patch_enabled = false

### #show_previews

Enable or disable component previews:

    config.view_component.show_previews = true

Defaults to `true` in development.

### #show_previews_source

Enable or disable source code previews in component previews:

    config.view_component.show_previews_source = true

Defaults to `false`.

### #test_controller

Set the controller used for testing components:

    config.view_component.test_controller = "MyTestController"

Defaults to ApplicationController. Can also be configured on a per-test
basis using `with_controller_class`.

### #view_component_path

Path for component files

    config.view_component.view_component_path = "app/my_components"

Defaults to "app/components".

## ViewComponent::TestHelpers

### #render_inline(component, **args, &block) → [Nokogiri::HTML]

Render a component inline. Internally sets `page` to be a `Capybara::Node::Simple`,
allowing for Capybara assertions to be used:

```ruby
render_inline(MyComponent.new)
assert_text("Hello, World!")
```

### #with_controller_class(klass)

Set the controller to be used while executing the given block,
allowing access to controller-specific methods:

```ruby
with_controller_class(UsersController) do
  render_inline(MyComponent.new)
end
```

### #with_request_url(path)

Set the URL for the current request (such as when using request-dependent path helpers):

```ruby
with_request_url("/users/42") do
  render_inline(MyComponent.new)
end
```

### #with_variant(variant)

Set the Action Pack request variant for the given block:

```ruby
with_variant(:phone) do
  render_inline(MyComponent.new)
end
```
