# The Revere Mobile Ruby Gem

[![Build
Status](https://travis-ci.org/revolution-messaging/revere_mobile_ruby_client.svg?branch=master)](https://travis-ci.org/revolution-messaging/revere_mobile_ruby_client)
[![Gem Version](https://badge.fury.io/rb/revere_mobile.svg)](https://badge.fury.io/rb/revere_mobile)

# Quick Start

Add this line to your applications Gemfile:

```ruby
gem 'revere_mobile'
```

And then execute

```sh
$ bundle
```

Or install as standalone gem:

```sh
$ gem install revere_mobile
```

# Configuration

Revere Mobile takes a block to be configured:

```ruby
RevereMobile.configure do |config|
  # Configure the API Endpoint
  # See https://mobile-developers.reverehq.com for more info for API Versions
  config.api_endpoint = 'https://mobile.reverehq.com/api/v1'
  # Configure an API Key
  config.api_key = 'd1286a1a-f2e7-421a-91b8-f8cc8201558f'
  # Defaults to "Revere Mobile Ruby Gem #{RevereMobile::VERSION}"
  config.user_agent = 'CustomUserAgent'
end
```

You can also configure options in a configuration object like so:

```ruby
RevereMobile.configuration.api_key = 'd1286a1a-f2e7-421a-91b8-f8cc8201558f'
```

For workers, for many instances you can create multiple configurations. This is also helpful for switching sessions based on
username and password authentication.

```ruby
configuration = RevereMobile::Configuration.new
configuration.username = 'example'
configuration.password = 'example'
client = RevereMobile::Client.new(configuration)
client.login 
```

# Requests

Using a `Username` and `Password` this sets the session via the `#login` method.

```ruby
configuration = RevereMobile::Configuration.new
configuration.username = 'example'
configuration.password = 'example'
client = RevereMobile::Client.new(configuration)
client.login # saves the session cookie for the instance of the client
client.campaigns # returns lists of campaigns
```

You can also make requests directly with the module by just defining the `api_key`:

```ruby
RevereMobile.configuration.api_key = 'd1286a1a-f2e7-421a-91b8-f8cc8201558f'
RevereMobile.campaigns
```


# Development

Download this repo and run `rake spec` to run the tests.

A console method has also been included, run `bin/console` to get a pry prompt in which to experiment.

```ruby
% bin/console
[1] pry(main)> RevereMobile::VERSION
# => "x.x.x"
[2] pry(main)> RevereMobile.configuration.api_key = 'd1286a1a-f2e7-421a-91b8-f8cc8201558f'
# => "d1286a1a-f2e7-421a-91b8-f8cc8201558f"
[3] pry(main)> RevereMobile.campaigns
# => {
#  "page"=>1,
# "size"=>-1,
# "total"=>119,
# "collection"=>
# ...}
```
