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
---
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
---
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

---
# Template
```html
<title>{{ .Params.title }} | {{ .Site.title }}</title>
<p>you can use double curly braces like this: {{ "Hello!" }}.</p>

{{ if isset .Params "title" }}
 <title>{{ .Params.title }}</title>
{{ else }}
 <title>{{ .Site.title }}</title>
{{ end }}

{{ $favorite_food := "Gazelle" }}
{{ $favorite_food }}

{{ $best_friends := slice "pumbaa" "timon" "nala" "rafiki" }}

<ul>
{{ range $best_friends }}
 <li>{{ . }}</li>
{{ end }}
</ul>
```

to create conditiotonal templeting, enter params in config.toml or hugo.toml file

```toml
[params]
name = 'Functor'
```
then create a footer.html partial where footer will only seen if params is exist
```html
{{ with .Params.hide_footer }}
 <!-- No footer here! -->
{{ else }}
 <footer>
   Website made by {{ .Site.Params.name }} in {{ now.Year }}
 </footer>
{{ end }}
```
then add partial in baseof.html

```html
{{ partial "footer.html" . }}
```
we can hide footer in any html page(content) adding hide_footer just below title
```html
hide_footer: true
```
---
# Creating Blog
cretate  _index.md under /content/posts/
```markdown
---
title: Blog
---
```
this markdown file will follow the rules of list.html unde /layouts/_default/ folder
we can create our spesific layout if we also create list.html  under /layout/posts folder
```html
{{ define "main"}}
  {{ .Content}}
{{ end }}
```
but we can also create single.html under /layout/posts/ folder so every post will follow the rules of single.html file's rules
```html
{{ define "main"}}
  {{ .Content}}
{{ end }}
```

---
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
```
or directly place below code to hugo.toml before running hugo server
```console
theme: ["PaperMod"]
```
delete draft = true or assign false
to add content and publish it(files in public folder)
```console
hugo new content content/posts/my-first-post.md
hugo server
hugo
```

when we created new post in terminal, the current time automatically created but if we like to create a file and add front matter later, we can modify date as
```console
date = `{{ .Date }}`
```



