# Minimal makefile for Sphinx documentation
#

# You can set these variables from the command line.
SPHINXOPTS    = -W  # turn warnings into errors
SPHINXBUILD   = sphinx-build
SPHINXPROJ    = torchvision
SOURCEDIR     = source
BUILDDIR      = build

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

docset: html
	doc2dash --name $(SPHINXPROJ) --icon $(SOURCEDIR)/_static/img/pytorch-logo-flame.png --enable-js --online-redirect-url http://pytorch.org/vision/ --force $(BUILDDIR)/html/

	# Manually fix because Zeal doesn't deal well with `icon.png`-only at 2x resolution.
	cp $(SPHINXPROJ).docset/icon.png $(SPHINXPROJ).docset/icon@2x.png
	convert $(SPHINXPROJ).docset/icon@2x.png -resize 16x16 $(SPHINXPROJ).docset/icon.png

html-noplot:  # Avoids running the gallery examples, which may take time
	$(SPHINXBUILD) -D plot_gallery=0 -b html $(ASPHINXOPTS)  "$(BUILDDIR)"/html
	@echo
	@echo "Build finished. The HTML pages are in $(BUILDDIR)/html."

clean:
	rm -rf $(BUILDDIR)/*
	rm -rf auto_examples/

.PHONY: help Makefile docset

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
