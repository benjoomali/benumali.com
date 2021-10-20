---
title: Sort Records by Total Number of Associations in Rails
date: 2021-08-14
author: Ben Umali
description: Sort records by the total number of has_many associations.
tags: ['rails', 'left outer join', 'ruby']
---

## Sorting Records by Total Number of Has_Many Associations

#### August 14, 2021

Needed to be able to sort an index of records by the total number of has_many associations that existed on the record.

I originally wrote this scope:

```ruby
class Carrier < ApplicationRecord
	has_many :loads, through: :dispatches

	scope :by_total_loads, -> {joins(:loads).group(:id).order('COUNT(loads.id) DESC')}
end
```

However, this would only return the Carriers with 1 or more associations.

Then, in Rails 5, left outer joins was introduced. A left outer join gets all the rows from the tables where the join conditions are met, while also leaving in the unmatched rows. That way, we could sort the index by number of total associations, and leave the 0 association records at the end!

### Left Outer Joins in Rails 5

```ruby
scope :by_total_loads, -> {left_joins(:loads).group(:id).order('COUNT(loads.id) DESC')}
```

I totally abstracted this, but this article was very helpful in understanding. [https://www.ananunesdasilva.com/posts/understanding-activerecord-left-outer-joins](https://www.ananunesdasilva.com/posts/understanding-activerecord-left-outer-joins)
