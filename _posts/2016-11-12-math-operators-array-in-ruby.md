---
layout: post
date: 2016-11-12 10:48
title: "Storing Math Operators in an Array or Hash"
description: In Ruby math operators are method calls because of this we can store math operators as symbols in an array or hash and loop through them.
comments: true
category:
- ruby
tags:
- ruby
- how-to
---
<figure class="alignleft">
	<img src="{{ site.image }}ruby_math.png" width="120"/>
</figure>
I was recently doing an exercise that involved performing multiple math operations on
a set of numbers and thought that rather than executing each operation on it's own
line of code wouldn't it be simpler to store the operators in an array and then
execute them one by one.  Here is what I learned.

### In Ruby math operators are methods
In Ruby math is basically invoking a method (the math operator) on two objects (the operands).
This can be demonstrated by the following in IRB:

{% highlight text %}
2.3.0 :001 > 2 + 3
 => 5
2.3.0 :002 > 2.+(3)
 => 5
{% endhighlight %}

The same is true for comparison and other operators

{% highlight text %}
2.3.0 :001 > 2.==(3)
 => false
2.3.0 :002 > 2.<(3)
 => true
{% endhighlight %}

### Using the send method we can iterate through each operation
The [send method](http://devdocs.io/ruby~2.3/object#method-i-send) "Invokes the
method identified by symbol, passing it any arguments specified." This means that
we can store each operation method as a symbol in an array or hash and invoke them
one by one through iteration.  Here is an example:

{% highlight ruby linenos %}
def calculate(num1, num2)
  operators = [:+, :-, :*, :/, :%, :**, :!=]
  operators.each do |op|
    puts "==> #{num1} #{op} #{num2} = #{num1.send(op, num2)}"
  end
end

calculate(13, 21)
{% endhighlight %}

Here is the output:

{% highlight text %}
==> 13 + 21 = 34
==> 13 - 21 = -8
==> 13 * 21 = 273
==> 13 / 21 = 0
==> 13 % 21 = 13
==> 13 ** 21 = 247064529073450392704413
==> 13 != 21 = true
{% endhighlight %}

### Takeaways
* math operators in Ruby are methods
* method names can be stored as symbols
* the send method can invoke methods identified by symbols
