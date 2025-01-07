---
title: Ruby 버전 업 후 오류
author: imbsh
date: 2025-01-07 22:36:00 +0900
categories: [IT, GIT, BLOG, RUBY]
tags: [ruby, error, blog, git, wdm, version, "0.1.1"]
pin: true
---

## 왜 문제가 발생했나요?
> 다른 PC에 git clone 후 로컬에서 테스트를 위해 ruby를 기존(3.2.4)보다 최근 버전(3.3.6)으로 설치했습니다. **jekyll serve** 명령 후 아래와 같은 오류가 발생했습니다.

```shell
C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:354:in raise_not_found!': Could not find gem 'wdm (~> 0.1.1) mingw, x64_mingw, mswin' in locally installed gems. (Bundler::GemNotFound)

The source contains the following gems matching 'wdm':
  * wdm-0.2.0
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:445:in block in prepare_dependencies'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:420:in each'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:420:in filter_map'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:420:in prepare_dependencies'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:64:in setup_solver'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/resolver.rb:29:in start'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/definition.rb:731:in start_resolution'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/definition.rb:341:in resolve'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/definition.rb:640:in materialize'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/definition.rb:232:in specs'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/definition.rb:299:in specs_for'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler/runtime.rb:18:in setup'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/bundler-2.6.2/lib/bundler.rb:167:in setup'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/jekyll-4.3.4/lib/jekyll/plugin_manager.rb:52:in require_from_bundler'
        from C:/Ruby33-x64/lib/ruby/gems/3.3.0/gems/jekyll-4.3.4/exe/jekyll:11:in <top (required)>'
        from C:/Ruby33-x64/bin/jekyll:36:in load'
        from C:/Ruby33-x64/bin/jekyll:36:in <main>'
```

## 어떤 문제인가요?
> 오류 메세지를 보시면 뭔가 wdm 버전 관련해서 뭐라고 하는 것 같죠? 저도 그렇게 생각했습니다. 찾아보니 ruby의 wdm이라는 gem 버전이 맞지 않아서라고 합니다.

## 어떻게 해결했을까요?
> 저의 경우 아래와 같이 Gemfile의 내용을 기존 0.1.1에서 0.2.0으로 수정 후 정상 작동을 확인했습니다.

```ruby
# (생략...)

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]

# (생략...)
```

> 감사합니다.