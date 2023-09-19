---
title: "🌱 Splat in ruby"
tags: [til, ruby]
date: 2022-11-16
---

- 🌱 Splat array in ruby with syntax below:

```rb
array = [1,2,3]
splat_array = [*array, 4, 5] # => [1,2,3,4,5]
```

- 🌱 Splat hash in ruby with syntax below:

```rb
hash = {a: 1, b: 2}
splat_hash = { **hash, c: 3} # => {:a=>1, :b=>2, :c=>3}
```