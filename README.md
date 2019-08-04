# Hacked for mingw-w64

Enough build instructions to get cracklib-check working. [BLFS](http://www.linuxfromscratch.org/blfs/view/svn/postlfs/cracklib.html)
has some helpful info. This "works for me"...

```sh
export LC_ALL=C
make -C words cracklib-words
cd src
./autogen.sh
./configure --enable-static --disable-shared --disable-nls --without-python --without-zlib --with-default-dict=C:/Dict/pw_dict
make
PATH="./util:$PATH" util/create-cracklib-dict ../words/cracklib-words
make distclean
./configure --build=i686-pc-cygwin --host=i686-w64-mingw32 --enable-static --disable-shared --disable-nls --without-python --without-zlib --with-default-dict=C:/Dict/pw_dict
make
echo password | util/crack-lib-check
```

Not sure why `fread` is failing, or why the database needs to be generated on Cygwin and copied for mingw, but these are worries
for another person or another day...

# cracklib

CrackLib Library and Dictionaries

  * src - Cracklib distribution itself
  * words - scripts and content to build a full size password dictionary

## translations

We use Fedora's Zanata for
[our translations](https://fedora.zanata.org/project/view/cracklib). Please
contribute translations for your language there.
