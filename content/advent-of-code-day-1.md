---
title: Advent of Code Day 1
date: 2021-12-01
author: Ben Umali
description: A little Ruby to solve the Advent of Code challenge for 2021.
tags: ['aoc', '2021', 'ruby']
---

### Sonar Sweep

This one was fun. We use the `.each_cons` enumerable method in Ruby to handle most of the work.

```ruby
arr = [199, 200, 208, 210, 200, 207, 240, 269, 260, 263]
# is the consecutive number an increase? If so return the amount of times the array increases. Answer: 7 times
```

"Given an array, count the number of times a depth measurement increases from the previous measurement. "

```ruby
iterator = 0
# Iterate over an array, comparing two consecutive values. If the condition of the scond value is greater than the first, then increase the iterator amount!
array.map(&:to_i).each_cons(2) {|first, second| iterator += 1 if second > first}
puts iterator
```

As this is my first time doing Advent of Code, I wrote a really rough few lines to get the answer.

### Part 2

Now to do it with three-measurements! Goal for this part was to return the number of times the sum of measurements in the "three measurement sliding window" increases.

```ruby
new_arr = []
# Store objects/arrays in triplets in a new array
array.map(&:to_i).each_cons(3) {|num| new_arr.push(num) }

# Then like before, compare the sums of the first set to the second set
new_arr.each_cons(2) { |first, second| iterator += 1 if second.sum > first.sum}
puts iterator
```

Similar idea to the first part, however I generated a new array from the "triple measurements" and iterated over those sums.
