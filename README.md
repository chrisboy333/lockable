# WithLock

Provides a DRb service to provide locking across a distributed ruby application.

## Installation

Add to your Gemfile and run the `bundle` command to install it.

```ruby
gem "with_lock"
```

**Tested under Ruby 1.9.3-p545 and 2.1.3**

Add script and config files to your project(from console):
```ruby
WithLock.setup
```
In the configuration file you can change some settings if you like ... it defaults to using the following... where 'scope' is the application directory name with rails environment appended(if present):
  url: druby://loclahost:9999
  scope: <%= File.basename(File.expand_path('.')) %><%= ":#{Rails.env}" if defined?(Rails) %>
  directory: tmp  
  
The scope is used to let different applications use the same drb server ... or different parts of an app acquire the same named locks(not that I think this latter is a great idea) ...

Start/Stop the service from ruby
```ruby
WithLock::Server.start_service
WithLock::Server.stop_service
```
## Usage
A "with_lock()" function is provided globally to wrap with_lock sections of code.
 
```ruby
with_lock('lock_name') do
  puts "This is something only I can do right now, provided others are using the locks!"
end 
```
## Development

Questions or problems? Please post them on the [issue tracker](https://github.com/chrisboy333/with_lock/issues). You can contribute changes by forking the project and submitting a pull request. You can ensure the tests passing by running `bundle` and `rake`.

This gem is created by Christopher Hauboldt and is under the MIT License.
