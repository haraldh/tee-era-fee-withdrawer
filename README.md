# tee-era-fee-withdrawer

This is a reproducible build of https://github.com/matter-labs/era-fee-withdrawer
with the gramine runtime to be run on SGX in Azure.

## Reproduce the NixOS build
```bash
$ docker run --privileged -it -v .:/mnt nixos/nix:2.19.2
```
Inside the container:
```bash
$ echo 'experimental-features = nix-command flakes' >> /etc/nix/nix.conf
$ echo 'sandbox = true' >> /etc/nix/nix.conf
$ cd /mnt
$ nix build
$ cp result era-fee-withdrawer-azure.tar.gz
$ exit
```
## Build the Docker image
```bash
$ docker load < era-fee-withdrawer-azure.tar.gz
$ docker build --no-cache --progress=plain -t efw -f Dockerfile-azure .
```

Should output something like:
```bash
[...]

#9 6.572 Measurement:
#9 6.572     6ea6a97a1672e240050fe687425d96d45adf09a84fcd099976d51df11fb98fcf
[...]
```
as the github actions build does.
