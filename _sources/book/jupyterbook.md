---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---


# How to write a book using Jupyter-Book on Github

This book is created using Jupyter-Book and published on GitHub. This document can be used as a reference to write another book.

## Introduction

[Jupyter Book](https://jupyterbook.org/stable/) is a tool to create computational narratives (i.e., books) that are accessible, reusable, reproducible, and interactive. JB is built on the [MyST Markdonw Document Engine (mystmd)](https://jupyterbook.org/stable/community/ecosystem/), which is a next generation document engine that is data-driven, computation-centric, and flexible. JB is a lightweight for mystmd.

We can write an online book using JB and publish it on Github using the [jupyter-book-demo template](https://github.com/giswqs/jupyter-book-demo) and YouTube video [Open Publishing in Action: Creating Interactive Books with Jupyter Book and MyST Markdown](https://www.youtube.com/watch?v=Z2d1Kw1xSVY) (published on 10/23/2025) which is part of the [Open Publishing](https://www.youtube.com/watch?v=BxoEM5x4EfQ&list=PLAxJ4-o7ZoPcudAyC050UOrSDr3v9leUP&index=2) part of  the [UTK Open Science Workshop](https://openscience.gishub.org/open-publishing/) held in the spring of 2025. The template sets up the project structure and configures the GitHub workflow to speed up the publishing process. This document is based on the YouTube video and the template project for reference.

Note there is an earlier version of the effort, the [cookiecutter-jupyter-book](https://github.com/giswqs/cookiecutter-jupyter-book) which is based on the [cookiecutter-jupyter-book](https://github.com/executablebooks/cookiecutter-jupyter-book).

## Create a book repository on GitHub

First we need to create a GitHub repository for the book. Here we assume that we have a GitHub account and we can use the [jupyter-book-demo template GitHub project](https://github.com/giswqs/jupyter-book-demo) to create our own book project.

* Use the "Use this template\Create a new repository" to create a new project on our GitHub repository
* Give a name to the book repository and simple description and then create the repository

Note: Jupyter-Book 2.x has some issues when building the book using command "uv run jupyter-book build .". So we will edit the file directly on GitHub to specify the version of 1.0.4 instead of 2.x for the package (i.e., jupyter-book==1.0.4). This is NOT necessary when those issues are addressed.

* Create a special branch (with the name "gh-pages") for the book repository to publish the book as [GitHub Pages](https://pages.github.com/) (basically a web site on github.io to host your personal, organization, or project pages from a GitHub repository). This is done by click on "main" and type in "gh-pages" and create the gh-pages branch from main. This also initiate the process (i.e., "Initial commit") of building the web site.
* The initial commit may encounter a permission error which can be resolved by changing "Settings\Actions\General\Workflow permissions" to "Read and write permission and rerun the job.
* Go to "Settings\Pages" to view the book web site. You can also link the site to a custom domain here.

## Set up a local environment

We will have a copy of the repository on local machine so that we can write the book locally and update it on the GitHub. We can use the git tool to clone a repository. In CMD,  navigate to your local folder and run the following command with your book repository URL:
```
# Navigate to your project directory
cd /path/to/your/project

# clone the repository
git clone https://github.com/XingongLi/spatial-data-analysis-with-map-compute.git
```

We will use VSC and Python to edit and write the book. We need to build a local Python environment for the book. Here we will use the latest uv tool to create and manage python environment. Follow the instructions [here](https://docs.astral.sh/uv/getting-started/installation/#installing-uv) to install uv on your machine.

Once uv is installed, you can create and activate a new environment with the following commands:

```
# Navigate to your project directory
cd /path/to/your/project

# Create a virtual environment
uv venv --python 3.12

# Activate the environment (varies by OS)
.venv\Scripts\activate

# Install all the dependence
uv pip install pip
uv pip install -r requirements.txt
```

## Write and edit the book

We can built the book by running command, and the local book can be opened under "_build\html\index.html".
```
uv run jupyter-book build .
```
If necessary, you can also remove any existing builds by:
```
uv run jupyter-book clean .
```

To build the book as PDF file and Word document using the following command:
```
uv run myst build --typst --pdf --docx
```

## Update the book online

To update the book's web site, we can open the book project in VSC, add or change any contents, commit and synchronize the changes on GitHub Pages. The template provides the workflow to automate the process of building the book.

## Tools

### Gemini

Most of lecture slides are saved as PDF files. Each slide is saved as a PDF page in those PDF files. The following is the "Master Prompt" that I used to convert a PDF file into a MD document as the draft/outline for the topic using Gemini.

"Please convert this PDF into a structured Markdown document. Use hierarchical headers and bullet points. Include all details from every slide. Keep the formatting clean by minimizing the use of bold text, and provide the final result inside a single Markdown code block for easy copying."

### Microsoft MarkItDown

[This X post](https://x.com/TheTuringPost/status/1977465872592867662?t=HAU2I-2JIPrk6LQHDrZMpg&s=09) mentioned using Microsoft [MarkItDown tool](https://github.com/microsoft/markitdown) to convert dozens of file types to MD. My initial test seems it is NOT as good as using Gemini. 