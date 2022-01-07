---
title: Advent of Code Day 2
date: 2021-12-03
author: Ben Umali
description: Solving the Dive! question with ruby.
tags: ['aoc', '2021', 'ruby']
---

### Dive!

#### Part 1

Wrote a rough solution to solve this one. It involves taking the input data, splitting it, then iterating over the new split values and updating the position.

```ruby
def submarine_position(arr)
  position = Hash[x: 0, y: 0]

  new_array = []
  arr.each {|input| new_array.push(input.split(" "))}

  new_array.each do |n|
    case n[0]
    when "forward"
      position[:x] += n[1].to_i
    when "down"
      position[:y] += n[1].to_i
    when "up"
      position[:y] -= n[1].to_i
    else
      puts "error"
    end
  end

  return position
end

```

From there you can multiply the values in the position hash to get the solution.

#### Part 2

I misread the prompt on this part on my first attempt!

Turns out that the depth and position of the submarine no longer changes when "down" or "up" they just affect the aim of the submarine.

```ruby
def submarine_position(arr)
  position = Hash[x: 0, y: 0, aim: 0]

  new_array = []
  arr.each {|input| new_array.push(input.split(" "))}

  new_array.each do |n|
    case n[0]
    when "forward"
      position[:x] += n[1].to_i
      position[:y] += (position[:aim] * n[1].to_i)
      puts "X #{position[:x]}, Y #{position[:y]}, Aim #{position[:aim]}"
    when "down"
      position[:aim] += n[1].to_i
      puts "X #{position[:x]}, Y #{position[:y]}, Aim #{position[:aim]}"
    when "up"
      position[:aim] -= n[1].to_i
      puts "X #{position[:x]}, Y #{position[:y]}, Aim #{position[:aim]}"
    else
      puts "error"
    end
  end

  return position
end

```
