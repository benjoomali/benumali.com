---
title: Multi Faceted Search with PG_Search, Pagy and Rails 6
date: 2020-01-27
author: Ben Umali
description: So currently I'm building a custom theme in Wordpress that implements Vue with completely replacing the front end. Here's how I build a dropdown component in Vue...
tags: ['vuejs', 'wordpress']
---

In the process of creating a scoped search module for a freelance project, I ran into an issue with implementing PG_Search with Pagy. Basically, the concept was to build a Route Search function, where a user could search from location to location, with specific filters.

### PG_Search

Scopes in the my Stop Model

```
acts_as_list  scope:  :load

# associations
belongs_to  :load

#scopes
pg_search_scope  :route_search, against: [:city, :state, :zip]
scope  :first_in_position, -> { where(position:  1) }
```

Then in the controller:

```
#Store the from and to search queries
from_search = Stop.route_search(params[:from_query]).first_in_position.pluck(:load_id)
to_search = Stop.route_search(params[:to_query]).select{ |record| record  if  record.last?}.pluck(:load_id)
```

### Active Record Relations

It's always a good reminder to know the difference between an Array and Active Record Relation. I spent some time trying

### Pagy

Passing pg_search results into PAGY

### Intersection of Arrays

### Scopes

### Pluck
