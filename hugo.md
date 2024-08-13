## hugo

```console
brew install go
go version

brew install hugo
hugo version

hugo new site myspace
code .
```

## Create custom layout

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


## Using available layouts

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


