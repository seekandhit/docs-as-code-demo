# Docs-as-Code Demo

For this demo we chose MkDocs hosted on read-the-docs to demonstrate how to set up a simple Docs-as-Code system in your repo.
This guide will essentially be a quick run-through of the complete setup described in their respective documentation. 

## Guide

### Building the docs

Assuming you have a git repository, the first step is installing the `mkdocs` package.
For this, you will need `pip` (Python package installer). Simply run:

```bash
pip install mkdocs
```

Before continuing confirm the installation with `mkdocs --version`.

If everything went well, navigate to your repository root folder and run:

```bash
mkdocs new .
```

This will create a `docs` folder along with a `mkdocs.yml` configuration file.
The `docs` folder will hold all of your markdown files, in other words, your documentation.

We can now serve the docs and monitor the changes we make:

```bash
mkdocs serve  # This should serve the docs on http://127.0.0.1:8000/
```

Any markdown file you add, you should link in the navigation. To do this expand the `mkdocs.yml` configuration with the `nav` property. You should now have something like this:

```yaml
site_name: DaC Demo
nav:
  - Home: index.md
  # Just lorem ipsum files below
  - Reference: reference.md
  - About: about.md
  - Contact: contact.md
```

Let's also add some theming. We are going to use the classic `readthedocs` theme as we are going to be hosting it there anyway:

```yaml
site_name: DaC Demo
nav:
  - Home: index.md
  - Reference: reference.md
  - About: about.md
  - Contact: contact.md
theme: readthedocs
```

Now we can build our docs as they are ready to deploy:

```bash
mkdocs build
```

This will generate a `site` folder which contains all the statically generated sites from your markdown.

### Deploying the docs

As we mentioned we will deploy the documentation to ReadtheDocs. You will need to create an account [there](https://about.readthedocs.com/?ref=readthedocs.com) before you can continue. In case you are deploying some personal project it is completely free.

Now before we connect our repository to ReadtheDocs we need another configuration file called `.readthedocs.yaml`. This simply tells ReadtheDocs how to handle your documentation.

MkDocs has a predefined configuration for ReadtheDocs so we will use some existing boilerplate configuration given to us from ReadtheDocs.

```yaml
# Read the Docs configuration file for MkDocs projects
# See https://docs.readthedocs.io/en/stable/config-file/v2.html for details

# Required
version: 2

# Set the version of Python and other tools you might need
build:
  os: ubuntu-22.04
  tools:
    python: "3.11"

mkdocs:
  configuration: mkdocs.yml
```

Once you have added this file to the root folder of your project, push your changes.

Deploying to ReadtheDocs can be done in two ways. You can manually import the project, or simply connect your GitHub account to your ReadtheDocs account. If you choose to import it manually, you will have to trigger the build each time a new version is deployed. Connecting your GitHub account will make sure deployments happen automatically from your watched branch.

To do any of these two, once you are logged in, from the dashboard click `Import a Project` and follow the steps. once your build is complete you will be able to check out your deployed docs.
For the docs of this project head to https://dac-demo.readthedocs.io/en/latest/.

You are all set, happy documenting!
