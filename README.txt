Dennis Guse, 2013

This git-repository is a clone of the original pjproject-svn (at the moment revision r4562).
It was created to:
1. make debian package building easier (configuration and small patches so it can be build for ubuntu)
2. add patches that didn't made it yet upstream

It was setup using the following command:
# git svn clone -r4650:HEAD http://svn.pjsip.org/repos/pjproject/trunk
and the portaudio-lib (also a git svn clone of the original svn-repo) important from 
# git submodule add https://github.com/dennisguse/portaudio.git third_party/portaudio

to clone the repository do this:
# git clone --recursive https://github.com/dennisguse/pjsip.git

By cloning the connection to "git svn" is lost. If you would like to use the "git svn rebase" for updates from upstream:
http://stackoverflow.com/questions/5339838/cloning-a-git-svn-repository-with-svn-metadata
If you don't know what it is: just ignore it.

################### Packaging

1. Setup build environment
# apt-get install packaging-dev
# export DIST=saucy
# pbuilder create or (git-pbuilder create)

2. Prepare to build
- (optional) Update changelog, if necessary
# git-dch -a -R
- Commit all changes (incl. changelog)!

3. Build
# export DIST=saucy

- for upload (signed source package); Use your PGP-Keyid:
# git-buildpackage --git-upstream-tree=XXX -git-ignore-branch --git-submodules --git-dist=saucy -S -k3103E9ED
- binary deb
# git-buildpackage --git-upstream-tree=XXX -git-ignore-branch --git-submodules --git-dist=saucy
- replace XXX to select the tree you want.

4. Clean
# git clean  -f -x -d
# git reset --hard

5. (optional) upload to launchpad
- replace XXX appropiately
# dput ppa:dennis.guse/sip-tools XXX.changes 

