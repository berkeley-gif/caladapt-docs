# Cal-Adapt API Documentation and Cookbook

This repository contains documentation, tutorials and code samples for working with the Cal-Adapt API. Documentation created by Sphinx.


## Links
- [Cal-Adapt API Documentation and Tutorials](https://berkeley-gif.github.io/caladapt-docs/index.html)
- [Cal-Adapt website](beta.cal-adapt.org) 


## Setup
- Clone the repo

	```python
	git clone https://github.com/berkeley-gif/caladapt-docs.git
	```
- Change directory

	```python
	cd caladapt-docs
	```
- Create a python3 virtualenv

	```python
	python3 -m venv env
	```
- Install libraries

	```python
	pip install -r requirements.txt
	```


## Editing
- Make your edits in `docs/source`
- To rebuild the docs, run the following in `caladapt-docs` directory

	```python
	make html
	```
- Commit all changes and push to master. The `docs/build/html/` is also checked into the master branch. 
- Update website by deploying `docs/build/html/` to Github Pages branch.

	```python
	make gh-pages
	```
