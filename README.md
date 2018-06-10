# Intro

Jekyll Blog Theme "[EasyBook](https://github.com/laobubu/jekyll-theme-EasyBook/wiki)"

## Install

```
brew update && brew upgrade
brew doctor
```

```
brew install rbenv
brew install ruby-build
```

```
echo 'export RBENV_ROOT=/usr/local/var/rbenv' >> ~/.bash_profile
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
```

```
rvm install "ruby-2.5.0"
rvm use 2.5.0 --default
```

```
gem install jekyll bundler jekyll-gist jekyll-paginate jemoji
```

```
bundle exec jekyll serve
```