## hugo

```console
brew install go
go version

brew install hugo
hugo version

hugo new site myspace
code .
```

Above we can see basic hugo structure, we need a theme to be able to see the site

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


