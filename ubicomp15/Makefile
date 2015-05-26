LATEX = pdflatex
TEXFILES = $(wildcard *.tex)
BIBFILES = $(wildcard *.bib)

MAINFILE = main
	
all: $(MAINFILE).pdf

%.pdf: %.tex %.bib %.blg *.cls $(TEXFILES) $(BIBFILES)
	pdflatex $*.tex 
	bibtex --min-crossrefs=20 $*
	pdflatex $*.tex
	pdflatex $*.tex

%.blg: %.bib
	pdflatex $*.tex
	bibtex --min-crossrefs=20 $*
	pdflatex $*.tex

%.toc: %.tex
	pdflatex $*.tex

clean:
	/bin/rm -f $(MAINFILE).pdf *.dvi *.aux *.ps *~ *.log
	/bin/rm -f *.lot *.lof *.toc *.blg *.bbl url.sty *.out

view: 
	pdflatex $(MAINFILE).tex
	acroread  -geometry 1000x1000 $(MAINFILE).pdf

html:	
	latex2html -nonavigation -math -html_version '4.0' -split 0 paper.tex
	
osx:
	pdflatex $(MAINFILE).tex
	open $(MAINFILE).pdf

check:
	pdflatex $(MAINFILE).tex | grep -s -e "multiply" -e "undefined"

pdf: 
	latex $(MAINFILE).tex
	bibtex $(MAINFILE)
	#Insert \vspace*{0.5mm}\n\scriptsize into $(MAINFILE).bbl
	#Also insert \vfill\eject to pagebreak in the references and balance columns
	latex $(MAINFILE).tex
	dvips -P pdf -G0 -t letter -o $(MAINFILE).ps $(MAINFILE).dvi
	#dvipdf -P pdf -t letter $(MAINFILE).dvi $(MAINFILE).pdf
	ps2pdf -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress $(MAINFILE).ps $(MAINFILE).pdf

