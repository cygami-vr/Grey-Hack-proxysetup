# Grey-Hack-proxysetup

## What is this?
This is a series of scripts intended for use in the video game Grey Hack which expedites the setup of in-game proxy computers.

## Installation
1. Install `proxysetup` to `/bin`
2. Install `proxysetupremote` and `proxysetuplocal` to `/etc/proxysetup/`
3. Create your proxysetup configuration. Refer to the next section for detils.
4. Done! You are ready to run `proxysetup` from the command line.

## Configuration
1. Your configuration file will actually be a compiled program that should be saved as `/etc/proxysetup/Config` (no extension).
2. Here is an example source code snippet that could be compiled into the configuration file:

        routerInstall = {
        	"/lib/init.so": "/lib",
        	"/lib/net.so": "/lib",
        	"/path/to/kernel_router.so": "/lib",
        	"/path/to/libhttp.so": "/lib" }
    
        proxyInstall = {
            "/lib/init.so": "/lib",
            "/lib/net.so": "/lib",
            "/lib/metaxploit.so": "/lib",
            "/lib/crypto.so": "/lib",
            "/usr/bin/ScanLan.exe": "/usr/bin",
            "/path/to/libssh.so": "/lib" }

## Command syntax
proxysetup can be run in two ways:
1. To secure a proxy, run `proxysetup [ip] [root pw]`
2. To secure the proxy's router, run `proxysetup router [connection file name] [router root pw]`
  1. The connection file is created by the first command in the folder `/etc/proxy/` and can be renamed to something user-friendly. It defaults to the IP address.
  2. The connection file name should end in `.txt`, but do not include the extension when running `proxysetup router...`.

## What does this do?
This performs the following tasks on the proxy or router in question:
1. Updates the root password to a new random password
2. Installs binaries per the configuration file
   1. This should be used to replace the default lib files with more secure copies.
4. Deletes the `/etc/passwd` file and `/home/guest` directory
5. Removes all non-root permissions from the file system

## Roadmap
I'd like to make the following enhancements to the scripts:
1. Add an "update only" mode for updating libs but skip other tasks.
2. Add a third sub-command for installing an rshell-server.
3. Have the main script automatically compile the remote and local subscripts to simplify the install.
