# HUGO

Setting up go and hugo in mac with brew

```console
brew install go
go version

brew install hugo
hugo version

hugo new site myspace
code .
```
---

# Create custom layout

create _index.md under content

```markdown
---
title: Home
---

Hello World!!!
```

and about.md with title: About then create default layout as baseof.html under layouts folder unde _default folder

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{.Page.Title}}</title>
</head>
<body>
    {{ block "main" . }}
    {{ end }}
</body>
</html>
```
create 2 more html file under _default folder list.html for landing page and single.html for about page with below content

```html
{{ define "main"}}
  {{ .Content}}
{{ end }}
```

# Stylesheet

```html
{{ $style := resources.Get "sass/main.scss" | resources.ToCSS | resources.Minify }}
<link rel="stylesheet" href="{{ $style.Permalink }}">
```

then create main.scss under assets/sass/ folder

```css
body {
  width: 400px;
  margin: 0 auto;
  font-family: sans-serif;
}
```
# Partials

Create nav.html under /layoutes/partials/ 

```html
<nav>
 <ul>
   <li><a href="/">Home</a></li>
   <li><a href="/about/">About</a></li>
 </ul>
</nav>
```
then add below line in the baseof.html
```html
{{ partial "nav.html" }}
```
we can also create meta partial as meta.html
```html
<meta charset="utf-8">
<title>{{ print .Page.Title }}</title>
{{ $style := resources.Get "sass/main.scss" | resources.ToCSS | resources.Minify }}
<link rel="stylesheet" href="{{ $style.Permalink }}">
```
then add snippet in baseof.html
```html
{{ partial "meta.html" . }}
```
That little . at the end is passing the context of the current page, which allows the partial to print out the current page’s title.


# Using available layouts

Above we can see basic hugo structure, alternatively we can use a theme to be able to see the site

```console
cd myspace
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme = 'ananke'" >> hugo.toml
hugo server
```
we can also use git clone instead of fit submodule add

* you can refer from https://gohugo.io/getting-started/quick-start/ 

```console
echo "theme = 'ananke'" >> hugo.toml
hugo server
```
to add content and publish it(files in public folder)
```console
hugo new content content/posts/my-first-post.md
hugo
```
delete draft = true or assign false


