# Cal-Adapt API Documentation and Tutorials

This repository contains documentation, tutorials and code samples for working with the Cal-Adapt API. Documentation created by Sphinx.

### Links
- [Cal-Adapt API Documentation and Tutorials](https://berkeley-gif.github.io/caladapt-docs/index.html)
- [Cal-Adapt.org](beta.cal-adapt.org) 

### Setup
- `git clone https://github.com/berkeley-gif/caladapt-docs.git`
- Create a python3 virtualenv `python3 -m venv env`
- `pip install -r requirements.txt`

### Editing
- Make your edits to `docs/source`
- Run `make html` to build the docs
- Commit all changes and push to master
- Run `make gh-pages` to deploy `docs/build/html/` to Github Pages branch.