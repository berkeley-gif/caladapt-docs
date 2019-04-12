Cal-Adapt API Documentation and Cookbook
========================================
This repository contains documentation, tutorials and code samples for working with the Cal-Adapt API. Documentation created by Sphinx.


Links
-----
- [Cal-Adapt API Documentation and Tutorials](https://berkeley-gif.github.io/caladapt-docs/)
http://api.cal-adapt.org/docs/
- [Cal-Adapt website](https://cal-adapt.org/)


Setup
-----
- Clone the repo

	git clone https://github.com/berkeley-gif/caladapt-docs.git

- Change directory

	cd caladapt-docs

- Create a python3 virtualenv

	python3 -m venv env

- Install libraries

	pip install -r requirements.txt


Editing
-------
- Make your edits in `docs/source`
- To rebuild the docs, run the following in `caladapt-docs` directory

	make html

- Commit all changes and push to master. The `docs/build/html/` is also checked into the master branch.
- Update website by deploying `docs/build/html/` to Github Pages branch.

	make gh-pages
