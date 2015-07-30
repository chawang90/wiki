Open the production console:

```
heroku run console -r production
```

Create or update the user record.

```ruby
props = { email: 'martha@stewart.com', first_name: 'Martha', last_name: 'Stewart', phone_number: '5558675309', handle: 'martha-stewart' }

user = User.find_or_initialize_by(email: props[:email])
user.first_name ||= props[:first_name]
user.last_name ||= props[:last_name]
user.phone_number ||= props[:phone_number]

unless user.password_digest.present?
  puts 'Setting password as "sharing"..."
  user.password = 'sharing'
end

user.save!

cook.create(user: user, handle: props[:handle])
```