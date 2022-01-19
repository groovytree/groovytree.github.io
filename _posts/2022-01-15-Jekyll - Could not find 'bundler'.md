---
layout: post
title: Jekyll Blog - Could not find 'bundler', GemNotFoundException
subtitle: 깃허브 블로그 서버구동시 에러
categories: Web
tags: [Web, Jekyll, Troubleshooting]
---

## Error 
```bash
>> bundle exec jekyll serve --trace 
Traceback (most recent call last):
	2: from /usr/bin/bundle:23:in `<main>'
	1: from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/rubygems.rb:302:in `activate_bin_path'
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/rubygems.rb:283:in `find_spec_for_exe': Could not find 'bundler' (2.2.31) required by your /Users/User_name/groovytree.github.io/Gemfile.lock. (Gem::GemNotFoundException)
To update to the latest version installed on your system, run `bundle update --bundler`.
To install the missing version, run `gem install bundler:2.2.31`
```

## Solution

```bash
gem install bundler:2.2.31
```

