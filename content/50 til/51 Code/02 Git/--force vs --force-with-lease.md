---
title: "🌱 --force vs --force-with-lease"
tags: [til, git]
date: 2023-05-26
alias: [--force-with-lease, --force]
---

## 🌿 --force
- `push --force`: luôn ghi đè lên remote branch theo trạng thái commit của local branch.

```
remote brach: --cm1--cm2--cm3
		                \
			             -- cm4 -> push --force
remote branch: --cm1--cm2--cm4
```

## 🌿 --force-with-lease
- `push --force-with-lease`: chỉ ghi đè khi remote branch **không có commit mới** so với local branch.

```
remote brach: --cm1--cm2--cm3
		                \
			             -- cm4 -> push --force-with-lease
-> Error, remote brach: --cm1--cm2--cm3

-----------------------------------------------------

remote brach: --cm1--cm2--cm3
			                \
				             -- cm4 -> push --force-with-lease
remote brach: --cm1--cm2--cm3--cm4

```

- Option này tránh việc ghi đè commit của người khác(trong trường hợp một nhánh có nhiều người cùng contribute). Khi có commit mới trên remote branch, chúng ta cần phải pull về và rebase trước thì mới push đươc lên remote branch.

- 🌱 Refer: https://stackoverflow.com/questions/59309402/is-git-push-force-with-lease-always-safe