# Overlays and Wizard Steps

We use overlays in some places and have some nice library code to make adding (and transitioning to) them super easy.

## How to use

Create a new overlay partial:

```
app/views/overlays/meals/_confirm_sales.html.erb
```

And render it anywhere in the template you're working in:

```erb
<!-- app/views/meals/sales.html.erb -->
<%= content_for :overlay do %>
  <%= render 'overlays/meals/confirm_sales' %>
<% end %>
```

The only thing the partial needs is a `wizard-step` class and has a data attribute with that step's name.

```erb
<!-- app/views/overlays/meals/_confirm_sales.html.erb -->
<div class="wizard-step" data-wizard-step="confirm-sales">
  ...
</div>
```

Then, to open the overlay to the appropriate wizard step, create a button with the following:

```erb
<!-- app/views/meals/sales.html.erb -->
<button class="open-overlay-trigger wizard-step-trigger" data-wizard-step="confirm-sales">
  Confirm My Sales
</button>
```

The `open-overlay-trigger` class will cause our overlay modal to open, and the `wizard-step-trigger` class, coupled with the data attribute, will cause the `confirm-sales` wizard step to open up.
