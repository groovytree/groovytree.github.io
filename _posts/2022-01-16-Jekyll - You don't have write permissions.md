---
layout: post
title: Jekyll Blog - You don't have write permissions for the /Library/Ruby/.. directory
subtitle: 깃허브 블로그 서버구동시 에러
categories: Web
tags: [Troubleshooting, Jekyll]
---

## Error

```bash
>> gem install bundler:2.2.31
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory.
```

## Solutions

```bash
sudo gem install bundler:2.2.31
```

```bash
gem install bundler
vim ~/.zshrc

[[ -d ~/.rbenv ]] &&
export PATH=${HOME}/.rbenv/bin:${PATH} &&
eval "$(rbenv init -)"

source ~/.zshrc
```

