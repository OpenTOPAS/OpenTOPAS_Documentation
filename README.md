# OpenTOPAS-docs

The documentation is written in reStructuredText format (reST). It is hosted by [ReadTheDocs](https://docs.readthedocs.org). A good resource on reST is the [Sphinx documentation](http://www.sphinx-doc.org), but please note that not all features described there are supported by ReadTheDocs. It also describes some Python-only features, since that is its domain.

> [!WARNING]
> If working on a Mac, we recommend installing Python with [Homebrew](http://brew.sh) to avoid messing up your system Python. These instructions are only meant to be followed for substantial changes to the documentation.

You can download Python and `git` with the `brew` command as follows.

	brew install python
	brew install git

To build and view the docs locally (recommended for substantial editing), you will need to

	pip3 install sphinx sphinx-autobuild sphinx_rtd_theme
	pip3 install furo
 	pip3 install git+https://github.com/tmasilela/topas-pygments.git
	pip3 install git+https://github.com/harshil21/furo-sphinx-search@v0.2.0.1
	pip3 install myst-parser

Download the documentation:

 	git clone https://github.com/OpenTOPAS/OpenTOPAS_Documentation.git
	cd Documentation

You can now edit any of the .txt and .rst files in the subfolders. When ready to view the changes locally, navigate to the `/Documentation` directory and

	make clean
	make html
	open .build/html/index.html
