LANG1=es
LANG2=ia
PREFIX1=$(LANG1)-$(LANG2)

BASENAME=apertium-es-ia
BILNAME=apertium-es-ia.es-ia.dix

TARGETS_COMMON = $(PREFIX1).automorf.bin $(PREFIX1).autobil.bin $(PREFIX1).autogen.bin \
     $(PREFIX1).autopgen.bin \
     $(PREFIX1).t1x.bin $(PREFIX1).t2x.bin $(PREFIX1).t3x.bin

TARGETS = $(TARGETS_COMMON)

@ap_include@

$(PREFIX1).automorf.bin: $(BASENAME).$(LANG1).dix
	apertium-validate-dictionary $(BASENAME).$(LANG1).dix
	lt-comp lr $(BASENAME).$(LANG1).dix $@

$(PREFIX1).autobil.bin: $(BILNAME)
	apertium-validate-dictionary $(BILNAME)
	lt-comp lr $(BILNAME) $@

$(PREFIX1).autogen.bin: $(BASENAME).$(LANG2).dix
	apertium-validate-dictionary $(BASENAME).$(LANG2).dix
	lt-comp rl $(BASENAME).$(LANG2).dix $@
	
$(PREFIX1).autopgen.bin: $(BASENAME).post-$(LANG2).dix
	apertium-validate-dictionary $(BASENAME).post-$(LANG2).dix
	lt-comp lr $(BASENAME).post-$(LANG2).dix $@
	
$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $(BASENAME).$(PREFIX1).t1x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t1x $@


$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $(BASENAME).$(PREFIX1).t2x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t2x $@


$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $(BASENAME).$(PREFIX1).t3x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t3x $@


EXTRA_DIST=$(BASENAME).$(LANG2).dix $(BILNAME) \
	   $(BASENAME).post-$(LANG2).dix \
	   $(BASENAME).$(LANG1).dix \
	   $(PREFIX1).prob \
	   $(BASENAME).$(PREFIX1).t1x $(BASENAME).$(PREFIX1).t2x \
	   $(BASENAME).$(PREFIX1).t3x \
	   modes.xml

apertium_es_ia_DATA=$(PREFIX1).automorf.bin \
		    $(PREFIX1).autobil.bin \
		    $(PREFIX1).autogen.bin \
		    $(PREFIX1).autopgen.bin \
		    $(PREFIX1).prob \
		    $(PREFIX1).t1x.bin $(PREFIX1).t2x.bin $(PREFIX1).t3x.bin \
		    $(BASENAME).$(PREFIX1).t1x $(BASENAME).$(PREFIX1).t2x $(BASENAME).$(PREFIX1).t3x

apertium_es_iadir=$(prefix)/share/apertium/apertium-$(PREFIX1)/

install-data-local: install-modes
	$(INSTALL_DATA) $(BASENAME).$(PREFIX1).t1x $(BASENAME).$(PREFIX1).t2x $(DESTDIR)$(apertium_es_iadir)
	$(INSTALL_DATA) $(BASENAME).$(PREFIX1).t3x $(DESTDIR)$(apertium_es_iadir)


CLEANFILES = -rf $(TARGETS)

test: all
	apertium-regtest test
