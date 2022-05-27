---
title: Using mkosi-initrd with OpenSUSE Tumbleweed
SPDX-License-Identifier: LGPL-2.1-or-later
---

# Building an initramfs image

Some tools are required: `cpio`, `zstd`, `python38`, `python38-xattr`, a
development version of `mkosi` from git, and the `mkosi-initrd` repository
with configuration for `mkosi`.

```bash
sudo zypper install zstd cpio python38 python38-xattr
git clone https://github.com/systemd/mkosi
git clone https://github.com/systemd/mkosi-initrd
cd mkosi-initrd
```

The initrd is built for a specific kernel version.
We provide 2 setting files:

- `opensuse-tumbleweed.mkosi` should produce an image that is about 186.7 MB and contains all kernel modules.
- `opensuse-tumbleweed-base.mkosi` should produce an image that is about 66.8 MB and contains only the base kernel modules.

We pass `KERNEL_VERSION=…` to tell the `kernel-install` scripts what version to install.

```bash
KVER=`uname -r`
sudo PYTHONPATH=$PWD/../mkosi python3 -m mkosi -f --default opensuse-tumbleweed.mkosi --finalize-script=opensuse-tumbleweed.mkosi.finalize --image-version=$KVER --environment=KERNEL_VERSION=$KVER
```

Hint: on repeated runs, it may be useful to add `--with-network=never` if no new packages need to be downloaded.

# Installing the initramfs image

Add a new grub2 entry using `/etc/grub.d/40_custom`

# Building system extension images
TODO: TBD

# Verity and signatures

TODO: TBD
