## Project Overview

This directory contains a personal blog built with Jekyll, a static site generator written in Ruby. The site is hosted on GitHub Pages.

- **Framework:** Jekyll
- **Content Format:** Blog posts are written in AsciiDoc (`.adoc`).
- **Theme:** The site uses the "Type on Strap" theme.
- **Dependencies:** Ruby gems are managed via `bundler` and a `Gemfile`. Key dependencies include `jekyll`, `jekyll-asciidoc`, and various other Jekyll plugins.

## Building and Running

### Local Development

To run the site locally for development and previewing changes:

1.  **Install Dependencies:**
    ```bash
    bundle install
    ```

2.  **Run the Jekyll Server:**
    ```bash
    bundle exec jekyll serve --livereload
    ```

    The site will be available at `http://localhost:4000/blog/`. The `--livereload` flag automatically refreshes the browser when changes are made to the source files.

### Production Build

The production build is handled automatically by a GitHub Actions workflow. The command to build the site is:

```bash
bundle exec jekyll build
```

This command generates the static site in the `_site` directory.

## Deployment

Deployment is automated via the `.github/workflows/publish.yml` GitHub Actions workflow. The workflow is triggered on every push to the `master` branch. It performs the following steps:

1.  Checks out the code.
2.  Sets up Ruby and installs dependencies from the `Gemfile`.
3.  Builds the Jekyll site in production mode.
4.  Deploys the contents of the `_site` directory to GitHub Pages.

There is no need for manual deployment.

## Development Conventions

### Creating a New Post

1.  Create a new file in the `_posts` directory.
2.  The filename must follow the format `YYYY-MM-DD-your-post-title.adoc`.
3.  The file must start with a YAML front matter block, specifying the layout, title, author, and tags. For example:
    ```yaml
    ---
    layout: post
    title: "My New Blog Post"
    author: your_author_id
    tags: [tag1, tag2]
    ---
    ```
4.  Write the post content in AsciiDoc format.
5.  To include images, place them in a new subdirectory within `assets/img/` named after the post slug (e.g., `assets/img/YYYY-MM-DD-your-post-title/`). Then, in the post's front matter, set the `:imagesdir:` attribute:
    ```asciidoc
    :imagesdir: /blog/assets/img/YYYY-MM-DD-your-post-title
    ```
    You can then reference images in the post like this: `image::my-image.png[]`.
