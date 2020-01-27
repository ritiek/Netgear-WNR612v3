# Netgear-WNR612v3

Source rootfs for Netgear WNR612 v3 Router Firmware v1.0.0.18


## Retrieving Files

I was able to retrieve files using telnet and router's HTTP service.

```
$ telnet 192.168.1.1
```
User and password are both `root`.

The below to be run via telnet:
```
# ps
  PID  Uid        VSZ Stat Command
  ....
   10 root            SW< [mtdblockd]
   27 root       2504 SW  /usr/sbin/mini_httpd -d /usr/www -c /cgi-bin/* -u roo
   31 root       1796 SW  -sh
  .....

# kill -9 27
# /usr/sbin/mini_httpd -d <directory/on/router/>
```

And then, wgetting the served directory on the main machine:
```
$ wget -r --tries=3 http://192.168.1.1/
```

I wanted to retrieve an .img file for `/dev/root`, but I couldn't make one. The
router runs `ash` shell with very limited BusyBox applets being available. I also
failed to execute any manually cross-compiled binaries for MIPS(?) platform on the
router.
