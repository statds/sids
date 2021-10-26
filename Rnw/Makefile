RNW_SRC := $(wildcard *.Rnw)
TEX_OUTPUT := $(patsubst %.Rnw,%.tex,$(RNW_SRC))

.PHONY: all
all: $(TEX_OUTPUT)

%.tex: %.Rnw
	Rscript -e "knitr::knit('$<')"
	rsync -r figure/ ../figure

