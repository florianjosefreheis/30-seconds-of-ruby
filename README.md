# 30 Seconds of Ruby

![RubyLogo](/ruby_logo.png)

Ruby snippets you can understand in 30 seconds or less.

Inspired by [30-seconds-of-knowledge](https://github.com/petrovicstefanrs/30_seconds_of_knowledge/).

[Element: hr]

## Snippets

### Ruby's Ancestor Chain

Always wondered how to see Ruby's class hierarchy? Simply call `ancestors` on aclass to see the ancestor chain.

The return array contains the following order:

- the calling class
- its included modules
- its parent class
- the included modules of its parents class
- the parent class of its parent class

Here is the ancestor chain of the String class:

```ruby
irb> String.ancestors
=> [String, Comparable, Object, Kernel, BasicObject]
```

#### Additional links

- [Ruby Doc - Ancestors](https://ruby-doc.org/core-2.6.1/Module.html#method-i-ancestors)

[⬆ Back to top](#30-seconds-of-ruby)

### What is a Ruby Interpreter?

A Ruby interpreter is any program that parses the Ruby source code to imitate its behavioral execution. It converts the program line by line compared to a compiler which converts the whole program at once. Hence, a code change only requires an edit. Interpreters only throw an error if the program gets executed and reach the line that containes the error, whereas compilers will throw the error already before execution.
There are multiple versions of Ruby interpreters to choose from, each with a different but very similar set of rules and options.

Common Ruby Interpreters:

- Ruby MRI
- JRuby
- YARV
- Rubinius

[⬆ Back to top](#30-seconds-of-ruby)

### Ruby's .methods method

If you've ever wondering what methods are available for a specific object, just call `.methods` on it:

```bash
irb> name = 'Bob'
 => "Bob"
irb> name.methods
 => [:include?, :%, :unicode_normalize, :*, :+, :to_c, ...]
```

This will return an array of symbols (names) of all publicly accessible methods of the object and its ancestors.

[⬆ Back to top](#30-seconds-of-ruby)

### BasicObject

The BasicObject class is the top parent of all class. It is a blank instance of class `class` with no superclass and contains a minimum of methods for object creation and comparison.

```bash
irb> class User
irb> end
 => nil
irb> User
 => User
irb> User.class
 => Class
irb> User.superclass
 => Object
irb> Object.ancestors
 => [Object, Kernel, BasicObject]
irb> BasicObject.class
 => Class
irb> BasicObject.superclass
 => nil
irb> BasicObject.ancestors
 => [BasicObject]
```

#### Additional links

- [Ruby Doc - BasicObject](https://ruby-doc.org/core-1.9.3/BasicObject.html)

[⬆ Back to top](#30-seconds-of-ruby)

### Hash#dig

Ever wondered if there is a better way how you can traverse through multi-layer hashes or arrays to retrieve a specific value? Luckily Ruby 2.3 introduced a new method called `dig`.

```ruby
  catalogue = {
    drinks: {
      apple_juice: {
        stock: 8,
        price_per_unit: 2.4
      },
      orange_juice: {
        stock: 4,
        price_per_unit: 2.2
      }
    }
  }
```

Given the above hash, we would access the price per unit of the orange juice by the below line.

```ruby
  catalogue[:drinks][:carrot_juice][:price_per_unit]
  => NoMethodError: undefined method `[]' for nil:NilClass
```

To mitigate Rails to throw an error we need to check the existence of each key while navigating through the hash structure.

```ruby
  catalogue[:drinks] && catalogue[:drinks][:carrot_juice] && catalogue[:drinks][:carrot_juice][:price_per_unit]
```

By using `dig` we follow **DRY** and retrieve the value of each key object by dealing smoothly with nil values.

```ruby
  catalogue.dig(:drinks, :carrot_juice, :price_per_unit)
  => nil
  catalogue.dig(:drinks, :apple_juice, :price_per_unit)
  => 2.4
```

#### Additional links

- [Ruby Doc - Hash#dig](https://ruby-doc.org/core-2.3.0_preview1/Hash.html#method-i-dig)

[⬆ Back to top](#30-seconds-of-ruby)

### Method Naming Conventions "!" vs. "?"

In Ruby there are two common naming conventions for methods. Either you end a method name with a **!** or **?**.
Methods ended by a **!** are called bang methods and often modifies the original object.

```bash
irb> book_title = "example book title"
 => "example book title"
irb> puts book_title.capitalize!
Example book title
 => nil
irb> puts book_title
Example book title
 => nil
irb>
```

A famous example is `merge` vs `merge!` when dealing with params, whereas the former method will return the params and the latest modifies the original params.

The question mark at the end of a method name indicates that we can expect a boolean as return value.

```bash
irb> array = []
 => []
irb> array.empty?
 => true
irb> user = { 'first_name' => 'Bob', 'last_name' => 'Carlton' }
irb> user.has_key?('first_name')
 => true
```

#### Additional links

- [Awesome post about Ruby's conventions](https://blog.codeminer42.com/and-understanding-one-of-rubys-coolest-naming-conventions-5a9300b75605)

[⬆ Back to top](#30-seconds-of-ruby)

### Kernel (module)

The Kernel module is included by class Object and provides methods that are globally available, hence every Ruby object has access to them. These methods are called without a receiver and only act on the passed arguments.

Famouse representative of the Kernel module are:

- Array
- Hash
- Integer
- Hash
- p, print and puts

#### Additional links

- [Ruby Doc - Kernel](https://ruby-doc.org/core-2.6.1/Kernel.html)

[⬆ Back to top](#30-seconds-of-ruby)

### Where do methods live?

Ever wondered how you can find out where exactly a method lives inside Ruby?

Ruby offers two helpful methods here. By passing the name of the method as a symbol to `owner` will reveal where a method lives inside Ruby. If you curious about who receives s specific method, just pass the name again as a symbol to `receiver`.

```bash
irb> method(:initialize).owner
 => BasicObject
irb> method(:initialize).receiver
 => main
```

#### Additional links

- [Ruby Doc - owner](https://apidock.com/ruby/v1_9_3_392/Method/owner)
- [Ruby Doc - receiver](https://apidock.com/ruby/v1_9_3_392/Method/receiver)

[⬆ Back to top](#30-seconds-of-ruby)

### Ruby -e

The `ruby` command is mostly known for running a ruby app or script. But it also has a number of interesting options to offer.

Execute a single line code snippet just by using the -e flag:

```bash
  ruby -e '[1, 2, 3].each do |e| puts e end'
```

[⬆ Back to top](#30-seconds-of-ruby)

### Integer#digits(base)

Calling `digits` on an integer returns the array including the digits extracted by place-value notation with radix base of int.

```bash
irb> 123.digits
 => [3, 2, 1]
irb> 14.digits(7)
 => [0, 2]
```

#### Additional links

- [Ruby Doc - Integer#digits](https://ruby-doc.org/core-2.4.0/Integer.html#method-i-digits)

[⬆ Back to top](#30-seconds-of-ruby)

### values_at

Using `values_at`to retrieve multiple non-sequential values of arrays and hashes.

For a given array it will return an array of the values associated with the index position.

```bash
  irb> programming_languages = ['Ruby', 'Python', 'Golang', 'C++', 'C', 'D']
   => ["Ruby", "Python", "Golang", "C++", "C", "D"]
  irb> programming_languages.values_at(0, 2, 4)
   => ["Ruby", "Golang", "C"]
```

For a given hash it will return an array of the values associated with the given keys.

```bash
  irb> fruits = { 'orange' => '$2.00', 'apple' => '$3.00', 'grapes' => '$2.50' }
   => => {"orange"=>"$2.00", "apple"=>"$3.00", "grapes"=>"$2.50"}
  irb> fruits.values_at('orange')
   => ["$2.00"]
```

#### Additional links

- [Ruby Doc - Array#values_at](https://apidock.com/ruby/Array/values_at)
- [Ruby Doc - Hash#values_at](https://apidock.com/ruby/Hash/values_at)

[⬆ Back to top](#30-seconds-of-ruby)

### Splat operators

The \*splat operator has almost endless uses. But the main idea is that whenever you don’t want to specify the number of arguments you have, you would use a splat operator. The simplest example would be something like this:

```bash
irb> def foo(*args)
irb>  args
irb> end
 => :foo
irb> foo(1,5,9)
[1, 5, 9]
 => [1, 5, 9]
```

You can also use the splat operator to grab any segment of an array:

```bash
irb> first, second, *last = ["x", "y", "w", "z"]
 => ["x", "y", "w", "z"]
irb> first
 => "x"
irb> second
 => "y"
irb> last
 => ["w", "z"]
```

#### Additional links

- [Splat operators](https://medium.freecodecamp.org/rubys-splat-and-double-splat-operators-ceb753329a78)

[⬆ Back to top](#30-seconds-of-ruby)

### to_s vs. to_str

`to_s` is an explicit casting helper and is used to transform a value from one type to another. `to_str` is an implicit casting helper
with the same purpose. The difference is that the former will always return a string whereas the later will result in an error or data loss
if the value it acts on does not act like the type we are casting. Ruby will only return a value when objects act like the type.
Ruby is very strict when using an implicit casting helper to ensure that the value acts like the type we want.

```bash
irb> [1, 2].to_s
 => "[1, 2]"
irb> [1, 2].to_str
NoMethodError: undefined method `to_str` for [1, 2]:Array
Did you mean? to_s
irb> :name.to_s
 => "name"
irb> :name.to_str
NoMethodError: undefined method `to_str` for :name:Symbol
Did you mean? to_s
```

[⬆ Back to top](#30-seconds-of-ruby)

### to_i vs. to_int

`to_i` is an explicit casting helper and is used to transform a value from one type to another. `to_int` is an implicit casting helper
with the same purpose. The difference is that the former will always return a string whereas the later will result in an error or data loss
if the value it acts on does not act like the type we are casting. Ruby will only return a value when objects act like the type.
Ruby is very strict when using an implicit casting helper to ensure that the value acts like the type we want.

```bash
irb> 19.99.to_i
 => 19
irb> 19.99.to_int
 => 19
irb> '19.99'.to_i
 => 19
irb> '19.99'.to_int
NoMethodError: undefined method `to_int` for "String":String
Did you mean?  to_i
               to_str
```

[⬆ Back to top](#30-seconds-of-ruby)

### lamba vs. proc

A **lambda** is a way to define a block & its parameters with some special syntax. You can save this **lambda** into a variable for later use.

The syntax for defining a Ruby **lambda** looks like this:

```bash
irb > say_something = -> { puts "This is a lambda" }
 => #<Proc:0x0000556829fa2fa8@(lambda)>
```

Defining a **lambda** won’t run the code inside it, just like defining a method won’t run the method, you need to use the call method for that.

```bash
irb > say_something = -> { puts "This is a lambda" }
 => #<Proc:0x0000556829fa2fa8@(lambda)>
irb > say_something.call
 This is a lambda
 => nil
```

**Procs** are a very similar concept. But one of the differences is how you create them.

```bash
irb > my_proc = Proc.new { |x| puts x }
 => #<Proc:0x0000556829f8ad68@>
```

There is no dedicated **Lambda** class. A **lambda** is just a special **Proc** object. If you take a look at the instance methods from **Proc**, you will notice there is a `lambda?` method.

```bash
irb > my_proc = Proc.new { |x| puts x }
 => #<Proc:0x0000556829f8ad68@>
irb > my_proc.lambda?
 => false
irb > my_lambda = -> { puts "This is a lambda" }
 => #<Proc:0x0000556829f59a60@(lambda)>
irb > my_lambda.lambda?
 => true
```

A **proc** behaves differently than a **lambda**, specially when it comes to arguments. Procs don’t care about the correct number of arguments, while lambdas will raise an exception.

```bash
irb > my_proc = Proc.new { |x,y| puts "I do not care about arguments!" }
 => #<Proc:0x0000556829f8ad68@>
irb > my_proc.call
 I do not care about arguments!
 => nil
irb > my_lambda = -> x { "x = #{x}" }
 => #<Proc:0x000056145b4325e0@(lambda)>
irb > my_lambda.call
 ArgumentError (wrong number of arguments (given 0, expected 1))
irb > my_lambda.call(10)
 => "x = 10"
```

#### Additional links

- [Ruby Guides - Lambdas vs Procs](https://www.rubyguides.com/2016/02/ruby-procs-and-lambdas/)

[⬆ Back to top](#30-seconds-of-ruby)

### to_a vs. to_ary

`to_a` is an explicit casting helper and is used to transform a value from one type to another. `to_ary` is an implicit casting helper
with the same purpose. The difference is that the former will always return a string whereas the later will result in an error or data loss
if the value it acts on does not act like the type we are casting. Ruby will only return a value when objects act like the type.
Ruby is very strict when using an implicit casting helper to ensure that the value acts like the type we want.

```bash
irb > { key: :value }.to_a
 => [[:key, :value]]
irb > { key: :value }.to_ary
NoMethodError: undefined method `to_ary` for {:key=>:value}:Hash
Did you mean?  to_a
```

[⬆ Back to top](#30-seconds-of-ruby)

### map vs. each

The way the `map` method works in Ruby is, it takes an enumerable object, (i.e. the object you call it on), and a block.

Then, for each of the elements in the enumerable, it executes the block, passing it the current element as an argument. The result of evaluating the block is then used to construct the resulting array.

In other words:

> Applying map on an array returns a new array where each element is the result of evaluating the block with the element as an argument.

```bash
irb> a = [1, 2, 3]
 => [1, 2, 3]
irb> b = a.map { |n| n * 2 }
 => [2, 4, 6]
irb> b
 => [2, 4, 6]
```

`each` is just another method on an object. That means that if you want to iterate over an array with `each`, you’re calling the `each` method on that array object.

It takes a list as it’s first argument and a block as the second argument. For every element in the list, it runs the block passing it the current element as a parameter.

You should use `each` when you want iteration but don’t care about what it returns.

[1, 2, 3].each { |n| puts "Current number is: #{n}" }

```bash
irb> [1, 2, 3].each { |n| puts "Current number is: #{n}" }
 Current number is: 1
 Current number is: 2
 Current number is: 3
 => [1, 2, 3]
irb> a = [1, 2, 3]
 => [1, 2, 3]
irb> b = a.each { |n| n * 2 }
 => [1, 2, 3]
irb> b
 => [1, 2, 3]
```

[⬆ Back to top](#30-seconds-of-ruby)

### Enumerable#cycle

Ruby's `Enumerable#cycle` offers an easy way to either repeat a certain pattern n times or just to switch between two predefined states.

Repeating a certain pattern:

```bash
irb> array = [1, 2, 3]
 => [1, 2, 3]
irb> array.cycle(3).to_a
 => [1, 2, 3, 1, 2, 3, 1, 2, 3]
```

Switching between two states:

```bash
irb> button = ['on', 'off'].cycle
 => #<Enumerator: ["on", "off"]:cycle>
irb> button.next
 => "on"
irb> button.next
 => "off"
```

#### Additional links

- [Ruby Doc - Enumerable#cycle](https://ruby-doc.org/core-2.6.1/Enumerable.html#method-i-cycle)

[⬆ Back to top](#30-seconds-of-ruby)

### Enumerable#all?

Passes each element of the collection to the given block. The method returns true if the block never returns false or nil. If the block is not given, Ruby adds an implicit block of `{ |obj| obj }` which will cause `all?` to return true when none of the collection members are false or nil.

```bash
irb> a = [1, 2, 3]
 => [1, 2, 3]
irb> a.all?(&:integer?)
 => true
irb> a.all?(&:odd?)
 => false
irb> a.all?
 => true
irb> a = [1, 2, nil]
 => [1, 2, nil]
a.all?
 => false
```

#### Additional links

- [Ruby Doc - Enumerable#all?](https://ruby-doc.org/core-2.6.1/Enumerable.html#method-i-all-3F)

[⬆ Back to top](#30-seconds-of-ruby)

## Enumerable#none?

Passes each element of the collection to the given block. The method returns true if the block never returns true for all elements. If the block is not given, `none?` will return true only if none of the collection members is true.

```bash
irb> a = []
 => []
irb> a.none?
 => true
irb> a = ['a', 'bb', 'c']
 => ["a", "bb", "c"]
irb> a.none? { |e| e.length > 1 }
 => false
irb> (1..10).none?(&:nil?)
 => true
```

#### Additional links

- [Ruby Doc - Enumerable#none?](https://ruby-doc.org/core-2.6.1/Enumerable.html#method-i-none-3F)

[⬆ Back to top](#30-seconds-of-ruby)

## Enumerable#any?

Passes each element of the collection to the given block. The method returns true if the block ever returns a value other than false or nil. If the block is not given, Ruby adds an implicit block of `{ |obj| obj }` that will cause `any?` to return true if at least one of the collection members is not false or nil.

```bash
irb> a = []
 => []
irb> a.any?
 => false
irb> a = [1, 'a']
 => [1, "a"]
irb> a.any? { |e| e.class == String }
 => true
irb> h = { a: 1, b: 2 }
 => {:a=>1, :b=>2}
irb> h.any? { |k, v| v.odd? }
 => true
```

- [Ruby Doc - Enumerable#any?](https://ruby-doc.org/core-2.6.1/Enumerable.html#method-i-any-3F)

[⬆ Back to top](#30-seconds-of-ruby)

## Enumerable#one?

Passes each element of the collection to the given block. The method returns true if the block returns true exactly once. If the block is not given, `one?` will return true only if exactly one of the collection members is true.

```bash
irb> a = [500]
 => [500]
irb> a.one?
 => true
irb> a.one? { |e| e < 100 }
 => false
irb> (1..4).one? { |n| n % 2 == 0 }
 => false
```

#### Additional links

- [Ruby Doc - Enumerable#one?](https://ruby-doc.org/core-2.6.1/Enumerable.html#method-i-one-3F)

[⬆ Back to top](#30-seconds-of-ruby)

### Array#count

Ever wondered how much power Ruby's `count` method has? Besides counting the elements of an array, it can do pretty awesome things. So lets' start with the most common use case counting the elements of an array.

```bash
irb> numbers = [1,2,5,3,6,2,5,3]
 => [1, 2, 5, 3, 6, 2, 5, 3]
irb> numbers.count
 => 8
```

Let's say you want to count how often the number 3 is represented in the above array. The thought would be to use a loop an iterate over the array and increment a counter every time you see the number 3. But there is a better way. Just pass the object you looking for to the `count` method.

```bash
irb> numbers.count(3)
 => 2
```

Finally, you can also pass a block to do more complicated counts.

```bash
irb> numbers.count(&:even?)
 => 3
```

#### Additional links

- [Ruby Doc - Array#count](https://ruby-doc.org/core-2.2.0/Array.html#method-i-count)

[⬆ Back to top](#30-seconds-of-ruby)

### clone vs dup

Both methods are used to produce a shallow copy of obj—the instance variables of obj are copied, but not the objects they reference. `clone` copies the frozen and tainted state of obj whereas `dup` copies the tainted state of obj.

In general, clone and dup may have different semantics in the descendant classes. While clone is used to duplicate an object, including its internal state, dup typically uses the class of the descendant object to create the new instance. When using dup, any modules that the object has been extended with will not be copied.

```bash
irb> array = ['a','b','c']
 => ["a", "b", "c"]
irb> array.freeze
 => ["a", "b", "c"]
irb> array_clone = array.clone
 => ["a", "b", "c"]
irb> a_clone << "d"
RuntimeError: cant modify frozen Array
irb> array_dup = array.dup
 => ["a", "b", "c"]
irb> a_dup << "d"
 => ["a", "b", "c", "d"]
```

#### Additional links

- [Ruby Doc - #clone](https://ruby-doc.org/core-2.0.0/Object.html#method-i-clone)
- [Ruby Doc - #dup](https://ruby-doc.org/core-2.6.1/Object.html#method-i-dup)

[⬆ Back to top](#30-seconds-of-ruby)

### Hash#fetch

Returns a value from the hash for the given key. If the key can't be found, there are several options:

- will raise a KeyError exception when no arguments given
- if a default is given, then that will be returned
- if the optional code block is specified, then that will be run and its result returned.

```bash
irb> user = {'first_name': 'Dummy', 'last_name': 'User'}
 => {:first_name=>"Dummy", :last_name=>"User"}
irb> user.fetch(:first_name)
 => "Dummy"
irb> user.fetch(:email)
KeyError: key not found: :email
  from (irb):5:in `fetch'
irb> user.fetch(:email, 'no email added')
 => "no email added"
irb> user.fetch(:email){ |e| "no #{e} added"}
 => "no email added"
```

#### Additional links

- [Ruby Doc - Hash#fetch](https://ruby-doc.org/core-2.2.0/Hash.html#method-i-fetch)

[⬆ Back to top](#30-seconds-of-ruby)

### Array#zip

Converts any arguments to arrays, then merges elements of self with corresponding elements from each argument.

This generates a sequence of ary.size n-element arrays, where n is one more than the count of arguments.

If the size of any argument is less than the size of the initial array, nil values are supplied.

If a block is given, it is invoked for each output array, otherwise an array of arrays is returned.

```bash
irb> first_names = ['George', 'Marcus', 'Brian']
 => ["George", "Marcus", "Brian"]
irb> last_names = ['Massy', 'Windmil']
 => ["Massy", "Windmil"]
irb> first_names.zip(last_names)
 => [["George", "Massy"], ["Marcus", "Windmil"], ["Brian", nil]]
```

#### Additional links

- [Ruby Doc - Array#zip](https://ruby-doc.org/core-2.2.0/Array.html#method-i-zip)

[⬆ Back to top](#30-seconds-of-ruby)

### Adding uniq values to an array

Let's say we wanna add a new element to an array but we want to make sure to keep each element uniq. One way to achive this would be:

```bash
irb> alphabet = ['a','b','c']
 => ["a", "b", "c"]
irb> alphabet << 'c'
 => ["a", "b", "c", "c"]
irb> alphabet.uniq
 => ["a", "b", "c"]
```

Luckily Ruby offers Bitwise OR operator:

```ruby
x |= y
is shorthand for:
x = x | y
```

So our example from above would become:

```bash
irb> alphabet = ['a','b','c']
 => ["a", "b", "c"]
irb> alphabet | ['c']
 => ["a", "b", "c"]
```

We can also assign more than one element at the same time:

```bash
irb> alphabet = ['a','b','c']
 => ["a", "b", "c"]
irb> alphabet | ['c','d']
 => ["a", "b", "c", "d"]
```

[⬆ Back to top](#30-seconds-of-ruby)

### Ruby's Benchmark

The Benchmark module provides methods to measure and report the time used to execute Ruby code. This report shows the user CPU time, system CPU time, the sum of the user and system CPU times, and the elapsed real time. The unit of time is seconds. Consider the following example:

```ruby
require 'benchmark'
N = 1_000_000
puts RUBY_DESCRIPTION
Benchmark.bm(15, "concat/append") do |bm|
  concat_report = bm.report("concat") { N.times { 'Hello' +  ' ' +  'World' } }
  append_report = bm.report("append") { N.times { 'Hello' <<  ' ' <<  'World' } }
  [concat_report / append_report]
end
```

```bash
~/: ruby concat_append_benchmark.rb
ruby 2.4.4p296 (2018-03-28 revision 63013) [x86_64-darwin17]
                      user     system      total        real
concat            0.290000   0.000000   0.290000 (  0.608981)
append            0.260000   0.000000   0.260000 (  0.362523)
rescue/condition  1.115385        NaN        NaN (  1.679841)
```

#### Additional links

- [Benchmark](https://ruby-doc.org/stdlib-2.5.0/libdoc/benchmark/rdoc/Benchmark.html)

[⬆ Back to top](#30-seconds-of-ruby)

### Ruby's logger class

The Ruby Logger class gives you a way to generate logs with a default output format & different levels of importance.

```ruby
  logger = Logger.new("my_log_file.txt")
```

For logging to the terminal just pass `STDOUT`.

```ruby
  logger = Logger.new(STDOUT)
```

Logger levels are:

- **UNKNOWN:** An unknown message that should always be logged.

- **FATAL:** An unhandleable error that results in a program crash.

- **ERROR:** A handleable error condition.

- **WARN:** A warning.

- **INFO:** Generic (useful) information about system operation.

- **DEBUG:** Low-level information for developers.

Default log format is:

```bash
SeverityID, [DateTime pid] SeverityLabel -- ProgName: message
```

For instance:

```bash
I, [1999-03-03T02:34:24.895701 19074]  INFO -- Main: info.
```

#### Additional links

- [Ruby Doc - Logger](https://ruby-doc.org/stdlib-2.4.0/libdoc/logger/rdoc/Logger.html)

[⬆ Back to top](#30-seconds-of-ruby)

### to_h vs. to_hash

`to_h` is an explicit casting helper and is used to transform a value from one type to another. `to_hash` is an implicit casting helper
with the same purpose. The difference is that the former will always return a string whereas the later will result in an error or data loss
if the value it acts on does not act like the type we are casting. Ruby will only return a value when objects act like the type.
Ruby is very strict when using an implicit casting helper to ensure that the value acts like the type we want.

```bash
irb > rue.to_s
 => "true"
irb > true.to_str
=> NoMethodError: undefined method `to_str' for true:TrueClass
Did you mean?  to_s
```

[⬆ Back to top](#30-seconds-of-ruby)

### Ruby from CMD (Command Line)

Ever wondered how you can use ruby code in the command line?

Running a ruby file from CMD:upcase

```bash
~/: ruby myprogram.rb
```

You can pass in code as a command-line argument to the **ruby** command...

```bash
~/: ruby -e "puts 'Hello World!'"
~/: Hello World!
```

and you have accss to the ARGV array to process additional passed arguments.

```bash
~/: ruby -e 'puts ARGV.inspect' 1 2 3 4
["1", "2", "3", "4"]
```

It is also possible to use the pipe command to execute ruby code.

```bash
~/: echo "puts 'Hello World!'" | ruby
~/: Hello World!
```

[⬆ Back to top](#30-seconds-of-ruby)

### Append only uniq elements to array

You an call `.uniq` on the array after appending all elements. This will remove all elemnts that occure more than once in the array.

```bash
irb> array = []
=> []
irb> array << 1
=> [1]
irb> array << 2
=> [1, 2]
irb> array << 1
=> [1, 2, 1]
irb> array.uniq
=> [1, 2]
```

An ohter way is to only append an element if the array does not contain it already by using the **'|'**.

```bash
irb> array = []
=> []
irb> array << 1
=> [1]
irb> array << 2
=> [1, 2]
irb> array | [1]
=> [1, 2]
irb> array
=> [1, 2]
```

[⬆ Back to top](#30-seconds-of-ruby)
