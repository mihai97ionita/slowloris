# SlowLoris attack proof of concept

## Added docker functionality 
Docker-compose to start a target container with a vulnerable server

## What is Slowloris?
Slowloris is basically an HTTP Denial of Service attack that affects threaded servers. It works like this:

1. We start making lots of HTTP requests.
2. We send headers periodically (every ~15 seconds) to keep the connections open.
3. We never close the connection unless the server does so. If the server closes a connection, we create a new one keep doing the same thing.

This exhausts the servers thread pool and the server can't reply to other people.

# NOTE

####PLEASE USE THIS ATTACK ONLY ON YOUR OWN PROPERTY 

#####The attempt of using such an attack on a real website is illegal under the Federal Computer Fraud and Abuse Act. Violators may be subjected to prison sentences of up to 10 years and a fine of up to $500,000.

## Requirements to run this locally 

* Docker
* Python 3

## How to run?

* `docker-compose up ` to build and run the target for the attack 

* `docker container ls ` to check if the containers are running or access ` http://localhost/ ` to see if the website is running

* `python slowloris.py 127.0.0.1` to start the attack with default value of 150 sockets

* `python slowloris.py 127.0.0.1 -s 2000` <- slow down of the website

* `python slowloris.py 127.0.0.1 -s 15000` <- makes the website almost unreachable   

* Check traffic and status of the containers using prometheus ` http://localhost:8181/ `

### SOCKS5 proxy support

However, if you plan on using the `-x` option in order to use a SOCKS5 proxy for connecting instead of a direct connection over your IP address, you will need to install the `PySocks` library (or any other implementation of the `socks` library) as well. [`PySocks`](https://github.com/Anorov/PySocks) is a fork from [`SocksiPy`](http://socksipy.sourceforge.net/) by GitHub user @Anorov and can easily be installed by adding `PySocks` to the `pip` command above or running it again like so:

* `sudo pip3 install PySocks`

You can then use the `-x` option to activate SOCKS5 support and the `--proxy-host` and `--proxy-port` option to specify the SOCKS5 proxy host and its port, if they are different from the standard `127.0.0.1:8080`.

## Configuration options
It is possible to modify the behaviour of slowloris with command-line arguments.

## License
The code is licensed under the MIT License.
