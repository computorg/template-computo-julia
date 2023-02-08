
# Computo template for Julia users

[![build and deploy](https://github.com/computorg/template-computo-julia/actions/workflows/build.yml/badge.svg)](https://github.com/computorg/template-computo-julia/actions/workflows/build.yml)

Documentation and sample of a simple `Julia`-based submission for the [Computo journal](https://computorg.github.io), using our Quarto-based template and Julia github-action for handling dependencies.

Shows how to automatically setup and build the HTML and PDF outputs, ready to submit to our peer-review platform.

Additional details can be found [in the template manuscript](https://computo.sfds.asso.fr/template-computo-python). 

  ## Process overview

Submissions to [Computo](https://computorg.github.io) require both scientific content (typically equations, codes and figures, data) and a proof that this content is reproducible. This is achieved by means of i) a notebook system, ii) a virtual environment fixing the dependencies and iii) continuous integration (plus, if needed, an external website to store large data files such a [Zenodo](https://zenodo.org/) or [OSF](https://osf.io/) ). 

A Computo submission is thus a git(hub) repository like this one containing 

- the source files of the notebook (a quarto .qmd file + a BibTeX .bib file + some statics files, _e.g._ figures or small .csv data tables)
- configuration files to set up the dependencies in a virtual environment
- configuration files to set up the continuous integration rendering the final documents

In this template, we focus on `Julia` users and detail a solution based on

- The `julia-1.8` `Jupyter` kernel of Quarto for rendering the document,
- The Julia built-in `Pkg` for setting the environment,
- Github actions for handling the continuous integration.

## Step-by-step procedure

### Step 0: setup a git repository

Use this repository as a template via the "use this template" button on the top of this page.

**Note**: _You can use Gitlab for submitting for Computo. We hope giving more support in the future._

### Step 1. setup Quarto and Computo extension on your system

You need [quarto](https://quarto.org/) installed on your computer, as well as the [Computo extension](https://github.com/computorg/computo-quarto-extension) to prepare your document. 
The latter can be installed as follows:

```.bash
quarto add computorg/computo-quarto-extension
```

### Step 2. write your contribution 

Write your notebook as usual, [as demonstrated in the `template-computo-python.qmd` sample](https://computorg.github.io/template-computo-python/).

**Note**: _Make sure that you are able to build your manuscript as a standard notebook on your system before proceeding to the next step._

### Step 3: setup dependencies with `Pkg`, Julia's built-in package manager

Use the [`Pkg` package manager](https://docs.julialang.org/en/v1/stdlib/Pkg/) to setup a reproducible environment handling your `Julia` dependencies.

### Step 4: proof reproducibility

Put everything together and check that your work is indeed reproducible. To this end, you need to rely on a github action, whose default is pre-configured and found here: [.github/workflows/build.yml](https://github.com/computorg/template-computo-R/blob/main/.github/workflows/build_n_publish.yml)

This action will

1. Check out repository on the ubuntu-latest machine
2. Install quarto and dependencies, including the Computo extension for Quarto
4. Install Julia and dependencies with `Pkg` using the `Project.toml` and `Manifest.toml` files (found here in the directory `julia_env`)
5. Render your .qmd file and Publish the results on a gh-page (both HTML and PDF)

**Note**: _Gitlab CI can be used to obtained similar results._

### Step 5. submit

Once step 4 is successful, you should end up with an HTML version published as a gh-page, as well as a PDF version (see "Other format" at the end of the table of content of the rendered HTML). This PDF version can be submitted to the [Computo submission platform](https://computo.scholasticahq.com/):

<div id="scholastica-submission-button" style="margin-top: 10px; margin-bottom: 10px;"><a href="https://computo.scholasticahq.com/for-authors" style="outline: none; border: none;"><img style="outline: none; border: none;" src="https://s3.amazonaws.com/docs.scholastica/law-review-submission-button/submit_via_scholastica.png" alt="Submit to Computo"></a></div>
