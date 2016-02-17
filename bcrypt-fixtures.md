When you are creating fixtures for your users in Rails, you can assign them a password: 

In your `users.yml` file for example: 

```
valid_user: 
  password_digest: <%= BCrypt::Password.create('1234') %>
```

This will create a password hash that corresponds to the raw input of '1234' or whatever 
you choose to be the default password for your users. 

I would suggest that any user records you create all have the same password, so that you 
can easily remember them when using them in your other tests. 
