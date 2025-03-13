# Paleo Data Knowledge Hub

This repository contains files for the 
[Paleo Data Knowledge Hub](https://paleo-data.github.io/knowledge-hub) website,
which enables open access to resources for anyone producing, managing, or utilizing
paleontological specimen data. The hub empowers ongoing engagement and continuous
knowledge sharing across stakeholder communities. Resources hosted on the knowledge
hub are broadly relevant, and ideally adaptable to other domains beyond paleo. The
site design strives to be human-centered, especially prioritizing an intuitive
interface with a low barrier to entry for new users.

## Adding new pages

Contributors are welcome to add new content or suggest changes to existing content.
The instructions below describe the process for adding a new page to the site.

Once you are satisfied that the content you'd like to add is not already covered,
the next step is to decide where in the site it should go. The site is organized into
five sections:

- Community
- Data ecosystem
- Explanations
- How to guides
- Tutorials

Create a Markdown file under the appropriate section for your content. The filename
should be lowercase and include only numbers, letters, and hyphens. It should closely
match the page title and use the file extension `.md`.

### Writing front matter

Open the Markdown file and add the *front matter*, which is a special section at the 
top of each Markdown document with metadata about the page. Front matter is 
delineated by a line of three hyphens before and after the content. The content itself
is written in YAML, a human-readable markup language.

The front matter should include:

- The **title** of the page
- The publication **status** of the page. Pages with `status: published` are
  considered complete. Pages with any other status will include a warning that the
  page is still in draft form.
- The **last_modified_at** date as `yyyy-mm-dd`
- Associated **topics** as a list. In YAML, lists are comma-delimited and use square
  brackets. A list of topics in use on the site is available [here]().

Other metadata (for example, page layouts and navigation) are added automatically
based on the section the page appears in.

Metadata for the file `manage-data-about-lithostratigraphy.md` might look like this:

```yaml
---
title: Manage data about lithostratigraphy
status: draft
last_modified_at: 2025-03-14
topics: [manage data, lithostratigraphy]
---
```

### Writing content

Individual pages are written in Markdown, which is a simple, readable syntax used to
format text documents. Content can be added below the front matter. A cheat
sheet for Markdown is available [here](https://www.markdownguide.org/cheat-sheet/).

Markdown files can also include HTML. HTML should be used sparingly and only when
suitable Markdown is not available, for example, for embed tags.

Jekyll also supports [Liquid](https://shopify.github.io/liquid/), which is a template
language that can be used to add dynamic content to pages. Liquid tags should also be
used sparingly, with the primary exceptions being (1) use of the `relative_url`
filter to link to pages elsewhere on the site and (2) use of `include` tags to display
widgets defined by either the `minimal-mistakes` template or created specifically for
this site.

#### Linking within the site

We recommend using Jekyll's `relative_url` filter to link to other pages on the hub.
This filter accepts a root-relative URL. Note that the collections folder is not
part of the URL for pages in a collection and that page names do not need to include
a file extension.

Link to a top-level page:

```
[Community]{{ "/community" | relative_url }}
```

Link to a page in a collection:

```
[PDWG Happy Hours]{{ "/community/pdwg-happy-hours" | relative_url }}
```

#### Widgets

Include a list of related pages matching one or more topics:

```
{% include related_list topics='manage data|share data' %}
```

Include a list of external resources defined in the `_data/resources` folder matching
one or more topics:

```
{% include resource_list topics='symbiota' %}
```

Include a resource card to highlight a single resource defined in the
`_data/resources` folder:

```
{% include resource_card filename='pearson-2022.yml' %}
```

Include a 
[callout box](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#notices):

```
{: .notice--info }
**Callout**
Access the portal at [paleo.symbiota.org](https://paleo.symbiota.org)
```

## External resources

Information from external resources, like websites or publications, can also be
included on the site. Resources are defined as YAML files in the `_data/resources`
directory. Two templates for defining resources are available in the `templates/data`
folder:

- `data-file-zenodo.yml` can be used for resources published on Zenodo. It includes
  only the metadata fields needed to identify and annotate a resource. Additional
  metadata is pulled from Zenodo when the site is built.
- `data-file-manual.yml` is intended for non-Zenodo resources (like websites) and
  includes the metadata fields needed to construct a complete reference.

Both files include the topics field, which can be used to tag the resources in the
same way that internal pages are tagged.

## Building the site

It can be useful to build the site locally before submitting a pull request or
committing changes to the main repository. The build process uses a combination of
Python and Ruby to index the site, update metadata for external resources, and build
the HTML pages from the Markdown files.

Note that files created during the build process are not committed to GitHub. The build
process runs automatically through a GitHub Action when changes are pushed to the
repository.

### Initial setup

Building the site locally requires that the following three applications are installed:

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [MiniForge](https://github.com/conda-forge/miniforge) (under Install)
- [Ruby](https://www.ruby-lang.org/en/downloads) (under Ways of Installing Ruby)

Once those applications are installed, you can
[fork this repository](https://github.com/paleo-data/knowledge-hub/fork), then clone
the fork to your system:

```
git clone https://github.com/{username}/knowledge-hub
```

Navigate to the directory you just created:

```
cd path/to/knowledge-hub
```

Set up the Python environment:

```
mamba create -f environment.yml
```

Set up Jekyll:

```
gem install bundler jekyll
```

### Build the site locally

Open the command prompt and run the following commands to activate the environment
needed to build and run the site locally:

```
mamba activate pdh
cd path/to/knowledge-hub
```

To build the site and launch Jekyll, run the following commands in the same prompt:

```
cd scripts
python build-site.py
cd ..
bundle exec jekyll serve
```

Alternatively you can simply run Jekyll itself:

```
bundle exec jekyll serve
```

Jekyll will pick up many routine changes as files are updated, but some changes
(including but not limited to changes to _config.yml or topic lists on individual
pages) will not be reflected until Jekyll is restarted or the full site is rebuilt.

## Acknolwedgments

Icons are from the [Remix icon set](https://icon-sets.iconify.design/ri/) (Apache 2.0) from Iconify. 
