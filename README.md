# Install python3.10 on Debian
How to install python 3.10 with venv on Debian

Python 3.10 isn't in Debian stable since Buster and neither is it in Sid since 2024. Instead of installing files from the internet that some guy uploaded we'll use a snapshot for Debian Sid here.

First we'll add the snapshot to sources.list.

**/etc/apt/sources.list**
>deb [check-valid-until=no] https://snapshot.debian.org/archive/debian/20240326T090155Z/ sid main<br />
>deb-src [check-valid-until=no] https://snapshot.debian.org/archive/debian/20240326T090155Z/ sid main

Then we'll add some preferences to prevent apt from installing any files from this snapshot that we haven't asked for.

**/etc/apt/preferences**
>Package: *<br />
Pin: release a=unstable<br />
Pin-Priority: 1<br />

Here comes the tricky part though, python3.10-venv depends on python3.10-distutils, a package that only existed in the right name and version back in Debian Buster. So instead we break the earlier rule of not downloading packages from the net and grab python3.10-distutils-bogus_1.0_all.deb. This is a meta package that says "python3.10-distuilts is installed". Unzip the .deb file and look at what it contains, or even better make it yourself with [equivs](https://packages.debian.org/search?keywords=equivs). If you trust me (which you shouldn't) download the .deb file and install it with apt.

>sudo apt install ./python3.10-distutils-bogus_1.0_all.deb

After this we can install python3.10-minimal and python3.10-venv and we're ready to go.

>sudo apt install python3.10-minimal python3.10-venv
