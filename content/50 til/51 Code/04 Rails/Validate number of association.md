---
title: "🌱 Validate number of association"
tags: [til, rails]
date: 2022-09-29
---

### 🌿 What?
- 🌱 If you have a People model and a Vehicle model, every people has_many vehicles but you want to set maximum for number of vehicles which a people can has. You can use following command below:

```ruby
# vehicle.rb
class Vehicle
  belongs_to :people
end

# people.rb
class People
  has_many :vehicles

  validates :vehicles, length: { maximum: 2 }
end
```

### 🌿 Refer
https://til.hashrocket.com/posts/egegrgsdnj-limiting-object-counts-in-rails-associations-
