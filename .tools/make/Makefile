SOURCES = $(wildcard *.yinx)
EXAMPLE = example-data
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

model.tree: $(yams) $(yl)
	yangson -t -p $(modpath) $(yl) > $@

$(EXAMPLE).json: $(EXAMPLE).xml
	xsltproc -o $@ model.xsl $<

validate: $(EXAMPLE).json $(yams)
	yangson -v $< $(yl)

clean:
	@rm -rf $(yams) model.tree $(EXAMPLE).json
