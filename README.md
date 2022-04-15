Ninjam Server Script Helpers
----------------------------

Helper scripts for installing a ninjam server on macOS or Linux

## Dependencies

#### MacOS

* Xcode command line tools

#### Ubuntu/Debian

* `sudo apt-get install build-essential`

#### Other linux

Install standard build tools (make, gcc, etc). That should be about it.

## Building and Installing

Run `bin/build` to clone ninjam and build the server. On success an application binary
`ninjamsrv` should be produced in this repo's checkout location.

Run `sudo bin/install` to copy application binary and config file to recommended locations.
On Linux this script also installs a `systemd` service (see below for more details).

Run `bin/clean` to clean up build artifacts including the server application binary.

## Configuring

A default configuration file `config.cfg` is provided. It is recommended you at least
change the default admin password before deploying the server.

If you change the configuration file after starting the server application, you'll need
to restart the server (see "Running" section below).

On linux it's recommended to keep in e.g. `/etc/ninjam/config.cfg` by default. If you're
using the `bin/install` script - be sure to edit that copy of the file going forward.

## Running

The server application can be run manually from the command line in the checkout directory 
with the default configuration file:

`./ninjamsrv config.cfg`

Or, if you successfuly ran `bin/install`:

`ninjamsrv /etc/ninjam/config.cfg`

However this is not ideal for a deployed server since you don't want to have to ssh in
every time to start it.

#### MacOS

TODO

#### Linux

On Linux we can use any number of service management systems to start the server on
system boot and manage it using common commands. The install script installs the server
as a `systemd` service, which will start automatically on boot once the network is available.
The service can be manually managed with the following commands:

`sudo systemctl (start|stop|restart) ninjam` -- start/stop/restart service

`systemctl status ninjam` -- Get service status

`journalctl -u ninjam` -- Show logs
