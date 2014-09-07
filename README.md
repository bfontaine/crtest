# crtest

`crtest` is a simple tests module for [Crystal][].

[Crystal]: http://crystal-lang.org/

Note: This was written with/for Crystal 0.4.3. The language API is not stable
right now, this library might not work with future versions.

## Usage

Write your code as usual, using the `$TESTS` global variable to check if you’re
in a test environment.

For example:

```crystal
# hello.cr

def hello(name)
  puts "hello #{name}"
end

hello("world") unless $TEST
```

Write your tests in another file, and require `crtest` at its top:

```crystal
# hello_tests.cr

require "crtest"
require "./hello"
```

Tests must be enclosed in a test suit:

```crystal
# declare a tests suit, with an optional name
ts = TestsSuite.new "MyTestSuite"

ts.run do |tr|
  # all your tests
end
```

Each test is another block:

```crystal
  tr.test("an awesome feature") do |t|
    # ...
  end
```

`t` is a test runner. It has the following test methods:

* `assert_equal(ref, value)`: pass only if both values are equal (`==`)
* `assert_true(value)`: pass only if `value` is truthy
* `assert_false(value)`: pass only if `value` is falsy
* `assert_nil(value)`: pass only if `value` is `nil`

You can also use the lower-level method `assert`:

```crystal
t.assert("didn't work as expected") do
  # ...
end
```

It takes a text to print if the test fail and a block. The block must return a
`truthy` value (i.e. not `false` or `nil`) to be considered as a success.
