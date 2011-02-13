
<img src="http://lispnyc.org/static/images/theme-lispnyc.png" alt="lispnyc logo" title="LispNYC's webserver" />

# LispNYC's Webapplication Server

This is the jetty webserver configured for the use with the lispnyc-homebase 
webapp, also included is the Pebble blog webapp.

## Requirements

  * Java
  * build the [LispNYC Homebase Webapp](https://github.com/heow/lispnyc-homebase)

## Running

After the [LispNYC Homebase Webapp](https://github.com/heow/lispnyc-homebase) has been built and deployed here, just run:

  ./start
  
Then hit *http://localhost:8000*

## Jetty Details

The [Jetty Webserver](http://jetty.codehaus.org/jetty/contains) executes two webapps:

* [LispNYC Homebase Webapp](https://github.com/heow/lispnyc-homebase) 
* [Pebble Blog Webapp](http://pebble.sourceforge.net/)
 
Because the initial homepage of LispNYC is dynamic, the Homebase Webapp is the *main* application and thus runs as the main context.  This means that by default it intercepts all requests including ones for things like CSS, HTML and images.  There are several techniques to handle this, the one we chose is to set up a seperate context for static files and serve it up there, which is a typical scaling technique, by using Apache (or something else) for static files.

Pebble runs and serves up the blogs.

    uri path         handled by
    --------         ----------
    /static/         Jetty
    /blog/           Pebble Webapp
    /*               Homebase Webapp
