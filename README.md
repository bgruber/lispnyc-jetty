
<img src="http://lispnyc.org/static/images/theme-lispnyc.png" alt="lispnyc logo" title="LispNYC's webserver" />

# LispNYC's Webapplication Server

The highly acclaimed lightweight Jetty webserver is configured for the
use with our LispNYC Homebase Webapp, also included is the Pebble blog
webapp.

## Requirements

  * Java
  * deploy the [LispNYC Homebase Webapp](https://github.com/heow/lispnyc-homebase)

## Running

After the [LispNYC Homebase Webapp](https://github.com/heow/lispnyc-homebase) has been built and deployed here, just run:

  ./start
  
Then hit [http://localhost:8000](http://localhost:8000)

## Jetty Details

The [Jetty Webserver](http://jetty.codehaus.org/jetty/contains) executes two webapps:

* [LispNYC Homebase Webapp](https://github.com/heow/lispnyc-homebase) 
* [Pebble Blog Webapp](http://pebble.sourceforge.net/)
 
Because the initial homepage of LispNYC is dynamic, the Homebase Webapp is the *main* application and thus runs as the main context.  This means that by default it intercepts all requests including ones for things like CSS, HTML and images ...which is not what we want.  

There are several techniques to handle this, the one we chose is to set up a seperate context for static files and serve it up there.  It's a typical scaling technique: using Apache (or something) for static files.

    uri path         handled by
    --------         ----------
    /static/         Jetty
    /blog/           Pebble Webapp
    /*               Homebase Webapp

# Pebble Details

The password for the default accounts is *password*
