
CC=gcc
CXX=g++
CFLAGS=-O2 -fpic -ggdb


.c.o:
	@rm -f $@
	$(CC) $(CFLAGS) -c $*.c

.cc.o:
	@rm -f $@
	$(CXX) $(CFLAGS) -c $*.cc

OFILES = thttpd.o libhttpd.o fdwatch.o timers.o pprof.o 

ALL = libghttpd.a libghttpd.so libghttpd-preload.so

CLEANFILES =	$(ALL) *.o	

all:		$(ALL)

libghttpd.a: $(OFILES)
	@rm -f $@
	ar rvc $@ $(OFILES)

libghttpd.so: $(OFILES)
	@rm -f $@
	$(CC) -shared -o $@ $(OFILES) -L/usr/local/lib -ldl -lpthread -ltcmalloc -lprofiler -lstacktrace

libghttpd-preload.so: $(OFILES) autostart.o
	@rm -f $@
	$(CC) -shared -o $@ $(OFILES) autostart.o -L/usr/local/lib -ldl -lpthread -ltcmalloc -lprofiler -lstacktrace

install:	$(ALL)
	cp $(ALL) /usr/local/lib
	cp gperftools-httpd.h /usr/local/include

clean:
	rm -f $(CLEANFILES)

distclean:
	rm -f $(CLEANFILES)

thttpd.o:	config.h version.h libhttpd.h fdwatch.h timers.h 
libhttpd.o:	config.h version.h libhttpd.h timers.h 
fdwatch.o:	fdwatch.h
timers.o:	timers.h

