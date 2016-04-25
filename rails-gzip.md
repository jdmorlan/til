You can encode your responses with GZip, which can decrease the amount of 
bandwidth required. Since Rails is Rack compatible you can use the 
`Rack::Deflator` middleware. 

You can add the middleware by adding the following code to your 
`config/application.rb` file within the `Application` class 
definition. 

```
config.middleware.use Rack::Deflator
```

The app that I added this to was an API, from what I can tell 
the browser decodes Gzip'd responses for you, but when I was 
testing I had to decode the response manually. `ActiveSupport` 
provides methods for this. In my `test/test_helper.rb` file I 
defined the following method to get the decoded response. 

```
def get_json_response
  decompressed_body = ActiveSupport::Gzip.decompress(response.body)
  HashWithIndifferentAccess.new(JSON.parse(decompressed_body))
end
```
