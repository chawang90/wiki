# Testing

This documents our testing strategy.

Some great resources:
- http://betterspecs.org/
- https://www.relishapp.com/rspec
- https://github.com/jnicklas/capybara
- https://robots.thoughtbot.com/how-we-test-rails-applications

## Integration Tests

We use Capybara for integration tests, which has its own verbs for Rspec.

### Write your tests in feature language, not implementation language

We want our integration tests to be as easy to read as possible, so that developers can read the spec and understand what users do without having to jump around code.

A few examples:

1. Prefer real URLs (`/meals/copy-from-existing`) to named routes (`copy_from_existing_meals_path`)

2. Prefer copy (`'Chapati'`) to selectors (`[data-hidden-item-...]`)

3. Use helper methods to ensure the feature steps are easy to read through (more on this below)

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

### Test Full Scenarios

Integration tests are slower than other tests, since they spawn a headless browser with Phantom JS.

For that reason, we should have try to have tests (`scenarios`) that do multiple things, and test for multiple things, in order to have a faster test suite. This is in contrast to the [Single Expectation](http://betterspecs.org/#single) best practive related to unit tests. Unit tests are faster to run.

### Helper Methods

#### When to use helper methods

In integration tests, we'll often use private, local helper methods to hide underlying DOM. An added benefit is that these methods can be reused.

An example:

```ruby
describe 'User places order' do
  scenario 'User places an order, enters special enter_special_instructions, and sees stuff.' do
    visit meal_path(meal)
    
    ...
    
    choose_item('Mac n Cheez', 2)
    click_place_order_button
  end
  
  scenario 'User places an order, enters their credit card' do
    visit meal_path(meal)
    
    ...
    
    choose_item('Lasagna', 5)
    click_place_order_button
  end
  
  private
  
  def click_place_order_button
    within '.overlay' do
      click_button 'Place Order'
    end
  end
  
 def choose_item(item_name, quantity)
    row = find_item_row(item_name)
    within row do
      select quantity, from: item_name
    end
  end
  
  def find_item_row(item_name)
    ...
  end
end
```

#### When not to use helper methods

In larger integration specs (like `user_places_order`), we've started to have "helper method bloat." In many cases, the methods are trivial (no complex DOM stuff) and not being reused. In some ways they're actually causing more confusion than good– magic methods with hidden behavior, having to parse through large files, etc.

Because of that we've started to cut down on our helper method use – a good rule of thumb is: if it's a short, easy-to-understand one-liner and it's not being reused, it's chill to keep it directly in the scenario.

```ruby
feature 'User views a neighborhood' do
  background(:each) do
    create(:meal, title: 'Friendly Neighborhood Meal', neighborhood: Neighborhood.find('downtown-oakland'))
    create(:meal, title: 'Unfriendly Neighborhood Meal', neighborhood: Neighborhood.find('nopa'))
  end

  scenario 'User views a neighborhood' do
    visit '/neighborhoods/downtown-oakland'

    expect(page).to have_content('Friendly Neighborhood Meal')
    expect(page).to_not have_content('Unfriendly Neighborhood Meal')

    expect_hero_to_have_title('Downtown Oakland')
  end

  private

  def expect_hero_to_have_title(title)
    within '.hero' do
      expect(page).to have_content(title)
    end
  end
end

```

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
