#
# Copyright (C) 2016-2017 Red Hat, Inc.  All rights reserved.
#
# Authors: Fabio M. Di Nitto <fabbione@kronosnet.org>
#
# This software licensed under GPL-2.0+, LGPL-2.0+
#

MAINTAINERCLEANFILES	= Makefile.in

include $(top_srcdir)/build-aux/check.mk
include $(top_srcdir)/libknet/tests/api-check.mk

EXTRA_DIST		= \
			  api-test-coverage \
			  api-check.mk

AM_CPPFLAGS		= -I$(top_srcdir)/libknet
AM_CFLAGS		= $(PTHREAD_CFLAGS)
LIBS			= $(top_builddir)/libknet/libknet.la \
			  $(PTHREAD_LIBS) $(dl_LIBS)

noinst_HEADERS		= \
			  test-common.h

# the order of those tests is NOT random.
# some functions can only be tested properly after some dependents
# API have been validated upfront.

check_PROGRAMS		= \
			  $(api_checks) \
			  $(int_checks) \
			  $(fun_checks)

int_checks		= \
			  int_crypto_test \
			  int_timediff_test

fun_checks		=

benchmarks		= \
			  crypto_bench_test \
			  knet_bench_test

noinst_PROGRAMS		= \
			  api_knet_handle_new_limit_test \
			  pckt_test \
			  $(benchmarks) \
			  $(check_PROGRAMS)

noinst_SCRIPTS		= \
			  api-test-coverage

TESTS			= $(check_PROGRAMS)

check-local: check-api-test-coverage

check-api-test-coverage:
	chmod u+x $(top_srcdir)/libknet/tests/api-test-coverage
	$(top_srcdir)/libknet/tests/api-test-coverage $(top_srcdir) $(top_builddir)

pckt_test_SOURCES	= pckt_test.c

int_crypto_test_SOURCES = int_crypto.c \
			  ../common.c \
			  ../crypto.c \
			  ../crypto_nss.c \
			  ../crypto_openssl.c \
			  ../logging.c \
			  test-common.c

int_crypto_test_CFLAGS	= $(nss_CFLAGS) $(openssl_CFLAGS)

int_timediff_test_SOURCES = int_timediff.c

crypto_bench_test_SOURCES = crypto_bench.c \
			    ../common.c \
			    ../crypto.c \
			    ../crypto_nss.c \
			    ../crypto_openssl.c \
			    ../logging.c \
			    test-common.c

crypto_bench_test_CFLAGS  = $(nss_CFLAGS) $(openssl_CFLAGS)

knet_bench_test_SOURCES	= knet_bench.c \
			  test-common.c \
			  ../common.c \
			  ../logging.c \
			  ../compat.c \
			  ../transport_common.c
