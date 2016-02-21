# Feature Flags

This document outlines how to use [Feature Flags](http://martinfowler.com/bliki/FeatureToggle.html) in the Josephine app.

## Creating a Feature

- Feature flags are stored in the application environment.
- Feature names start with a `FEATURE_` prefix.
- Features are enabled if their value is `TRUE` or `true`.
- Keys and values are case insensitive. Regardless of their case in `ENV`, they will end up `snake_cased` in Ruby land.

```sh
heroku config:set FEATURE_SF_LAUNCH=TRUE -r staging
```

In development, you'll need to add a line to the `.env` file:

```sh
FEATURE_SF_LAUNCH="TRUE"
```

## Checking for a Feature (server side)


```ruby
Features.sf_launch?
# => true

Features.nonexistent_flag?
# => false
```

## Checking for a Feature (client side)

This is not implemented yet!

## Writing Tests

Sometimes you need to write integrations tests that simulate a feature being enabled or disabled. Instead of manually making changes to `ENV` in the tests, you can use the `enable` and `disable` convenience methods:

```ruby
Features.enable(:unicorns)
Features.unicorns?
# => true

Features.disable(:unicorns)
Features.unicorns?
# => false
```
