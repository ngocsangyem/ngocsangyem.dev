---
layout: post
title: "Set up Jekyll environment on macOS"
category: logs
description: Set Ruby, Bundler and Jekyll on macOS Silicon
tags: jekyll tips
---

This guide is for macOS Catalina and is based on the [Jekyll on macOS] doc and my experience.

* this ordered seed list will be replaced by the toc
{:toc}

## Install dev tools

Use the [XCode] CLI to install dev tools. Recommended so that you can install native extensions when installing gems.

```bash
xcode-select --install
```

## Install homebrew

> Think of Homebrew as an app store for the command line. Everything you install for Jekyll will be free and open source.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Note**: be sure to replace [username] with the username you use on your Mac.

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/[yourusername]/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
export SDKROOT=$(xcrun --show-sdk-path)
```

## Install Ruby

You can see the version of Ruby pre-installed with your Mac, by typing:

```bash
ruby -v
```

Your system already has a Ruby installed, but its version and gems are locked in Catalina. So here we install another Ruby using Homebrew.

```bash
brew install ruby
```

### Ruby configuration path

Type:

```bash
echo $SHELL
```

The result will be `zsh` or `bash`.

For zsh, type:

```bash
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
```

For bash, type:

```bash
echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile
```

X.X.0 is the version of Ruby you installed with Homebrew or open /Users/[yourusername]/.gem/ruby to check out the folder version you have installed.

Type:

```bash
exit
```

Quit terminal

Run terminal again and type:

```bash
ruby -v
```

You will see the version of Ruby has updated.

## Install Jekyll and Bundler

Type:

```bash
gem install --user-install bundler jekyll
```

```bash
echo $SHELL
```

For zsh, type:

```bash
echo 'export PATH="$HOME/.gem/ruby/[ruby_latest_version_folder_name]/bin:$PATH"' >> ~/.zshrc
```

For bash, type:

```bash
echo 'export PATH="$HOME/.gem/ruby/[ruby_latest_version_folder_name]/bin:$PATH"' >> ~/.bash_profile
```

Type:

```bash
gem env
```

Look for the "GEM PATHS" section and make sure they all refer to your latest Ruby version folder.

## Other issues

### libffi or ffi_c missing

If you run into issues installing or running because of libffi or ffi_c missing, you can try these:

```bash
brew install libffi

gem install ffi --user-install
# Or
sudo gem install ffi
```

### Could not open library 'glib-2.0.0'

```bash
brew install vips
```

[Jekyll on macOS]: https://jekyll.readthedocs.io/en/latest/installation/macos.html
[XCode]: https://developer.apple.com/xcode/