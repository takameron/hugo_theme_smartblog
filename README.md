SmartBlog
====

This is the theme for HUGO.  
It is for blogs and has various functions.

## How to Use
(See https://gohugo.io/getting-started/quick-start/)

1. Create a New Site
    ```
    hugo new site examplesite
    ```

1. Add a Theme
    ```
    cd examplesite
    git init
    git submodule add https://github.com/takameron/hugo_theme_smartblog.git themes/smartblog
    ```

1. Replace `archetypes/default.md` with the following text.
    ```
    ---
    title: "{{ replace .Name "-" " " | title }}"
    date: {{ .Date }}
    lastmod: {{ .Date }}
    author: "{{ .Site.Params.author.name }}"
    images: ["post-cover.png"]
    categories: ["category1"]
    tags: ["tag1","tag2"]
    archives: ["{{ dateFormat "2006" .Date }}","{{ dateFormat "2006-01" .Date }}"]
    toc: true
    draft: true
    ---

    ```

1. Replace `config.toml` with the following text. Then modify it if necessary.
    ```
    baseURL = "http://example.org/"
    title = "My New Hugo Site"
    languageCode = "en-us"
    hasCJKLanguage = false
    pygmentsUseClasses = true
    pygmentsCodefences = true
    theme = "smartblog"

    #GoogleAnalytics = "UA-12345-6"
    #disqusShortname = "yourdiscussshortname"
    ignoreErrors = ["error-remote-getjson"]
    timeout = 30000

    [params]
      title = "My New Hugo Site" # For OGP
      copyright = "website copyright"
      description = "website description"
      logo = "apple-touch-icon.png"
      quicklink = true

      [params.author]
        logo = "/img/default.png"
        name = "author name"
        description= "author description"
        email = "author@example.com"
        twitter = "author_twitter"
        facebook = "author_facebook"
        instagram = "author_instagram"
        github = "author_github"

    [params.color]
      [params.color.light]
        base = "#FFF"
        text = "#333"
        primary = "black"
        secondary = "#5989cf"
        headerfooter = "white"
        link = "blue"

      [params.color.dark]
        base = "#333"
        text = "#e4e4e4"
        primary = "black"
        secondary = "#5989cf"
        headerfooter = "white"
        link = "#3495eb"

    [taxonomies]
      tag = "tags"
      category = "categories"
      archive = "archives"

    [markup]
      [markup.goldmark]
        [markup.goldmark.renderer]
          unsafe = true

      [markup.highlight]
        guessSyntax = true
        linenos = true

    [outputs]
      page = ["HTML", "AMP"]
    ```

1. Please install the following files.
    * favicon (path : `static/`)
    * logo (This is for apple-touch-icon, JSON-LD. Specify a relative link in `params.logo` in `config.toml`.)
    * default.png (path : `static/img/`)
    * movie-cover.png (path : `static/img/`)

1. Create and edit an article file.
    ```
    hugo new posts/first-post/index.md
    ```
    or
    ```
    hugo new posts/first-post.md
    ```
    Then edit the created file.

1. Start the hugo server and check the website.  
    ```
    hugo server -D -F
    ```

    To include the Google Analytics code, please use `hugo server -D -F --environment production`.

## Dependencies
* I am using the following icon files via [IcoMoon](https://icomoon.io/).
    * [Simple Icons](https://simpleicons.org) (CC0 1.0 Universal)
    * [IcoMoon Free Version](https://icomoon.io/#icons-icomoon) (GPL / CC BY 4.0)

* [site_schema.html](layouts/partials/head/site_schema.html) refers to [this site](https://codingnconcepts.com/hugo/structure-data-json-ld-hugo/).


## Shortcodes

### blogcard
```
{{< blogcard "https://www.google.com/" >}}
```

I am using the API at https://meta-api-sigma.vercel.app/api/ .

| Attributes | Info             | Key | Order | Default Value | Required | 
| ---------- | ---------------- | --- | ----- | ------------- | -------- | 
| url        | URL of the site. |     | 0     |               | o        |

### book
This is for Japan.  
```
{{< book "9784344413023" >}}
```

| Attributes | Info                            | Key  | Order | Default Value | Required | 
| ---------- | ------------------------------- | ---- | ----- | ------------- | -------- | 
| isbn       | ISBN number(ISBN-13 or ISBN-10) | isbn | 0     |               | o        | 

### Cloudinary
```
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580351936/Blog-personal/thumbnail/default.jpg" alt="alt text" caption="Photo description" href="https://www.google.com/" >}}
```

| Attributes | Info                                                            | Key | Order | Default Value | Required | 
| ---------- | --------------------------------------------------------------- | --- | ----- | ------------- | -------- | 
| src        | URL of the image.                                               | src | 0     |               | o        | 
| width      | image width                                                     | w   |       | 600           |          | 
| height     | image height                                                    | h   |       |               |          | 
| alt        | alternative text(If `alt` is empty, `caption` will be used instead) | alt     |       |               |          | 
| caption    | caption                                                         | caption |       |               |          | 
| href       | URL of the caption link                                         | href    |       |               |          | 
| class      | class of figure tag                                             | class   |       |               |          | 

### download
```
{{< download "https://github.com/gohugoio/hugo/releases/download/v0.83.1/hugo_0.83.1_Windows-64bit.zip" "title" "description" >}}
```

| Attributes  | Info             | Key         | Order | Default Value | Required | 
| ----------- | ---------------- | ----------- | ----- | ------------- | -------- | 
| src         | URL of the file. | src         | 0     |               | o        | 
| title       | file title       | title       | 1     |               |          | 
| description | file description | description | 2     |               |          | 

### Gist
example : https://gist.github.com/takameron/d4ef18e5c6e51453e4d8a5184e723904

```
{{< gist takameron d4ef18e5c6e51453e4d8a5184e723904 >}}
```

| Attributes | Info      | Key | Order | Default Value | Required | 
| ---------- | --------- | --- | ----- | ------------- | -------- | 
| user       | user name |     | 0     |               | o        | 
| id         | gist id   |     | 1     |               | o        | 
| file       | file name |     | 2     |               |          | 

### img
```
{{< img src="https://example.com/picture.jpg" caption="Photo description" href="https://google.com/" >}}
```

| Attributes | Info                                                            | Key     | Order | Default Value | Required | 
| ---------- | --------------------------------------------------------------- | ------- | ----- | ------------- | -------- | 
| src        | URL of the image.                                               | src     | 0     |               | o        | 
| width      | image width                                                     | w       |       | 600           |          | 
| height     | image height                                                    | h       |       | 450           |          | 
| alt        | alternative text(If `alt` is empty, `caption` will be used instead) | alt     |       |               |          | 
| caption    | caption                                                         | caption |       |               |          | 
| href       | URL of the caption link                                         | href    |       |               |          | 
| class      | class of figure tag                                             | class   |       |               |          | 

### info
```
{{< info >}}
information text
{{< /info >}}
```

The text enclosed in `info` is displayed as information.

### math

```
{{< math >}} x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} {{< /math >}}
```

For inline
```
{{< math inline >}} x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} {{< /math >}}
```

Renders the enclosed text as a LaTeX formula (using KaTeX).

### product
This is for Japan.  
example : https://www.amazon.co.jp/dp/B08GCM963G/
```
{{< product asin="B08GCM963G" title="product name" maker="product manufacturer" kw="product keywards" >}}
```

| Attributes | Info                                  | Key   | Order | Default Value | Required | 
| ---------- | ------------------------------------- | ----- | ----- | ------------- | -------- | 
| asin       | Amazon Standard Identification Number | asin  |       |               | o        | 
| title      | Product name                          | title |       |               | o        | 
| maker      | Product manufacturer                  | maker |       |               | o        | 
| keyword    | Product keywords                      | kw    |       |               | o        | 

### Twitter
example : https://twitter.com/Twitter/status/1390725076996268038
```
{{< twitter user="Twitter" id="1390725076996268038" >}}
```

| Attributes | Info      | Key  | Order | Default Value | Required | 
| ---------- | --------- | ---- | ----- | ------------- | -------- | 
| user       | User Name | user |       |               | o        | 
| id         | Tweet ID  | id   |       |               | o        | 

### video
```
{{< video "https://example.com/video.mp4" poster="https://example.com/poster.jpg" >}}
```

| Attributes | Info              | Key    | Order | Default Value | Required | 
| ---------- | ----------------- | ------ | ----- | ------------- | -------- | 
| src        | URL of the video. | src    | 0     |               | o        | 
| width      | width             | w      |       | 600           |          | 
| height     | height            | h      |       | 450           |          | 
| poster     | hint image        | poster |       | responsive    |          | 

### warning
```
{{< warning >}}
warning text
{{< /warning >}}
```

The text enclosed in `warning` is displayed as warning.

### YouTube
example : https://www.youtube.com/watch?v=WJzSBLCaKc8

```
{{< youtube WJzSBLCaKc8 >}}
```

| Attributes | Info             | Key      | Order | Default Value | Required | 
| ---------- | ---------------- | -------- | ----- | ------------- | -------- | 
| id         | YouTube video ID | id       | 0     |               | o        | 
| width      | width            | w        |       | 480           |          | 
| height     | height           | h        |       | 270           |          | 
| autoplay   | AutoPlay Enabled | autoplay |       | false         |          | 
| layout     | layout           | layout   |       | responsive    |          | 

## License
The source code is licensed MIT.
