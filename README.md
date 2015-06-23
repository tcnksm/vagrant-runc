# Vagrant runC [![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)][license]

[license]: https://github.com/tcnksm/vagrant-runc/blob/master/LICENSE

Play with [runC](https://github.com/opencontainers/runc) on Ubuntu 14.04 by Vagrant.

## Usage

To start running and provisioning VM,

```bash
$ vagrant up
```

To login to VM,

```bash
$ vagrant ssh
```

To check installation, 

```bash
$ which runc
/usr/local/bin/runc
```

```bash
$ runc -v
runc version 0.1
```

## Example

```bash
$ docker run -d -p 80:80 nginx
```

```bash
$ docker export 5c675da33d6c > nginx.tar
```

To create rootfs,

```bash
$ mkdir rootfs
$ tar -xf nginx.tar -C rootfs
```

To generate a new OCP specification file,

```bash
$ runc spec > container.json
```

To enter container,

```bash
$ sudo runc container.json
# ps
PID TTY          TIME CMD
1 ?        00:00:00 sh
    6 ?        00:00:00 ps
```



