# Removing Customer Credit Cards

There are rare occasions where customers ask for their credit cards to be removed from the system.

## Step By Step Guide

Fire up the production console:

```bash
heroku run console -r production
```

Find the user and remove their stripe info:

```ruby
user = User.find_by_email('mrs-no-more-credit-card@example.com')
user.update!(stripe_id: nil, stripe_last_4: nil)
```

Then visit [dashboard.stripe.com](https://dashboard.stripe.com) and remove their credit card info.
