include ../common.mak

CFLAGS  = -Os -Wall $(EXTRACFLAGS) -ffunction-sections -fdata-sections -Wsign-compare
CFLAGS += -I$(SRCBASE)/include -I$(TOP)/shared -I$(TOP)/nvram$(BCMEX)
LDFLAGS = -ffunction-sections -fdata-sections -Wl,--gc-sections -L$(TOP)/shared -L$(TOP)/nvram$(BCMEX)
LIBS    = -lshared -lnvram $(EXTRALIBS)

ifeq ($(TOMATO_EXPERIMENTAL),1)
 export CFLAGS += -DDEBUG_LOGMSG
endif

OBJS = cstats.o

all: cstats

%.o: %.c
	@echo " [cstats] CC $@"
	@$(CC) $(CFLAGS) -o $@ -c $<

cstats: $(OBJS)
	@echo " [cstats] CC $@"
	@$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS) $(LIBS)
	$(SIZECHECK)
	$(CPTMP)

install: all
	@echo " [cstats] Installing as $(INSTALLDIR)/bin/cstats"
	@install -D -m 0700 cstats $(INSTALLDIR)/bin/cstats
	@$(STRIP) $(INSTALLDIR)/bin/cstats
	@chmod 0500 $(INSTALLDIR)/bin/cstats

clean:
	@rm -f cstats *.o
