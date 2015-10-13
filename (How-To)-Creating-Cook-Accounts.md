Open the production console:

```
heroku run console -r production
```

Create or update the user record.

```ruby
props = {
  email: 'martha@stewart.com',
  first_name: 'Martha', 
  last_name: 'Stewart', 
  phone_number: '5558675309', 
  handle: 'martha-stewart'
}

user = User.find_or_initialize_by(email: props[:email])
user.first_name ||= props[:first_name]
user.last_name ||= props[:last_name]
user.phone_number ||= props[:phone_number]

if user.password_digest.blank?
  puts 'Setting password as "sharing"...'
  user.password = 'sharing'
end

user.save!

Cook.create!(user: user, handle: props[:handle])
```

Download the cook's avatar from Trello.

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/e0eeom-b.png)

Crop it to a square (Tal recommends Photoshop).

Save the file as `avatar-small.jpg`

Connect to our `josephine-production` S3 Bucket (Tal recommends Cyberduck. Zeke recommends [3Hub](http://www.3hubapp.com/) because it's free). Get the credentials with:

```
heroku config -r production | grep -i aws_
```

In `josephine-production/cooks`, Create a folder with the `handle` as the name.

Confirm that you're done by visiting the profile:

```
open http://josephine.com/cooks/martha-stewart
```

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/ha8s9srs.png)

FINAL STEP
==========

Move the Trello card to **Cook Account Complete** and leave a comment. Remember to note whether or not the user had a password, or whether it is "sharing."

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/h7__cgbg.png)

SO EASY!

