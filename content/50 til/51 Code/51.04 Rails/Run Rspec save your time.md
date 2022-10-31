---
title: "🥦 Run Rspec save your time"
tags: [til, rails, rspec]
date: 2022-09-29
---

---

#til #rspec
	If you want to run rspec for a specific example, context or describe without having to care about path file, line number, you can try it:

```ruby
# spec/rails_helper.rb

RSpec.configure do |config|
  config.filter_run_when_matching focus: true
end
```
Then you add f to example, context or describe, Rspec will only focus it.

```ruby
#example
fit 'should tell height' do
  expect(@person.height).to eq(160)
end

# as well

it 'should tell height', focus: true do
  expect(@person.height).to eq(160)
end
```
p/s: you can add focus for multi examples
Ref: https://manny.codes/7-ways-to-selectively-run-rspec-tests/