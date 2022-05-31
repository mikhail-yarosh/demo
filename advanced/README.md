/etc/mini-dinstall/mini-dinstall.conf:
```
[DEFAULT]
archive_style = flat
archivedir = /var/packages
logfile = /var/log/mini-dinstall.log

verify_sigs = 0
mail_to = root@localhost.int

generate_release = 1
release_origin = localhost.int
release_codename = stable

[internal]
release_label = Internal Packages
```

This command must be wrapped as a systemd service:
`mini-dinstall -v -d -c /etc/mini-dinstall/mini-dinstall.conf`


/root/.dput.cf:
```
[internal]
fqdn = 192.168.122.9
incoming = /var/packages 
method = internal
run_dinstall = 0
post_upload_command = mini-dinstall -r
```

dput internal peervpn_0.44-0_amd64.deb

debian/changelog (sample) :
```
peervpn (0.44) internal; urgency=medium
* Initial release. (Closes: #nnnn)  <nnnn is the bug number of your ITP>
-- Josip Rodin <joy-mg@debian.org>  Mon, 22 Mar 2010 00:37:31 +0100
```

