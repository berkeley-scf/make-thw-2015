INTERIMS = *.aux *.bbl *.blg *.log *.bak *~ *.Rout
INPUT_DATA = census.dat
DATA_WEBSERVER = http://www.census.gov/datafiles
DATA = *.Rda *.csv
USER = paciorek
SERVER = foo.berkeley.edu
WEBDIR = /web/share/$(USER)/files

R_OPTS = --no-save
R = R CMD BATCH $(R_OPTS)

mypaper.pdf: mypaper.bib mypaper.tex tables.tex Figs/fig1.pdf Figs/fig2.pdf
	pdflatex mypaper
	bibtex mypaper
	pdflatex mypaper
	pdflatex mypaper

# would be nice to automate checking to see if data on web has changed
web_data:
	cd data; wget $(DATA_WEBSERVER)/$(INPUT_DATA)

data.csv: code/make_data.py data/census.dat
	cd code; python make_data.py

results.Rda: data.csv model.R
	cd code; $(R) model.R model.Rout

tables.tex: results.Rda make_tables.R
	cd code; $(R) make_tables.R make_tables.Rout

Figs/fig1.pdf: R/fig1.R results.Rda
	cd code; $(R) fig1.R fig1.Rout

Figs/fig2.pdf: R/fig2.R results.Rda
	cd code; $(R) fig2.R fig2.Rout

web: *.pdf *.tex code/*.R code/*.py
	zip analysis.zip code/*.{R,py} *.pdf *.tex
	scp analysis.zip $(USER)@$(SERVER):$(WEBDIR)/.

clean:
	rm -f $(INTERIMS)

cleanall:
	rm -f $(INTERIMS) $(DATA)

.PHONY: web clean cleanall web_data
