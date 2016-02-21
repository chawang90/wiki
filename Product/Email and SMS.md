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

We use Mandrill to send emails. It's made by Mailchimp. It's okay.

### Checking if emails sent in Mandrill.

Sometimes you need to log into Mandrill to check if an email was sent. Here's how you do it:

1. Log into Heroku (information is in the Accounts doc)

1. [Click this link to go directly to Mandrill](https://addons-sso.heroku.com/apps/josephine-members/addons/d0531461-5386-4bb3-9a06-76a6ae94e9d6)

1. Click on "Outbound"

1. You should see all of the emails that were sent:
  ![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/f6r_w355.png)


