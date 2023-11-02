---
layout: post
title: Jekyll Blog - can't find gem bundler
subtitle: 깃허브 블로그 서버구동시 에러
categories: Web
tags: [Troubleshooting, Jekyll]
---

## Error

```bash
>> bundle exec jekyll serve --trace
Traceback (most recent call last):
        2: from /usr/bin/bundle:23:in `<main>'
        1: from /Library/Ruby/Site/2.6.0/rubygems.rb:284:in `activate_bin_path'
/Library/Ruby/Site/2.6.0/rubygems.rb:265:in `find_spec_for_exe': can't find gem bundler (>= 0.a) w
```

## Solutions
```bash
rm Gemfile.lock
bundle install
```

