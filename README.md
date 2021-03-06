Stove
=====
[![Gem Version](http://img.shields.io/gem/v/stove.svg)][gem]
[![Build Status](http://img.shields.io/travis/sethvargo/stove.svg)][travis]
[![Dependency Status](http://img.shields.io/gemnasium/sethvargo/stove.svg)][gemnasium]
[![Code Climate](http://img.shields.io/codeclimate/github/sethvargo/stove.svg)][codeclimate]

[gem]: https://rubygems.org/gems/stove
[travis]: http://travis-ci.org/sethvargo/stove
[gemnasium]: https://gemnasium.com/sethvargo/stove
[codeclimate]: https://codeclimate.com/github/sethvargo/stove

A utility for releasing and managing Chef Cookbooks. It will:

- Tag and push a new release to git
- Upload the cookbook to a cookbook share (such as Supermarket)


Why?
----
Existing tools to package cookbooks (such as [Knife Community](https://github.com/miketheman/knife-community) and `knife cookbook site share`) require a dependency on Chef. Because of thier dependency on Chef, they enforce the use of a "cookbook repo". Especially with the evolution of [Berkshelf](https://github.com/RiotGames/berkshelf), cookbooks are individualized artifacts and are often contained in their own repositories. [stove](https://github.com/sethvargo/stove) is **cookbook-centric, rather than Chef-centric**.


Installation
------------
1. Add Stove to your project's Gemfile:

        gem 'stove'

2. Run the `bundle` command to install:

        $ bundle install --binstubs


Configuration
-------------
Stove requires your username and private key to upload a cookbook. You can pass these to each command call, or you can set them Stove:

```bash
$ stove login --username sethvargo --key ~/.chef/sethvargo.pem
```

These values will be saved in Stove's configuration file and persisted across your workstation.

The default publishing endpoint is the [Chef Supermarket](https://supermarket.getchef.com), but this is configurable. If you want to publish to an internal community site, you can specify the `--endpoint` value:

```bash
$ stove --endpoint https://internal-cookbook-store.example.com
```

or for a private supermarket using the [supermarket](https://supermarket.getchef.com/cookbooks/supermarket) cookbook:

```bash
$ stove --endpoint https://internal-cookbook-store.example.com/api/v1
```

Usage
-----
There are two ways to use Stove. You can either use the `stove` command directly or use the embedded rake task.

### Command
Execute the `stove` command from inside the root of a cookbook:

```bash
$ bin/stove
```

This will package (as a tarball) the cookbook in the current working directory, tag a new version, push to git, and publish to a cookbook share.

### Rake task
If you are familiar with the Bundler approach to publishing Ruby gems, this approach will feel very familiar. Simply add the following to your `Rakefile`:

```ruby
require 'stove/rake_task'
Stove::RakeTask.new
```

And then use rake to publish the cookbook:

```bash
$ bin/rake publish
```


Contributing
------------
1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


See Also
--------
- [Knife Community](https://github.com/miketheman/knife-community)
- [Emeril](https://github.com/fnichol/emeril)


License & Authors
-----------------
- Author: Seth Vargo (sethvargo@gmail.com)

```text
Copyright 2013-2014 Seth Vargo <sethvargo@gmail.com>
Copyright 2013-2014 Chef Software, Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
