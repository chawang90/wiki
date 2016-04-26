# Email and SMS

This document outlines how we send emails and text messages to our users.

## Sending yourself SMS text messages

Messages go to Tal's number by default. To override, add your number
to `.env`, without the `+1` prefix:

```
TWILIO_RECIPIENT_OVERRIDE_NUMBER="5054592942"
```

You'll also need to turn sending on in our `.env` file:

```
ENABLE_SMS_DELIVERY="true"
```

## Sending yourself an email

```rb
# Find your user in the database
user = User.find_by_email('joy.j.ding@gmail.com')

# Deliver the email (on testing). Calling #deliver will actually send the email.
UserMailer.signup_confirmation(user.id).deliver

# On production, ActionMailer uses our queue, so `deliver` isn't necessary.
UserMailer.delay.signup_confirmation(user.id)
```


## Viewing Emails in Development

Emails are sent by background jobs. Be sure you're running the job worker:

```
rake jobs:clear && rake jobs:work
```

When you perform any action that sends an email (in development), that email will
open in a new tab in your browser instead of actually being sent. This convenient feature
is powered by [letter_opener](https://github.com/ryanb/letter_opener).

## Overriding the recipient of sanitized user email addresses

When you run `jodb` or `rake db:sanitize`, all customer email addresses are sanitized. Admin email addresses are left intact:

```
bob@example.com -> tal+bob__at__example.com@josephine.com
```

This means all emails get sent to `tal@josephine.com`. The `+` trick only works in Gmail:

> Append a plus ("+") sign and any combination of words or numbers after your email address. For example, if your name was hikingfan@gmail.com, you could send mail to hikingfan+friends@gmail.com or hikingfan+mailinglists@gmail.com.

To override the email address, set `SANITIZED_EMAIL_RECIPIENT` in your local `.env` file.

## Mandrill

We use Mandrill to send transactional emails. It's an add-on to Mailchimp. It's okay.

### Checking if emails sent in Mandrill.

Sometimes you need to log into Mandrill to check if an email was sent. Here's how you do it:

1. Log into MailChimp (information is in the Accounts doc)

2. Navigate to `Account` under the dropdown in the top right

3. Go to the `Transactional` tab

4. Click `Launch Mandrill`

5. You should see all of the emails that were sent:
  ![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/f6r_w355.png)

## Previewing Emails Locally

We use a nifty little gem called Letter Opener (written by Mr. Railscasts, Ryan Bates) to generate HTML templates of all emails we generate locally:

```ruby
# config/development.rb
config.action_mailer.delivery_method = :letter_opener
config.action_mailer.perform_deliveries = true
```

By default, all emails sent locally will generate local HTML templates that pop up automatically (via `launchy`) any time an email is generated:

```
meal = Meal.ended.last
CookMailer.meal_recap_after_first_meal(meal.id).deliver

# => pops open the following HTML file magically!
#    file:///Users/tal/Projects/josephine-www/tmp/letter_opener/1457643702_5e3268c/rich.html
```

If you're expecting transactional emails to send through the app (not manually, like above), you'll need to ensure your Delayed::Job queue is running.

```bash
$ # This is good practice, in case you have 1,000,000 jobs queued up
$ rake jobs:clear

$ rake jobs:work
# => running Delayed::Job and sending all emails with FooMailer.delay.mailer_method()
```
