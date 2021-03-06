carbon-relay-ng
===============

Installation
------------

The Debian way (Ubuntu 12.04 only):

    echo "deb http://packages.rcrowley.org precise main" | sudo tee /etc/apt/sources.list.d/rcrowley.list
    sudo wget -O /etc/apt/trusted.gpg.d/rcrowley.gpg http://packages.rcrowley.org/keyring.gpg
    sudo apt-get update
    sudo apt-get -y install carbon-relay-ng

The Go way:

    go get github.com/rcrowley/carbon-relay-ng

Usage
-----

<pre><code>carbon-relay-ng [-f] [-l [<em>ip</em>]:<em>port</em>] [<em>pattern</em>]=[<em>ip</em>]:<em>port</em>[...]</code></pre>

* `-f`: relay only to the first matching route
* <code>-l [<em>ip</em>]:<em>port</em></code>: listen address (default: `0.0.0.0:2003`)

Examples
--------

Send production and staging data to different `carbon-cache.py` instances:

    carbon-relay-ng -f \\.staging\\.=1.2.3.4:2003 \\.production\\.=5.6.7.8:2003

Note the use of `-f` to relay data only to the first matching route.

Fanout to multiple processors:

    carbon-relay-ng =:2003 =5.6.7.8:2003

Repeatedly reading the most recent data points in a Whisper file is silly.  This pattern allows alerting and event processing systems to act on the data as it is received.
