---
layout: default
title: Instrumentation
parent: Guide
---

# Instrumentation

To enable ActiveSupport notifications, use the `instrumentation_enabled` option:

```ruby
# config/application.rb
# Enable ActiveSupport notifications for all ViewComponents
config.view_component.instrumentation_enabled = true
```

Then subscribe to the `!render.view_component` event:

```ruby
ActiveSupport::Notifications.subscribe("!render.view_component") do |event|
  event.name    # => "!render.view_component"
  event.payload # => { name: "MyComponent", identifier: "/Users/mona/project/app/components/my_component.rb" }

  ApplicationComponent.logger.debug \
    "  Rendered #{bold}#{event.payload[:name]}#{clear}" \
    " (Duration: #{event.duration.round(1)}ms | Allocations: #{event.allocations})"
end
```
