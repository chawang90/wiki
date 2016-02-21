# Testing

This documents our testing strategy.

Some great resources:
- http://betterspecs.org/
- https://www.relishapp.com/rspec
- https://github.com/jnicklas/capybara
- https://robots.thoughtbot.com/how-we-test-rails-applications

## Integration Tests

We use Capybara for integration tests, which has its own verbs for Rspec.

### Capybara/Rspec Usage

A typical integration test should follow the following format:

```ruby
feature 'Cook creates a meal' do
  context 'Addons' do
    background do
      ...
    end

    given(:cook) { create(:cook) }
    given(:meal) { create(:meal, cook: cook) }

    scenario 'Cook creates items for a meal' do
      ...
    end
  end

  context 'Location Information' do
    scenario 'Cook sees pre-filled address information and market' do
      ...
    end
  end
end
```

Note that we use `feature` instead of `describe`, `scenario` instead of `it`, `given` instead of `let`, and `background` instead of `before`. This follows the [recommended Capybara Rspec DSL](https://github.com/jnicklas/capybara#using-capybara-with-rspec) from the docs, with the addition that we still use `context` to describe groupings.

### Capybara Best Practices

Integration tests are slower than other tests, since they spawn a headless browser with Phantom JS.

For that reason, we should have try to have tests (`scenarios`) that do multiple things, and test for multiple things, in order to have a faster test suite. This is in contrast to the [Single Expectation](http://betterspecs.org/#single) best practive related to unit tests. Unit tests are faster to run.

### Smoke-Testing Slack Notifications

Slack notifications are enqueued as jobs. If you're testing them out in development, you'll need to run the job worker:

```
rake jobs:clear && rake jobs:work
```

You'll also need to set `SLACK_NOTIFICATIONS_ENABLED` to `true` in your `.env` file, and restart your development server so the environmental changes take effect.

To keep noisy test data out of real slack channels, all non-production notifications are
re-routed to the `#nerds-testing` channel.

### Accessing Airbrake

We use [Airbrake.io](https://airbrake.io) to catch bugs in production. To view our account in the browser, you need to do the single-sign on dance through Heroku:

```sh
heroku addons:open airbrake -r production
```

This should pop open your browser and take you to airbrake.io, and your session will last for a while. If you get logged out, use the above `heroku` command again to log back in.
