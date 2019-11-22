# Dcokerのオフィシャルrubyイメージとは?

author
:   Kazuhiro NISHIYAMA

content-source
:   Docker Meetup Kansai #5 (19.11)

date
:   2019/11/22

allotted-time
:   5m

theme
:   lightning-simple

# 自己紹介

- 西山 和広
- Ruby のコミッター
- twitter, github など: @znz

# OFFICIAL とは?

```
$ docker search ruby | head -n 8
NAME                   DESCRIPTION      STARS  OFFICIAL  AUTOMATED
ruby                   Ruby is a dyn…   1776   [OK]
circleci/ruby          Ruby is a dyn…   65
starefossen/ruby-node  Docker Image…    32               [OK]
heroku/ruby            Docker Image…    22               [OK]
bitnami/ruby           Bitnami Ruby     17               [OK]
rubylang/ruby          Experimental …   17
arm32v7/ruby           Ruby is a dyn…   9
iron/ruby              Tiny Ruby ima…   7
```

# OFFICIAL の image

- <https://github.com/docker-library/ruby>
- コミュニティによるメンテナンス
- Docker としてのオフィシャル
- alpine などにも対応

# rubylang の image

- <https://hub.docker.com/u/rubylang/>
- Ruby コミッターによるメンテナンス
- いくつか種類がある
  - rubylang/ruby
  - rubylang/all-ruby
  - rubylang/rubyfarm

# rubylang/ruby

- <https://hub.docker.com/r/rubylang/ruby/>
- bundler 周りなどの余計な環境変数を設定していない
  - OFFICIAL だと設定されている
- 主に特定 OS バージョンのみ
  - 今だと Ubuntu bionic
  - alpine などに対応する余裕がない

# ruby/ruby-docker-image

- <https://github.com/ruby/ruby-docker-images> (rubylang/ruby のソース)
- 元は iruby や pycall のテストのため
  - make install しただけのピュアな状態の Ruby
  - gem のテストで広く使えるから rubydata/ruby から移籍

# rubylang/all-ruby

- 全てのリリースバージョンの ruby を網羅したイメージ
- バージョン間の差などを調べるのに便利

# rubylang/all-ruby 使用例

```
$ docker run -it --rm rubylang/all-ruby \
  ./all-ruby -e 'print("hello")'
ruby-0.49             hello
...
ruby-2.7.0-preview1   hello
$ docker run -it --rm rubylang/all-ruby \
  env ALL_RUBY_SINCE=ruby-2.3 \
  ./all-ruby -e 'p :world'
ruby-2.3.0          :world
...
ruby-2.7.0-preview1 :world
```

# rubylang/rubyfarm

- bisect 用
- 開発版のほぼ全リビジョン
  - ビルドできないものなどがないだけ

# まとめ

- OFFICIAL が品質が高いとは限らない
- ソフトウェアの upstream も docker のエキスパートとは限らない
- rubylang には色々なイメージがあります
- 他のソフトウェアのイメージの状況も知りたいです
