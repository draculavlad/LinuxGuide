### enable ubuntu server 18.04 kernel-based virtualization with web gui [kimchi]

# update system
```bash
sudo apt update -y
sudo apt upgrade -y
```

# check cpu availability for virtualization
```bash
sudo apt install cpu-checker -y
sudo kvm-ok
```

## result expectation(please enable vt-d in bios config):
INFO: /dev/kvm exists
KVM acceleration can be used

# enable universe & multiverse repo(it's a bug in early releases of ubuntu server 18.04)
```bash
sudo add-apt-repository universe
sudo add-apt-repository multiverse
```

# install virtualization related libs and tools 
```bash
sudo apt install qemu qemu-kvm libvirt-bin libvirt-clients libvirt-daemon-system bridge-utils virt-manager -y
```

# install nginx for kimchi
```
sudo apt-get install nginx -y
```

# download wok & related plugins
```bash
wget https://github.com/kimchi-project/kimchi/releases/download/2.5.0/wok-2.5.0-0.noarch.deb
wget http://kimchi-project.github.io/gingerbase/downloads/latest/ginger-base.noarch.deb
wget https://github.com/kimchi-project/kimchi/releases/download/2.5.0/kimchi-2.5.0-0.noarch.deb
```

# install wok & giner-base
```bash
sudo dpkg -i wok-2.5.0-0.noarch.deb
sudo apt --fix-broken install
sudo dpkg -i ginger-base.noarch.deb
sudo apt --fix-broken install
sudo systemctl restart wokd
sudo init 6
```

# modify kimchi debian package depencies list and install python-pil
# due to one of kimchi's dependency, python-imaging, is renamed to python-pil in python3 while python3 is the default python sdk in Ubuntu 18.04 
```bash
mkdir kimchi-work-dir
mv kimchi-2.5.0-0.noarch.deb kimchi-work-dir/
cd kimchi-work-dir
ar x kimchi-2.5.0-0.noarch.deb
rm kimchi-2.5.0-0.noarch.deb
tar zxf control.tar.gz
rm control.tar.gz
sed -i 's|python-imaging||g' control
tar --ignore-failed-read -cvzf control.tar.gz control.in Makefile Makefile.am Makefile.in control
rm control.in
rm Makefile
rm Makefile.am
rm Makefile.in
ar rcs kimchi-2.5.0-0.modified.noarch.deb debian-binary control.tar.gz data.tar.xz
```

# install kimchi & reboot
```
sudo dpkg -i kimchi-2.5.0-0.modified.noarch.deb
sudo init 6
```
