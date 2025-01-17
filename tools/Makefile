# Copyright (c) 2022 Lorenzo Salvadore <salvadore@FreeBSD.org>
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE AUTHOR AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED.  IN NO EVENT SHALL THE AUTHOR OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.
#
# Makefile targets:
# all		make build test
# build		make _index.adoc
# test		run many checks on _index.adoc and reports
# autofix	fix all errors reported by test that can be fixed automatically

ALL_REPORTS=	${TeamReports} \
		${Projects} \
		${Userland} \
		${Kernel} \
		${Architectures} \
		${Documentation} \
		${Ports} \
		${ThirdParty} \
		${Miscellaneous} \

SEPARATOR_STRING?=	==========================================
ERROR_STRING?=		[ERROR]
WARNING_STRING?=	[WARNING]

TOOLS_DIR=	../tools

TITLE_LEVEL=	===

all: build test

build: _index.adoc

# Use ! instead of : because the content of _index.adoc is independent from the
# content of the .adoc files, but we still want to check for their existence
_index.adoc!	intro.adoc \
		${TeamReports} \
		${Projects} \
		${Userland} \
		${Kernel} \
		${Architectures} \
		${Documentation} \
		${Ports} \
		${ThirdParty} \
		${Miscellaneous}
	${RUBY_CMD} ${RUBY_FLAGS} ${TOOLS_DIR}/generate-index.rb \
		${START} \
		${STOP} \
		${YEAR} \
		${QUARTER} \
		"${TeamReports}" \
		"${Projects}" \
		"${Userland}" \
		"${Kernel}" \
		"${Architectures}" \
		"${Documentation}" \
		"${Ports}" \
		"${ThirdParty}" \
		"${Miscellaneous}" > $@

test:	check_all-reports \
	check_pluses \
	check_titles

autofix:	fix_pluses \
		fix_titles

clean:
	rm -f _index.adoc

.include "Makefile.commands"
.include "tests/Makefile.all-reports"
.include "tests/Makefile.pluses"
.include "tests/Makefile.titles"
