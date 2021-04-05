SPHINXOPTS	=
SPHINXBUILD	= python -msphinx
SPHINXPROJ	= JDM
SOURCEDIR	= source
BUILDDIR	= "../../webDoc"

help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: help Makefile

html:
	cd $(BUILDDIR)/html
	git add .
	git commit -m "rebuilt docs"
	git push origin gh-pages
