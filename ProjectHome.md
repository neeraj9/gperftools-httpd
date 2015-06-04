Gperftools-httpd is a simple HTTP server, based on thttpd, that enables remote profiling via Google's pprof (see google-perftools).

This code is not from Google.  It is a copy of thttpd 2.25b
but then adapted to be a tiny minimal HTTP server
that can be linked into any program to serve
profiling information for pprof.

It has been chopped up significantly compared to the original.

After running make (which assumes you have the google-perftools
libraries installed in /usr/local/lib or a standard place like /usr/lib),
you can profile an arbitrary program with:

> LD\_PRELOAD=/usr/local/lib/libghttpd-preload.so ./a.out

and then while it is running, execute:

> pprof a.out http://localhost:9999/pprof/heap

The preload library starts the HTTP server at the first call
to malloc.  Alternately, you can link with -lghttpd and call ghttpd()
during program initialization (e.g., in main).

You can change the port number by setting the environment
variable GHTTPPORT:

> GHTTPPORT=12345 LD\_PRELOAD=libghttpd-preload.so ./a.out

