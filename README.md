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
