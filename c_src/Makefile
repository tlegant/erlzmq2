DEPS=../deps

unams=$(shell uname -s)
ZMQ_FLAGS=

ifeq ($(unams),Linux)
ZMQ_FLAGS=--with-pic
endif

ifeq ($(unams),FreeBSD)
ZMQ_FLAGS=--with-pic
CC=gcc
CXX=g++
endif

ifndef ZEROMQ_VERSION
ZEROMQ_VERSION=3.2.2
endif

all: $(DEPS)/zeromq3/src/.libs/libzmq.a

clean:
	if test -e $(DEPS)/zeromq3/Makefile; then \
		cd $(DEPS)/zeromq3; $(MAKE) clean; \
	else \
		true; \
	fi

distclean:
	@rm -rf $(DEPS)

$(DEPS)/zeromq3:
	@mkdir -p $(DEPS)
	@curl -L https://archive.org/download/zeromq_$(ZEROMQ_VERSION)/zeromq-$(ZEROMQ_VERSION).tar.gz -o $(DEPS)/zeromq-$(ZEROMQ_VERSION).tar.gz
	@cd $(DEPS) && tar xzvfp zeromq-$(ZEROMQ_VERSION).tar.gz && mv zeromq-$(ZEROMQ_VERSION) zeromq3

$(DEPS)/zeromq3/src/.libs/libzmq.a: $(DEPS)/zeromq3
	@cd $(DEPS)/zeromq3 && ./configure $(ZMQ_FLAGS) && $(MAKE)
