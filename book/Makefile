MAIN = main
OUT  = $(MAIN).pdf
RNW = $(wildcard Rnw/*.Rnw)
TEXSRC = $(wildcard *.tex)
BIBSRC = book.bib packages.bib
## executables
TEX    = xelatex
BIBTEX = bibtex
MAKEINDEX = makeindex

.PHONY: all
all: $(OUT)


$(OUT): $(TEXSRC) $(BIBSRC)
	$(TEX) $(MAIN)
	$(BIBTEX) $(MAIN)
	while grep -e 'Rerun to get' -e 'run LaTeX again' *.log ; do $(TEX) $(MAIN) ; done
	$(MAKEINDEX) $(MAIN)
	$(TEX) $(MAIN)


Rnw/%.tex: Rnw/%.Rnw
	cd Rnw;
	Rscript -e "knitr::knit('$^')"

.PNONY: clean
clean:
	rm -rf $(OUT) *~ .*~ .\#* .Rhistory *.aux *.bbl *.blg *.dvi *.out *.log *.toc \
	*.fff *.fdb_latexmk *.fls *.ttt *diff* *oldtmp* .blb *.idx *.ilg *.ind

