#
# %CopyrightBegin%
# 
# Copyright Ericsson AB 1997-2009. All Rights Reserved.
# 
# The contents of this file are subject to the Erlang Public License,
# Version 1.1, (the "License"); you may not use this file except in
# compliance with the License. You should have received a copy of the
# Erlang Public License along with this software. If not, it can be
# retrieved online at http://www.erlang.org/.
# 
# Software distributed under the License is distributed on an "AS IS"
# basis, WITHOUT WARRANTY OF ANY KIND, either express or implied. See
# the License for the specific language governing rights and limitations
# under the License.
# 
# %CopyrightEnd%
#

include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Application version
# ----------------------------------------------------
include ../../vsn.mk
VSN=$(PARSETOOLS_VSN)
APPLICATION=parsetools

# ----------------------------------------------------
# Release directory specification
# ----------------------------------------------------
RELSYSDIR = $(RELEASE_PATH)/lib/$(APPLICATION)-$(VSN)

# ----------------------------------------------------
# Target Specs
# ----------------------------------------------------
XML_APPLICATION_FILES = ref_man.xml
XML_REF3_FILES = yecc.xml leex.xml

XML_PART_FILES = part_notes.xml
XML_CHAPTER_FILES = notes.xml

BOOK_FILES = book.xml

XML_FILES = \
	$(BOOK_FILES) $(XML_CHAPTER_FILES) \
	$(XML_PART_FILES) $(XML_REF3_FILES) $(XML_APPLICATION_FILES)

GIF_FILES = \
	note.gif

XML_HTML_FILES = \
	notes_history.xml

# ----------------------------------------------------

HTML_FILES = $(XML_APPLICATION_FILES:%.xml=$(HTMLDIR)/%.html) \
	$(XML_HTML_FILES:%.xml=$(HTMLDIR)/%.html) \
	$(XML_PART_FILES:%.xml=$(HTMLDIR)/%.html)

INFO_FILE = ../../info

MAN3_FILES = $(XML_REF3_FILES:%.xml=$(MAN3DIR)/%.3)

HTML_REF_MAN_FILE = $(HTMLDIR)/index.html

TOP_PDF_FILE = $(PDFDIR)/$(APPLICATION)-$(VSN).pdf

# ----------------------------------------------------
# FLAGS 
# ----------------------------------------------------
XML_FLAGS += 
DVIPS_FLAGS += 

# ----------------------------------------------------
# Targets
# ----------------------------------------------------
$(HTMLDIR)/%.gif: %.gif
	$(INSTALL_DATA) $< $@

docs: pdf html man

$(TOP_PDF_FILE): $(XML_FILES)

pdf: $(TOP_PDF_FILE)

html: gifs $(HTML_REF_MAN_FILE)

clean clean_docs:
	rm -rf $(HTMLDIR)/*
	rm -f $(MAN3DIR)/*
	rm -f $(TOP_PDF_FILE) $(TOP_PDF_FILE:%.pdf=%.fo)
	rm -f errs core *~

man: $(MAN3_FILES)

gifs: $(GIF_FILES:%=$(HTMLDIR)/%)

debug opt: 

# ----------------------------------------------------
# Release Target
# ---------------------------------------------------- 
include $(ERL_TOP)/make/otp_release_targets.mk

release_docs_spec: docs
	$(INSTALL_DIR) $(RELSYSDIR)/doc/pdf
	$(INSTALL_DATA) $(TOP_PDF_FILE) $(RELSYSDIR)/doc/pdf
	$(INSTALL_DIR) $(RELSYSDIR)/doc/html
	$(INSTALL_DATA) $(HTMLDIR)/* \
		$(RELSYSDIR)/doc/html
	$(INSTALL_DATA) $(INFO_FILE) $(RELSYSDIR)
	$(INSTALL_DIR) $(RELEASE_PATH)/man/man3
	$(INSTALL_DATA) $(MAN3DIR)/* $(RELEASE_PATH)/man/man3


release_spec:

