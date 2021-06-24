TARGETNAME = migration
OUTDIR ?= bin

SWIFTC = xcrun -sdk iphoneos swiftc -target arm64-apple-ios11.0
CC = xcrun -sdk iphoneos clang -arch arm64
ifneq (,$(wildcard /opt/procursus/bin/ldid))
LDID = /opt/procursus/bin/ldid
else
LDID = ../amfidebilitate/ldid
endif

.PHONY: all clean

all: $(OUTDIR)/$(TARGETNAME)

SWIFTFLAGS =
CFLAGS =

DEBUG ?= 1
ifeq (($DEBUG), 1)
	SWIFTFLAGS += -D DEBUG
	CFLAGS += -DDEBUG
else
	SWIFTFLAGS += -O
	CFLAGS += -O3
endif

$(OUTDIR):
	mkdir -p $(OUTDIR)

$(OUTDIR)/$(TARGETNAME): main.swift | $(OUTDIR)
	$(SWIFTC) -o $@ $^ $(SWIFTFLAGS)
	strip $@
	$(LDID) -K../amfidebilitate/signcert.p12 -Sent.plist $@

clean:
	rm -f $(OUTDIR)/$(TARGETNAME)

