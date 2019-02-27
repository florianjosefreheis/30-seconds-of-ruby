![RubyLogo](/ruby_logo.png)

# 30 Seconds of Ruby

Ruby snippets you can understand in 30 seconds or less.

Inspired by [30-seconds-of-knowledge](https://github.com/petrovicstefanrs/30_seconds_of_knowledge/).

<hr></hr>

### Ruby's Ancestor Chain

Always wondered how to see Ruby's class hierarchy? Simply call `ancestors` on a class to see the ancestor chain.

The return array contains the following order:

* the calling class
* its included modules
* its parent class
* the included modules of its parents class
* the parent class of its parent class

Here is the ancestor chain of the String class:

``` ruby
irb> String.ancestors
=> [String, Comparable, Object, Kernel, BasicObject]
```

##### Additional links

* [Ruby Doc - Ancestors](https://ruby-doc.org/core-2.6.1/Module.html#method-i-ancestors)

[⬆ Back to top](#30-seconds-of-ruby)

### What is a Ruby Interpreter?

A Ruby interpreter is any program that parses the Ruby source code to imitate its behavioral execution. It converts the program line by line compared to a compiler which converts the whole program at once. Hence, a code change only requires an edit. Interpreters only throw an error if the program gets executed and reach the line that containes the error, whereas compilers will throw the error already before execution.
There are multiple versions of Ruby interpreters to choose from, each with a different but very similar set of rules and options.

Common Ruby Interpreters:

* Ruby MRI
* JRuby
* YARV
* Rubinius

[⬆ Back to top](#30-seconds-of-ruby)

### Ruby's .methods method

If you've ever wondering what methods are available for a specific object, just call `.methods` on it:

``` bash
irb> name = 'Bob'
 => "Bob"
irb> name.methods
 => [:include?, :%, :unicode_normalize, :*, :+, :to_c, ...]
 ```

This will return an array of symbols (names) of all publicly accessible methods of the object and its ancestors.

[⬆ Back to top](#30-seconds-of-ruby)

### BasicObject

The BasicObject class is the top parent of all class. It is a blank instance of class `class` with no superclass and contains a minimum of methods for object creation and comparison.

``` bash
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

##### Additional links

* [Ruby Doc - BasicObject](https://ruby-doc.org/core-1.9.3/BasicObject.html)

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

##### Additional links

* [Ruby Doc - Hash#dig](https://ruby-doc.org/core-2.3.0_preview1/Hash.html#method-i-dig)

[⬆ Back to top](#30-seconds-of-ruby)

### Mehtod Naming Conventions "!" vs. "?"

In Ruby there are two common naming conventions for methods. Either you end a method name with a **!** or **?**.
Methods ended by a **!** are called bang methods and often modifies the original object.

``` bash
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

[⬆ Back to top](#30-seconds-of-ruby)

### Kernel (module)

The Kernel module is included by class Object and provides methods that are globally available, hence every Ruby object has access to them. These methods are called without a receiver and only act on the passed arguments.

Famouse representative of the Kernel module are:

* Array
* Hash
* Integer
* Hash
* p, print and puts

##### Additional links

* [Ruby Doc - Kernel](https://ruby-doc.org/core-2.6.1/Kernel.html)

[⬆ Back to top](#30-seconds-of-ruby)

### Where do methods live?

Ever wondered how you can find out where exactly a method lives inside Ruby?

Ruby offers two helpful methods here. By passing the name of the method as a symbol to `owner` will reveal where a method lives inside Ruby. If you curious about who receives s specific method, just pass the name again as a symbol to `receiver`.

``` bash
irb> method(:initialize).owner
 => BasicObject
irb> method(:initialize).receiver
 => main
```

##### Additional links

* [Ruby Doc - owner](https://apidock.com/ruby/v1_9_3_392/Method/owner)
* [Ruby Doc - receiver](https://apidock.com/ruby/v1_9_3_392/Method/receiver)

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

 ##### Additional links

* [Ruby Doc - Integer#digits](https://ruby-doc.org/core-2.4.0/Integer.html#method-i-digits)

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

 ##### Additional links

* [Ruby Doc - Array#values_at](https://apidock.com/ruby/Array/values_at)
* [Ruby Doc - Hash#values_at](https://apidock.com/ruby/Hash/values_at)

[⬆ Back to top](#30-seconds-of-ruby)
