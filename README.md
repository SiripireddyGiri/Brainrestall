# BrainRest – Simple README
Simple guide to create .deb package and local APT repo.

-------------------------------------------------------
1. Make project folders
-------------------------------------------------------
mkdir -p Brainrestall/repo/dists/stable/main/binary-amd64
mkdir -p Brainrestall/repo/pool/main/b
mkdir -p Brainrestall/brainrest-1.0.0/DEBIAN
mkdir -p Brainrestall/brainrest-1.0.0/usr/bin
mkdir -p Brainrestall/brainrest-1.0.0/usr/share/man/man1

-------------------------------------------------------
2. Add control file
-------------------------------------------------------
File: Brainrestall/brainrest-1.0.0/DEBIAN/control

Content:
Package: brainrest
Version: 1.0.0
Section: utils
Priority: optional
Architecture: amd64
Maintainer: Siripireddygiri
Description: Simple micro-break reminder tool

-------------------------------------------------------
3. Add main script
-------------------------------------------------------
Place your script here:
Brainrestall/brainrest-1.0.0/usr/bin/brainrest

Make it executable:
chmod 755 Brainrestall/brainrest-1.0.0/usr/bin/brainrest

-------------------------------------------------------
4. Add man page
-------------------------------------------------------
Place file:
Brainrestall/brainrest-1.0.0/usr/share/man/man1/brainrest.1.gz

-------------------------------------------------------
5. Build .deb package
-------------------------------------------------------
cd Brainrestall
dpkg-deb --build brainrest-1.0.0

Move .deb to repo:
mv brainrest-1.0.0.deb repo/pool/main/b/

-------------------------------------------------------
6. Create Packages file
-------------------------------------------------------
cd repo
dpkg-scanpackages pool /dev/null > dists/stable/main/binary-amd64/Packages
gzip -k dists/stable/main/binary-amd64/Packages

-------------------------------------------------------
7. Create Release file
-------------------------------------------------------
File: repo/dists/stable/Release

Content:
Origin: Brainrest Repo
Suite: stable
Codename: stable
Architectures: amd64
Components: main
Description: Local repository for BrainRest

-------------------------------------------------------
8. Add repo to system
-------------------------------------------------------
sudo nano /etc/apt/sources.list.d/brainrest.list

Add line:
deb [trusted=yes] file:/home/siripireddy/Brainrestall/repo stable main

-------------------------------------------------------
9. Update APT
-------------------------------------------------------
sudo apt update

-------------------------------------------------------
10. Install package
-------------------------------------------------------
sudo apt install brainrest

-------------------------------------------------------
11. Run BrainRest
-------------------------------------------------------
brainrest
