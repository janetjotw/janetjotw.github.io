---
title: "Sphinx - RST to HTML"
date: 2025-01-30T11:22:19+00:00
draft: false
---

[reStructuredText](http://docutils.sourceforge.net/rst.html) is a lightweight markup language used in Static Site Generator (SSG) like [Sphinx](https://www.writethedocs.org/guide/tools/sphinx/). Sphinx is a Python application--an SSG to generate your documentation. 

This page showcases how to create documentation for Python modules in Sphinx.

- Install Sphinx

```
`pip install sphinx sphinx_rtd_theme`
```

2. From the repository, [https://github.com/janetjotw/sphinx_basics/tree/main](https://github.com/janetjotw/sphinx_basics/tree/main), fork it and run the below command from the docs folder:

```
`sphinx-quickstart`
```

Quickstart is a utility to generate the configuration file `conf.py` and the landing page `index.rst`.

3. To generate rst files from the maths modules, you want more than the basic index.rst landing page. To do this, go to the parent folder `sphinx_basics`, and run the command:

```
`sphinx-apidoc -o docs maths/
`
```

The command generates .rst files for the math modules. It generates `math.rst` and `modules.rst` files.

Now, include the generated `modules.rst` file in your `index.rst` file.

4. To generate documentation on Sphinx, run the below command to create HTML files.

```
`make html`
```

The HTML files are generated under > build/html. Open the HTML files on a browser.

5. See the screenshot below of the HTML documentation generated on Sphinx.