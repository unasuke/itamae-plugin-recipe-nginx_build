# Itamae::Plugin::Recipe::NginxBuild

Itamae recipe plugin for nginx-build

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'itamae-plugin-recipe-nginx_build'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install itamae-plugin-recipe-nginx_build

## Usage

### Install

```ruby
%w(
  git
  gcc
  openssl-devel
  ImageMagick-devel # ngx_small_light optional
).each do |pkg|
  package pkg
end

include_recipe "nginx_build"
include_recipe "nginx_build::install"
```

### Option

all parameter is optional.

```yaml
server:
  user: ec2-user
nginx_build:
  build_user: ec2-user
  platform: linux ( or darwin )
  version: 0.6.4
  bin: /usr/local/bin/
  nginx_version: 1.8.0
  nginx_user: nginx
  nginx_group: nginx
  nginx_sbin: /usr/sbin/nginx
  nginx_conf: /etc/nginx/nginx.conf
  nginx_pid: /var/run/nginx.pid
  modules:
    - http_ssl_module
  modules3rds:
    -
      name: ngx_cache_purge
      form: git
      url: https://github.com/FRiCKLE/ngx_cache_purge.git
      rev: 2.3
    -
      name: ngx_small_light
      form: git
      url: https://github.com/cubicdaiya/ngx_small_light.git
      rev: v0.6.15
      shprov: ./setup
  configure_path: /usr/local/nginx_build/configure.sh
  modules3rd_path: /usr/local/nginx_build/modules3rd.ini
  configure_options:
    prefix: /etc/nginx
    error-log-path: /var/log/nginx/error.log
    http-log-path: /var/log/nginx/access.log

```

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/zaru/itamae-plugin-recipe-nginx_build.
