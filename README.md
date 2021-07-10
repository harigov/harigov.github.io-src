# Blog Management

Blog is setup such that the `-src` repository contains the source code for the blog
and the regular blog repository contains the generated blog. Blog uses [`pelican`](https://docs.getpelican.com/en/3.6.3/quickstart.html) blog
management software. Here is the directory structure:

- `content` directory contains the main blog articles
- `themes` directory contains the themes that I have considered
- `workinprogress` directory contains all the blogs that are in progress
- `output` directory contains the output blog html after pelican is run

The contents of the `output` directory are then copied to main blog repository to update
the blog.

### Basic Setup

Blog runs using python3

First setup a virtual environment for the repo

```bash
$ python3 -m venv repo-env
$ source repo-env/bin/activate
```

### Running the server

Start the server using following command:

```bash
$ ./develop_server.sh start 8080
```

And then open the browser to point to `http://localhost:8080`

### Writing new blog articles

Pelican considers “articles” to be chronological content, such as posts on a blog,
and thus associated with a date.

The idea behind “pages” is that they are usually not temporal in nature and are used
for content that does not change very often (e.g., “About” or “Contact” pages).

Pelican supports writing blogs in several formats. Two of which are `markdown` and `html`.
No matter which format we choose, we need to provide additional metadata for it to work properly.

For markdown, it will be in the form of categories defined at the top of the file, like below:
Use your preferred text editor to create your first article with the following content:

```markdown
Title: My super title
Date: 2010-12-03 10:20
Modified: 2010-12-05 19:30
Category: Python
Tags: pelican, publishing
Slug: my-super-post
Authors: Alexis Metaireau, Conan Doyle
Summary: Short version for index and feeds

This is the content of my super blog post.
```

Given that this example article is in Markdown format, save it as `content/my-super-blog-post.md`.

For html, it will be read metadata from meta tags, the title from the title tag, and the body out from the body tag:

```html
<html>
    <head>
        <title>My super title</title>
        <meta name="tags" content="thats, awesome" />
        <meta name="date" content="2012-07-09 22:28" />
        <meta name="modified" content="2012-07-10 20:14" />
        <meta name="category" content="yeah" />
        <meta name="authors" content="Alexis Métaireau, Conan Doyle" />
        <meta name="summary" content="Short version for index and feeds" />
    </head>
    <body>
        This is the content of my super blog post.
    </body>
</html>
```

### Generating blog

Run the following command to generate the html version of the blog

```bash
pelican content
```

This generates static website with all the files located in the `output` directory. 

### Publishing blog

Copy the files from `output` directory to the main blog repository and commit the changes
for them to reflect in the github website. 
