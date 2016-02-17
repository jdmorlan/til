Setting up SendGrid for a Rails/Heroku application. 

1. In `app/config/environments/production.rb` insert the following: 

```
ActionMailer::Base.smtp_settings = {
  user_name: ENV['SENDGRID_USERNAME'],
  password: ENV['SENDGRID_PASSWORD'],
  domain: 'domain for your site', 
  address: 'smtp.sendgrid.net', 
  port: 587, 
  authentication: :plain, 
  enable_starttls_auto: true
}
```

When you add SendGrid to your Heroku application it should add the appropriate environment variables. 
