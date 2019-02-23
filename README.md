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
