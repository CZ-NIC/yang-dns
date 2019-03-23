SOURCES = $(wildcard *.yinx)
yams = $(SOURCES:.yinx=.yang)
yl = yang-library-data.json
modpath = .:../common:../ietf
xsldir = ../.tools/xslt
xslpars =

.PHONY: all clean

all: $(yams)

%.yang: %.yinx
	@xsltproc --xinclude $(xsldir)/canonicalize.xsl $< | \
	xsltproc --output $@ $(xslpars) $(xsldir)/yin2yang.xsl -

model.tree: $(yams)
	yangson -t -p $(modpath) $(yl) > $@

clean:
	@rm -rf $(yams) model.tree
