MAIN = main
MAIN_RNW = $(MAIN).Rnw
MAIN_TEX = $(MAIN).tex
PDFOUT  = $(MAIN).pdf
HTMLOUT = $(MAIN).html
RNW_DIR = Rnw
RNW_SRC = $(wildcard $(RNW_DIR)/*.Rnw)
RNW_OUT = $(patsubst %.Rnw,%.tex,$(RNW_SRC))
TEXSRC = $(wildcard *.tex)
BIBSRC = book.bib packages.bib
## executables
TEX    = xelatex
BIBTEX = bibtex
MAKEINDEX = makeindex

.PHONY: pdf html
pdf: $(PDFOUT)
html: $(HTMLOUT)

# knit Rnw/*.Rnw to Rnw/*.tex as needed
.PHONY: tex
tex: $(TEXOUT)

$(MAIN_TEX): $(MAIN_RNW)
	@Rscript -e "knitr::knit('$<', output = '$@')"

$(PDFOUT): $(TEXSRC) $(BIBSRC) $(MAIN_TEX) $(RNW_OUT)
	@Rscript -e "tinytex::latexmk('$(MAIN).tex', '$(TEX)', '$(BIBTEX)', clean = FALSE)"
# $(TEX) $(MAIN)
# $(BIBTEX) $(MAIN)
# while grep -e 'Rerun to get' -e 'run LaTeX again' *.log ; do $(TEX) $(MAIN) ; done
	$(MAKEINDEX) $(MAIN)
	$(TEX) $(MAIN)

$(HTMLOUT): $(PDFOUT)
	pdf2htmlEX --zoom 1.3 $(PDFOUT)

# would be invoked by tex but not pdf/html
Rnw/%.tex: Rnw/%.Rnw
	@Rscript -e "setwd('$(RNW_DIR)'); knitr::knit('$(<F)', output = '$(@F)')"

.PNONY: clean cleaner
clean:
	$(RM) -r $(OUT) *~ .*~ .\#* .Rhistory *.aux *.bbl *.blg *.dvi *.out *.log *.toc \
	*.fff *.fdb_latexmk *.fls *.ttt *diff* *oldtmp* .blb *.idx *.ilg *.ind

cleaner: clean
	$(RM) $(RNW_OUT)
