MAIN = main
OUT  = $(MAIN).pdf
RNW_DIR = Rnw
RNW_SRC = $(wildcard $(RNW_DIR)/*.Rnw)
RNW_OUT = $(patsubst %.Rnw,%.tex,$(RNW_SRC))
TEXSRC = $(wildcard *.tex)
BIBSRC = book.bib packages.bib
## executables
TEX    = xelatex
BIBTEX = bibtex
MAKEINDEX = makeindex

.PHONY: all
all: $(OUT)


$(OUT): $(TEXSRC) $(BIBSRC) $(RNW_OUT)
	$(TEX) $(MAIN)
	$(BIBTEX) $(MAIN)
	while grep -e 'Rerun to get' -e 'run LaTeX again' *.log ; do $(TEX) $(MAIN) ; done
	$(MAKEINDEX) $(MAIN)
	$(TEX) $(MAIN)


Rnw/%.tex: Rnw/%.Rnw
	@Rscript -e "knitr::knit('$<', output = '$@')"

.PNONY: clean
clean:
	rm -rf $(OUT) *~ .*~ .\#* .Rhistory *.aux *.bbl *.blg *.dvi *.out *.log *.toc \
	*.fff *.fdb_latexmk *.fls *.ttt *diff* *oldtmp* .blb *.idx *.ilg *.ind \


cleaner:
	make clean
	rm $(RNW_OUT)
