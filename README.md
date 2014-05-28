## Test::Unit support for Spork with ruby 1.9.2 and Rails 3.2.x support

This includes a plugin for spork to enable Test::Unit support for spork. It also comes with a very bare-bones drb client to run tests.

Then, once spork is running, invoke `testdrb`:
```ruby
$ testdrb path/to/your_test.rb
```
to run your tests under Spork.

Good part is that you still able to run your tests in `old` manner, like
```ruby
$ rake test TEST=path/to/your_test.rb
```
or simply
```ruby
$ rake test
```
to tun all test suite.

### Gotchas
This gem autoloads `test_helper.rb` file, so there is no need to require it in every test file.
But if you have already a bunch of tests WITH `require 'test_helper.rb'`
at the bottom of each test file and you need to
be compatible with some CI servers (you don't want to remove that line) then to avoid error message like "no such file to load `test_helper.rb`" you will need to add these extra config line to `Spork.each_run` block:


```ruby
Spork.each_run do
  $LOAD_PATH << "test/"
end
```

Now you should be compatible with Spork and CI servers.
