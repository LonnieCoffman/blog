---
layout: post
date: 2016-11-03 14:05
title: "Benchmarking Ruby Code Using Benchmark and Benchmark-ips"
description: How to benchmark Ruby code using the benchmark module and the benchmark-ips Ruby gem.
comments: true
category:
- how-to
tags:
- ruby
- how-to
---
<figure class="alignleft">
	<img src="{{ site.image }}benchmark.png" width="120"/>
</figure>
In Ruby there are many ways of writing code to accomplish the same thing. Some
are one liners while others are rather verbose. While choosing one over the other
may simply be a matter of personal preference, I am of the belief that faster
execution should also be a factor. The Benchmark module and the benchmark-ips
gem can provide performance data of code execution times.

### Ruby's Benchmark Module
The [benchmark module](https://ruby-doc.org/stdlib-2.3.1/libdoc/benchmark/rdoc/Benchmark.html)
from the Ruby Standard Library measures the time that it
takes to execute a specific section of code.  it generates data in seconds in
the following format:
{% highlight text %}
user       system     total     real
0.970000   0.000000   0.970000 (  0.970493)
{% endhighlight %}
* <code>user = User CPU Time</code> - the time spent processing your code
* <code>system = System CPU Time</code> - the time spent kernel code such as system calls.
* <code>total = Total CPU Time</code> - User CPU Time + System CPU Time
* <code>real = Real Time</code> - the actual time that execution took

### Testing with The Benchmark Module
I have been working through the 101-109 Small Problems section of [Launch School](https://launchschool.com)
in preparation for my first assessment and recently wrote a solution to the
'Sum of Digits' problem. This problem involved taking a positive integer and
returning a sum of its digits. When I wrote my solution I did not think of using
the reduce method as in the solution provided by Launch School. Using the code
below I am going to test four different solutions. Solution one is the provided
solution, number two is mine and three and four are from two random students. We
are going to measure the time it takes to call each method one million times.

{% highlight ruby linenos%}
require 'benchmark'

# solution 1
def sum(num)
  num.to_s.chars.map(&:to_i).inject(:+)
end

# solution 2
def sum_1(num)
  total = 0
  num.to_s.chars{ |n| total += n.to_i }
  total
end

# solution 3
def sum_2(int)
  sum = 0
  int.to_s.chars.each do |digit|
    sum += digit.to_i
  end
  sum
end

# solution 4
def sum_3(int)
  total = int.to_s.split('').reduce do |sum , num|
          sum.to_i + num.to_i
  end
end

Benchmark.bmbm do |test|
  test.report('Solution 1:') do
    1_000_000.times{ sum(123_456_789) }
  end

  test.report('Solution 2:') do
    1_000_000.times{ sum_1(123_456_789) }
  end

  test.report('Solution 3:') do
    1_000_000.times{ sum_2(123_456_789) }
  end

  test.report('Solution 4:') do
    1_000_000.times{ sum_3(123_456_789) }
  end
end
{% endhighlight %}
In the code above we used the [Benchmark#bmbm](https://ruby-doc.org/stdlib-2.3.1/libdoc/benchmark/rdoc/Benchmark.html#method-c-bmbm) method in order to avoid any garbage
collection overhead and get the runtime environment stable.  This is done by running
two passes, the first being a rehearsal. Each block is run one million times in order
to get enough iterations to compare data.  Executing the code above we get the following:
{% highlight text %}
Rehearsal -----------------------------------------------
Solution 1:   2.270000   0.000000   2.270000 (  2.267960)
Solution 2:   1.420000   0.000000   1.420000 (  1.418441)
Solution 3:   1.710000   0.000000   1.710000 (  1.713566)
Solution 4:   5.560000   0.010000   5.570000 (  5.571037)
------------------------------------- total: 10.970000sec

                  user     system      total        real
Solution 1:   2.230000   0.000000   2.230000 (  2.237467)
Solution 2:   1.430000   0.000000   1.430000 (  1.433155)
Solution 3:   1.690000   0.000000   1.690000 (  1.700853)
Solution 4:   5.640000   0.000000   5.640000 (  5.653556)
{% endhighlight %}

The data above provides some basic information about execution time, but offers
no built in way of comparing the data.

### More Informative Results With The Benchmark-ips Gem

In using the Benchmark module I had to choose an iteration value that would provide
enough information for comparison and then visually compare the results.  Using
the [benchmark-ips gem](https://github.com/evanphx/benchmark-ips) we can garner more information and do not have to guess
the number of iterations that would provide relevancy. This gem measures iterations
per second and then provides a comparison of the results.  Here is the same test
using benchmark-ips.

{% highlight ruby linenos%}
require 'benchmark/ips'

# solution 1
def sum(num)
  num.to_s.chars.map(&:to_i).inject(:+)
end

# solution 2
def sum_1(num)
  total = 0
  num.to_s.chars{ |n| total += n.to_i }
  total
end

# solution 3
def sum_2(int)
  sum = 0
  int.to_s.chars.each do |digit|
    sum += digit.to_i
  end
  sum
end

# solution 4
def sum_3(int)
  total = int.to_s.split('').reduce do |sum , num|
          sum.to_i + num.to_i
  end
end

Benchmark.ips do |test|
  test.report('Solution 1:') do
    sum(123_456_789)
  end

  test.report('Solution 2:') do
    sum_1(123_456_789)
  end

  test.report('Solution 3:') do
    sum_2(123_456_789)
  end

  test.report('Solution 4:') do
    sum_3(123_456_789)
  end

  test.compare!
end
{% endhighlight %}

Here are the benchmark results.

{% highlight text %}
Warming up --------------------------------------
         Solution 1:    39.555k i/100ms
         Solution 2:    60.691k i/100ms
         Solution 3:    50.504k i/100ms
         Solution 4:    17.079k i/100ms
Calculating -------------------------------------
         Solution 1:    443.740k (± 3.5%) i/s -      2.255M in   5.086977s
         Solution 2:    679.129k (± 3.1%) i/s -      3.399M in   5.009052s
         Solution 3:    569.331k (± 4.0%) i/s -      2.879M in   5.064038s
         Solution 4:    176.084k (± 3.6%) i/s -    888.108k in   5.049760s

Comparison:
         Solution 2::   679128.6 i/s
         Solution 3::   569331.1 i/s - 1.19x  slower
         Solution 1::   443740.2 i/s - 1.53x  slower
         Solution 4::   176084.2 i/s - 3.86x  slower
{% endhighlight %}

From the above information we can see the iterations per second and the solutions
ranked and compared.

### Final Thoughts
In Ruby and other programming languages there are many ways solve problems, with
the code choice being mainly a stylistic one.  On a small scale project these
choices have little, if any, impact on performance, but on larger projects with
a large user base these issues may cause unnecessary bottlenecks that can only
be discovered through benchmarking.
