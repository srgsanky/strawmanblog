# Demo of how to use a hugo site with github pages

This blog is published at <https://srgsanky.github.io/strawmanblog/>


## Steps

<https://gohugo.io/getting-started/quick-start/>

### Prerequisites - install hugo

```bash
# In MacOS <https://gohugo.io/installation/macos/>
brew install hugo
```


### Create the hugo site

```bash
# This will create the directory for you, so you don't have to create a directory manually
hugo new site strawmanblog
cd strawmanblog
```

### Set theme

```bash
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme = 'ananke'" >> hugo.toml
```

### Add new content

```bash
hugo new content content/posts/my-first-post.md
```

### Serve content

```bash
# Includes drafts
hugo server -D
```

### Configure the site using site configuration file (hugo.toml/hugo.yaml/hugo.json)

`hugo.toml` placed at the root of the site directory.

```toml
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```

### Hosting on github

<https://gohugo.io/host-and-deploy/host-on-github-pages/>

1. Create `.github/workflows/hugo.yml`. Copy most of the sample file, but customize the following
    ```bash
    mkdir -p .github/workflows
    touch .github/workflows/hugo.yaml
    ```
    1. Use most of hugo.yml from the sample, but customize the following
        1. Remove caching related changes to started with.
        1. Customize the hugo build command
            `hugo -s ${{github.workspace}}/ -d ${{github.workspace}}/dist  --environment github-pages`
        1. Customize the path to find the built files
            `path: '${{github.workspace}}/dist'`
1. Fix base URL on `hugo.toml` to `https://srgsanky.github.io/strawmanblog/`
1. Add `public` and `resources` to `.gitignore`.

### About github pages

You could have:

1. https://yourusername.github.io (your personal homepage).
1. https://yourusername.github.io/project1/
1. https://yourusername.github.io/project2/
