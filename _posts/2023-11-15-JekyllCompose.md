---
title: Jekyll::Compose
author: Su Yu
date: 2023-11-15 11:54:00 +0800
categories: [Jekyll, Compose]
tags: [plug-in]
render_with_liquid: false
---

# Jekyll::Compose

Streamline your writing in Jekyll with some commands.

通过一些命令简化你在Jekyll中的写作。

[![Linux Build Status](https://img.shields.io/travis/jekyll/jekyll-compose/master.svg?label=Linux%20build)](https://travis-ci.org/jekyll/jekyll-compose)
[![Windows Build status](https://img.shields.io/appveyor/ci/jekyll/jekyll-compose/master.svg?label=Windows%20build)](https://ci.appveyor.com/project/jekyll/jekyll-compose)

## Installation

Add this line to your application's Gemfile:

将此行添加到应用程序的Gemfile中：

```undefined
gem 'jekyll-compose', group: [:jekyll_plugins]
```

And then execute:

然后执行：

```undefined
$ bundle
```

## Usage 使用

After you have installed (see above), run `bundle exec jekyll help` and you should see:

安装后（见上文），运行“bundle exec jekyll help”，您应该会看到：

Listed in help you will see new commands available to you:

在帮助中列出，您将看到可用的新命令：

```sh
  draft      # Creates a new draft post with the given NAME
  # 用给定的NAME创建一个新的草稿帖子
  post       # Creates a new post with the given NAME
  # 用给定的NAME创建一个新的post
  publish    # Moves a draft into the _posts directory and sets the date
  # 将草稿移到_posts目录并设置日期
  unpublish  # Moves a post back into the _drafts directory
  # 将帖子移回_drafts目录
  page       # Creates a new page with the given NAME
  # 使用给定的NAME创建新页面
  rename     # Moves a draft to a given NAME and sets the title
  # 将草稿移动到给定的NAME并设置标题
  compose    # Creates a new file with the given NAME
  # 用给定的NAME创建一个新文件
```

Create your new page using:

使用以下内容创建新页面：

```sh
    $ bundle exec jekyll page "My New Page"
```

Create your new post using:

使用以下内容创建新帖子：

```sh
    $ bundle exec jekyll post "My New Post"
    # or specify a custom format for the date attribute in the yaml front matter
    # 或者为yaml前端事务中的date属性指定自定义格式
    $ bundle exec jekyll post "My New Post" --timestamp-format "%Y-%m-%d %H:%M:%S %z"
    # or by using the compose command
    # 或使用compose命令
    $ bundle exec jekyll compose "My New Post"
    # or by using the compose command with post specified
    # 或者使用compose命令指定post
    $ bundle exec jekyll compose "My New Post" --post
    # or by using the compose command with the posts collection specified
    # 或者通过使用指定posts集合的compose命令
    $ bundle exec jekyll compose "My New Post" --collection "posts"
```

Create your new draft using:

使用以下内容创建新草稿：

```sh
    $ bundle exec jekyll draft "My new draft"
    # or by using the compose command with draft specified
    # 或者通过使用指定草稿的compose命令
    $ bundle exec jekyll compose "My new draft" --draft
    # or by using the compose command with the drafts collection specified
    # 或者使用指定草稿集合的compose命令
    $ bundle exec jekyll compose "My new draft" --collection "drafts"
```

Rename your draft using:

使用以下方法重命名草稿：

```sh
$ bundle exec jekyll rename _drafts/my-new-draft.md "My Renamed Draft"
# or rename it back
# 或者重新命名
$ bundle exec jekyll rename _drafts/my-renamed-draft.md "My new draft"
```

Publish your draft using:

发布草稿时使用：

```sh
    $ bundle exec jekyll publish _drafts/my-new-draft.md
    # or specify a specific date on which to publish it
    # 或指定发布的特定日期
    $ bundle exec jekyll publish _drafts/my-new-draft.md --date 2014-01-24
    # or specify a custom format for the date attribute in the yaml front matter
    # 或者为yaml前端事务中的date属性指定自定义格式
    $ bundle exec jekyll publish _drafts/my-new-draft.md --timestamp-format "%Y-%m-%d %H:%M:%S %z"
```

Rename your post using:

使用以下方法重命名您的帖子：

```sh
$ bundle exec jekyll rename _posts/2014-01-24-my-new-draft.md "My New Post"
# or specify a specific date
# 或指定特定日期
$ bundle exec jekyll rename _posts/2014-01-24-my-new-post.md "My Old Post" --date "2012-03-04"
# or specify the current date
# 或指定当前日期
$ bundle exec jekyll rename _posts/2012-03-04-my-old-post.md "My New Post" --now
```

Unpublish your post using:

使用以下方式取消发布您的帖子：

```sh
    $ bundle exec jekyll unpublish _posts/2014-01-24-my-new-draft.md
```

Create your new file in a collection using:

使用以下方法在集合中创建新文件：

```sh
    $ bundle exec jekyll compose "My New Thing" --collection "things"
```

## Configuration 配置

To customize the default plugin configuration edit the `jekyll_compose` section within your jekyll config file.

要自定义默认插件配置，请编辑jekyll配置文件中的“jekyll_compose”部分。

### auto-open new drafts or posts in your editor

#### 在编辑器中自动打开新草稿或帖子

```yaml
  jekyll_compose:
    auto_open: true
```

and make sure that you have `EDITOR`, `VISUAL` or `JEKYLL_EDITOR` environment variable set.
For instance if you wish to open newly created Jekyll posts and drafts in Atom editor you can add the following line in your shell configuration:

并确保设置了“EDITOR”、“VISUAL”或“JEKYLL_EDITOR”环境变量。

例如，如果您希望在Atom编辑器中打开新创建的Jekyll帖子和草稿，您可以在shell配置中添加以下行：

```sh
export JEKYLL_EDITOR=atom
```

`JEKYLL_EDITOR` will override default `EDITOR` or `VISUAL` value.
`VISUAL` will override default `EDITOR` value.

JEKYLL_EDITOR`将覆盖默认的`EDITOR`或`VISUAL`值。

`VISUAL`将覆盖默认的`EDITOR`值。

### Set default front matter for drafts and posts

#### 设置草稿和帖子的默认标题

If you wish to add default front matter to newly created posts or drafts, you can specify as many as you want under `default_front_matter` config keys, for instance:

如果您希望将默认的主题添加到新创建的帖子或草稿中，可以在“default_front_matter”配置键下指定任意数量，例如：

```yaml
jekyll_compose:
  default_front_matter:
    drafts:
      description:
      image:
      category:
      tags:
    posts:
      description:
      image:
      category:
      tags:
      published: false
      sitemap: false
```

This will also auto add:

这也将自动添加：

- The creation timestamp under the `date` attribute.
- “日期”属性下的创建时间戳。
- The title attribute under the `title` attribute
- “title”属性下的title属性

For collections, you can add default front matter to newly created collection files using `default_front_matter` and the collection name as a config key, for instance for the collection `things`:

对于集合，可以使用“default_front_matter”和集合名称作为配置键将默认的front-matter添加到新创建的集合文件中，例如，对于集合“things”：

```yaml
jekyll_compose:
  default_front_matter:
    things:
      description:
      image:
      category:
      tags:
```

## Contributing 捐助

1. Fork it ( <http://github.com/jekyll/jekyll-compose/fork> )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Run the specs and our linter (`script/cibuild`)
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Push to the branch (`git push origin my-new-feature`)
6. Create new Pull Request

### Submitting a Pull Request based on an existing proposal

When submitting a pull request that uses code from an unmerged pull request, please be aware of the following:

- Changes proposed in the older pull request is still the original author's property. Moving forward from where they left it
  means that you're a `co-author`.
- GitHub allows attributing
  [credit to multiple authors](https://help.github.com/en/articles/creating-a-commit-with-multiple-authors)
  However, pull requests in this project are automatically squashed and then merged onto the base branch. So, only authors and
  co-authors of the opening commit gets credit once the pull request gets merged.
- If the original pull request contained multiple commits, you may squash them into a single commit but ensure that you list
  any additional authors (and yourselves) as co-authors of that commit.
- Use appropriate [keywords](https://help.github.com/en/articles/closing-issues-using-keywords) in your pull request post to
  link to the existing pull request or issue-ticket so that they're automatically closed when your pull request gets merged.
