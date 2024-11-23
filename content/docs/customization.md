---
title: Customization
description: Describes common Mainroad theme configuration parameters that can be adjusted via config file or via Front
  Matter section.
lead: Describes common Mainroad theme configuration parameters that can be adjusted via config file or via Front Matter section.
date: 2024-01-24T14:00:00.000Z
thumbnail:
  src: "img/壁纸2.png"
  visibility:
    - list
authorbox: false
sidebar: false
pager: false
weight: 2
menu: main
---

<!--more--> #`<!--more-->` 是一个常用于博客和网站内容管理中的标记，特别是在使用WordPress等CMS（内容管理系统）时。这个标记的主要作用是将文章内容分割成两部分：摘要（或预览）和全文。

This section will mainly cover customization settings that are unique to this theme. If something is not covered here,
there's a good chance it is covered somewhere in [Hugo docs](https://gohugo.io/documentation/).

### Logo

**Mainroad** allows you to set a custom logo in the site header. You may use text, or image, or both. Use the following options in your site config:

- `image = "img/placeholder.png"`：这里设置的是徽标的图片路径，您可以替换 `"img/placeholder.png"` 为您自己的图片路径。
- `title = "Mainroad"`：这里设置的是网站的标题，您可以将其更改为您想要的标题。
- `subtitle = "Just another site"`：这里设置的是网站的副标题，同样可以根据您的需求进行修改。

```toml
[Params.logo]
  image = "img/壁纸2.png"
  title = "Mainroad"
  subtitle = "Just another site"
```

**Note:** logo image will display at a maximum width of 128 pixels and a maximum height of 128 pixels
when you use text and image simultaneously. When the only logo image is active, it will display at a maximum height of 256 pixels. Ideally, your logo image should be SVG.

- 当您同时使用文本和图片作为 logo 时，图片的最大宽度和最大高度都会被限制在 128 像素。
- 当仅使用图片作为 logo 时，图片的最大高度会被限制在 256 像素（宽度可能会根据图片的原始宽高比自动调整，以保持图片的纵横比）。
- 此外，注释还建议您的 logo 图片最好是 SVG 格式。SVG（可缩放矢量图形）是一种基于 XML 的标记语言，用于描述二维矢量图形。

---

If you don't set any of these variables, the theme uses the site title as a logo title. Don't need a logo section?
Disable it this way:

```toml
[Params.logo]
  image = false
  title = false
  subtitle = false
```



### Hghlight color

Mainroad uses `#e22d30` as a default highlight color, but you may choose and set any other color.

```toml
[Params.style.vars]
  highlightColor = "#e22d30"
```



### Post meta 

关于“Post meta”（文章元数据）的说明，通常用于网站或博客系统中。

Post meta is a feature that refers to including additional meta information (such as author name, categories, date,translations, etc.) on pages. It can be enabled via config using the `post_meta` key with a list of meta field names asvalue. Order matters here: rearrange fields if you want to.

```toml
[Params]
  post_meta = ["author", "date", "categories", "translations"]
```

Full list of available default post meta fields:

* `author`, `categories`, `date`, `translations`

In addition to the default meta fields, you can add your own by placing a custom partial under
`layouts/partials/post_meta/<name>.html`.

####   Post meta: `date` localization

With [Hugo v0.87.0](https://gohugo.io/news/0.87.0-relnotes/) (or later), `date` meta field shows localized dates (with
weekdays and months in the current language) by default. In most cases, such a transition is painless, but owners of
multilingual sites should be careful and check that everything translates as expected after the upgrade.

You can also use a predefined layout, like `:date_full`, and it will output localized dates or times. For additional
information about localized dates and possible date/time formatting layouts, please see
[Hugo: time.Format](https://gohugo.io/functions/dateformat/).

### Thumbnail visibility

缩略图（thumbnail）可见性的配置

By default, a thumbnail image has shown for a **list and single pages** simultaneously. In some cases, you may want to show
a thumbnail for list-like pages only and hide it on single pages (or vice versa). Control global thumbnail visibility
via config, use the key `visibility` with combination of valid values `"list"` and `"post"`.

```toml
[Params.thumbnail]
  # Show thumbnail only for list items
  visibility = ["list"]
```

此配置表示缩略图将仅在列表页面（如博客文章列表、标签页面等）上显示，而在单个页面（如单独的博客文章页面）上则不显示。

Besides global configuration, you can change thumbnail visibility individually with extended thumbnail notation via
front matter block.

```yaml
thumbnail:
  src: "img/placeholder.png"
  visibility:
    - list
    - post
```

This page is an example of list-only thumbnail visibility.

除了全局配置外，您还可以通过页面或文章的前言（front matter）块使用扩展的缩略图表示法来单独更改缩略图的可见性。

### Sidebar 侧边栏

**Mainroad** comes with a configurable sidebar that can be on the left, on the right, or disabled. The default layout
can be specified in the `[Params.sidebar]` section of the configuration. The position can be specified for home, list
and single pages individually. Use the keys `home`, `list` and `single` with values `"left"`, `"right"` or `false`.

**Mainroad**附带了一个可配置的侧边栏，可以在左侧、右侧或禁用。默认布局可以在配置的“[Params.carebar]”部分指定。可以为主页、列表指定位置以及单独的单页。使用带有值“left”、“right”或“false”的键“home”、“list”和“single”。

```toml
[Params.sidebar]
  home = "right"
  list = "right"
  single = "right"
```

The layout can be configured per page, by setting the `sidebar` parameter with one of the same values (`"left"`,
`"right"` or `false`) in the page's front matter.

```yaml
sidebar: "left" # Enable sidebar (on the left side) per page
```

The sidebar consists of multiple widgets. Widgets can be enabled individually using the `widgets` key with a list of
widget names as value. You can add your own widgets, by placing a template under `layouts/partials/widgets/<name>.html`.

侧边栏由多个小部件组成。可以使用“小部件”键单独启用小部件，并将小部件名称列表作为值。您可以通过在“layouts/partials/widgets/<name>.html”下放置一个模板来添加自己的小部件。

```toml
[Params.sidebar]
  # Enable widgets in given order
  widgets = ["search", "recent", "categories", "taglist", "social", "languages"]
  这表示侧边栏将按顺序包含搜索、最近文章、分类、标签列表、社交链接和语言选择这些小部件。
```

The list of widgets can be overwritten from a page's front matter.

```yaml
# Enable sidebar widgets in given order
widgets:
  - "search"
  - "recent"
  - "taglist"
```

Full list of available default widgets:

* `search`, `ddg-search`, `recent`, `categories`, `taglist`, `social`, `languages`

**Note**: DuckDuckGo widget (`ddg-search`) deprecated in favor  of `search` widget.

- **默认小部件列表**：可用的默认小部件包括`search`（搜索）、`ddg-search`（DuckDuckGo搜索，现已被`search`小部件取代）、`recent`（最近文章）、`categories`（分类）、`taglist`（标签列表）、`social`（社交链接）和`languages`（语言选择）。

---

Some of our widgets respect optional configuration. Have a look at the `[Params.widgets]` and `[Params.widgets.social]`
sections in the example below.

```toml
[Params.widgets]
  recent_num = 5 # Set the number of articles in the "Recent articles" # widget 设置“最近文章”小部件中的文章数量 
  categories_counter = false # Enable counter for each category in # "Categories" widget 在“分类”小部件中禁用每个分类的计数 
  tags_counter = false # Enable counter for each tag in "Tags" # widget 在“标签”小部件中禁用每个标签的计数
```

```toml
[Params.widgets.social]
  # Enable parts of social widget
  facebook = "username"
  twitter = "username"
  instagram = "username"
  linkedin = "username"
  telegram = "username"
  github = "username"
  gitlab = "username"
  bitbucket = "username"
  email = "example@example.com"
```

在[Params.widgets.social]部分，你可以为社交小部件启用并配置不同的社交平台链接。

### Widget caching

Sidebar strongly affects overall build time, especially if you are using all of our widgets or even more. Widget caching
can significantly improve the generation time. Cached partials remain the same for all affected pages and are not
generated multiple times by Hugo. All built-in widgets (`search`, `recent`, `categories`, `taglist`, `social`,
`languages`) support caching.

Add `cached = true` inside the corresponding widget's dictionary table to activate caching. For example, to cache the
`recent` widget:

```toml
[Params.widgets.recent]
  cached = true
```

The following sample configuration extract shows how to cache all standard widgets and generate your website faster:

```toml
[Params.widgets.search]
  cached = true

[Params.widgets.recent]
  cached = true

[Params.widgets.categories]
  cached = true

[Params.widgets.taglist]
  cached = true

[Params.widgets.social]
  cached = true

[Params.widgets.languages]
  cached = true
```

Not all widgets are cacheable. If a widget contains (can contain) different data for different pages (e.g., for TOC
generation), then it should not be cached. Always check that your modified/customized widget is cached correctly.

### Social Widget: custom links

**Mainroad** contains built-in social links in the social widget. In addition to default social links, you may set
custom links by adding `Params.widgets.social.custom` to your `config.toml`. Here is an example:

```toml
[[Params.widgets.social.custom]]
  title = "My Home Page"
  url = "https://example.com"
```

If you want to display an icon of your social link, you need to put SVG icon file in `layouts/partials` directory under
your site's root. The `icon` key filed, which is optional, should be a path relative to `layouts/partials`.

```toml
[[Params.widgets.social.custom]]
  title = "Youtube"
  url = "https://youtube.com/user/username"
  icon = "youtube.svg"
```

**Note:** *Only* SVG files are supported to be used as custom social icons. If you use any other files, PNG for example,
a compile error will be raised by Hugo. Moreover, not every SVG icon can be used. For better results, it should be
one-color SVG file with a special class attribute `{{ with .class }}{{ . }} {{ end }}` and 24x24 size. At a minimum,
custom SVG icon needs these attributes:

```html
<svg class="{{ with .class }}{{ . }} {{ end }} icon" width="24" height="24">...</svg>
```

You can also specify the `rel` attribute for the link. By default, the attribute value is `"noopener noreferrer"`. You can remove the attribute completely by setting its value to `false`.

```toml
[[Params.widgets.social.custom]]
  title = "My Home Page"
  url = "https://example.com"
  rel = "me"

[[Params.widgets.social.custom]]
  title = "Youtube"
  url = "https://youtube.com/user/username"
  rel = false
```

### Search box widget

The search box widget can refer to the results of Google, Bing, and DuckDuckGo searches. By default, Mainroad uses
Google search if no additional configuration options are specified.

To use a different search engine, first of all, check that the search widget is enabled. Then set the search parameters
(`Site.Params.widgets.search` section) according to the data below.

**Google (default)**:

```toml
[Params.widgets.search]
  url = "https://google.com/search"
  [Params.widgets.search.input]
    name = "sitesearch"
    pre = ""
```

**DuckDuckGo**:

```toml
[Params.widgets.search]
  url = "https://duckduckgo.com/"
  [Params.widgets.search.input]
    name = "sites"
    pre = ""
```

**Bing**:

```toml
[Params.widgets.search]
  url = "https://www.bing.com/search"
  [Params.widgets.search.input]
    name = "q1"
    pre = "site:"
```

**Google PSE**:

```toml
[Params.widgets.search]
  url = "/search/"
  [Params.widgets.search.input]
    name = false
    pre = ""
```

Note that Google PSE requires additional steps to work correctly.
See [Creating a Programmable Search Engine](https://developers.google.com/custom-search/docs/tutorial/creatingcse) and
especially our [FAQ]({{< relref "/docs/faq.md" >}} "Mainroad FAQ") for more instructions.

### Menus

**Mainroad** supports multiple menus. The `main` menu is fully responsive and displayed right under the site header. The
secondary menus `side` and `footer` are displayed in a sidebar widget and the page footer respectively. To add a page to
a menu, add a `menu: <menu>` parameter to the page's front matter:

```yaml
menu: main # Add page to a main menu
```

**Note:** Don't forget to enable the `sidemenu` widget in the `widgets` configuration param if you want to use the
`side` menu.

---

You can also add a page to multiple menus by providing a list:

```yaml
# Add page to a main, side, and footer menu
menu:
  - main
  - side
  - footer
```

**Note:** Please keep in mind that Mainroad menus don't support nested items i.e. submenus.

See [Menus](https://gohugo.io/content-management/menus/#readout) from official Hugo documentation for more info.

### Custom Google Fonts support

Mainroad uses Open Sans from Google Fonts as a main font. But you can use any other font from Google Fonts if you'd
like. Beware, in most cases, such changes require manual CSS adjustment because every set of fonts is different and
might not look as good as our default font.

Follow the procedure below.

1. Open Google Fonts, choose font(s) that you prefer and copy href font link. For this particular example, we choose
[Roboto with 3 different styles](https://fonts.google.com/share?selection.family=Roboto:ital,wght@0,400;0,700;1,400;1,700).
Our href font link:

    ```
    https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400&display=swap
    ```

1. Set `googleFontsLink` site's config param value to your href font link. For example:

    ```toml
    [Params]
      googleFontsLink = "https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400&display=swap"
    ```

1. Override default font-family set(s):

    ```toml
    [Params.style.vars]
      fontFamilyPrimary = "'Roboto', sans-serif"
    ```

---

It is possible to disable Google Fonts and use system font stack instead.

1. Disable Google Fonts include. Set `googleFontsLink` site's config param value to `false`:

    ```toml
    [Params]
      googleFontsLink = false
    ```

1. Override font-family sets:

    ```toml
    [Params.style.vars]
      # Override font-family sets. Take care of different quotes OR escaping symbols in these params if necessary
      fontFamilyPrimary = "system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', 'Liberation Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'"
      # Secondary font-family set responsible for pre, code, kbd, and samp tags font
      fontFamilySecondary = "SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace"
    ```

[Edit this page on GitHub](https://github.com/vimux/mainroad/blob/master/exampleSite/content/docs/customization.md)
