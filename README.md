# PeerVPN

This one is made to prepare a build environment for the app, build it, create an http-accessible apt repo on it \
and install builded app anywhere.

## Requirements
------------

Ubuntu bionic with ssh access to it (assumed root access by ssh-key, but you can use become if you wish).
Packages to be installed by this playbook:
  - make 
  - gcc 
  - git 
  - libssl1.0-dev 
  - zlib1g-dev

Packages for repo:
  - dpkg-dev
  - nginx


## Example Playbooks
----------------
The `peervpn.yml` is a main one. It consists of few tasks-files and some variables (it also possible to set them in `defaults`). \
The `peervpn_install.yml` in it's turn is useful to only `install` peervpn app from repo (you should place a better repo url i think), \
like that `ansible-playbook -i inventory.yml peervpn_install.yml -e target=ubuntu`. It also possible to run `peervpn.yml` playbook \
to only install the app using tag `ansible-playbook -i inventory.yml peervpn.yml -e target=ubuntu -vv -t install_peervpn`. 

## Running from scratch
-----------------
Edit `inventoy.yml` file to point:
 - VM`s IP
 - ansible_user is root (set `become = yes` in playbook if you wish to not use root)

After that just run `ansible-playbook -i inventory.yml peervpn.yml -e target=ubuntu`

That's it!

## Advanced
----------------
The `advanced` directory consists of `Dockerfile` which point is build .deb package and push it using `dput` command to remote \
repo server running via `mini-dinstall`. `Mini-dinstall` is automated apt-repository manager but it utilyze the `changelog` files \
and this is why i decided to not use it for the project. But, in real production environment, where you want to build packages \
in isolated environments (Docker/chroot/jail...) it must be pushed to repo remotely. \
BTW: dockerfile is ready and produce .deb package on it's local FS but not run `dput`.

