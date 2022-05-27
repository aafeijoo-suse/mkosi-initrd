# mkosi-initrd — Build Initrd Images Using Distro Packages

Very brief instructions:
```
cd ~/src
git clone https://github.com/systemd/mkosi
git clone https://github.com/systemd/mkosi-initrd
cd mkosi-initrd
mkdir mkosi.cache
KVER=$(uname -r)
. /etc/os-release
sudo PYTHONPATH=$HOME/src/mkosi python3 -m mkosi -f --default $ID.mkosi --finalize-script=$ID.mkosi.finalize --image-version=$KVER --environment=KERNEL_VERSION=$KVER -o initrd-$KVER.cpio.zstd

```

Requirements:
- mkosi >= 10
- systemd >= 249
- util-linux >= 2.37
