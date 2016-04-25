Multiple Route files in Rails 

1. Create a folder in your config folder named routes 
2. In you application.rb file iterate over the files and add them to the config/routes.rb config path in Rails 

at config/application.rb

```
Dir[Rails.root.join('config/routes/*.rb').each do |file|
  config.paths['config/routes.rb'] << file
end
```

at config/routes/version_one.rb

```
Rails.application.routes.draw do
  get 'test_v1' => 'controller#action'
end
```

at config/routes/version_two.rb

```
Rails.application.routes.draw do 
  get 'test_v1' => 'controller#action'
end
```

You should see both routes when you run `rake routes`
