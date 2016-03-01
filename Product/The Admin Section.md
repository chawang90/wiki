# The Admin Section

We have an admin app! Yay!

## Using It

Go to `/admin`. The production environment will ask you for a HTTP password, it's `tal` / `saf`.

## Building It

We have separate routes, controllers, stylesheets (mostly Bootstrap), and layouts for our admin behavior.

- `app/views/layouts/admin.html.erb`
- `app/views/admin/*`
- `app/assets/stylesheets/admin.css.scss`
- `app/assets/javascripts/admin.js

We also have integration tests. Examples:

- `spec/features/admin_creates_cook_account_spec.rb`
- `spec/features/admin_creates_neighborhood_spec.rb`
- `spec/features/admin_creates_meal_notice_spec.rb`
- etc etc etc
