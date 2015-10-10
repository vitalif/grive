# Grive2 0.4.2-dev

10 Oct 2015, Vitaliy Filippov

http://yourcmc.ru/wiki/Grive2

This is the fork of original "Grive" (https://github.com/Grive/grive) Google Drive client
with the support for the new Drive REST API and partial sync.

Grive can be considered still beta or pre-beta quality. It simply downloads all the files in your
Google Drive into the current directory. After you make some changes to the local files, run
grive again and it will upload your changes back to your Google Drive. New files created locally
or in Google Drive will be uploaded or downloaded respectively. Deleted files will also be "removed".
Currently Grive will NOT destroy any of your files: it will only move the files to a
directory named .trash or put them in the Google Drive trash. You can always recover them.

There are a few things that Grive does not do at the moment:
- continously wait for changes in file system or in Google Drive to occur and upload.
  A sync is only performed when you run Grive, and it calculates checksums for all files every time.
- symbolic links support.
- support for Google documents.

These may be added in the future, possibly the next release.

You need the following libraries:

- yajl
- libcurl
- libstdc++
- libgcrypt
- Boost (Boost filesystem, program_options, regex, unit_test_framework and system are required)
- expat

There are also some optional dependencies:
- CppUnit (for unit tests)
- libbfd (for backtrace)
- binutils (for libiberty, required for compilation in OpenSUSE, Ubuntu, Arch and etc)

Grive uses cmake to build. Basic install sequence is

    mkdir build
    cd build
    cmake ..
    make -j4
    sudo make install

For the detailed instructions, see http://yourcmc.ru/wiki/Grive2#Installation

When Grive is run for the first time, you should use the "-a" argument to grant
permission to Grive to access to your Google Drive. A URL should be printed.
Go to the link. You will need to login to your Google account if you haven't
done so. After granting the permission to Grive, the browser will show you
an authenication code. Copy-and-paste that to the standard input of Grive.

If everything works fine, Grive will create .grive and .grive_state files in your
current directory. It will also start downloading files from your Google Drive to
your current directory.

Enjoy!

## Version History

### Grive2 v0.4.2 (unreleased)

- Option to exclude files by perl regexp
- Reimplemented HTTP response logging for debug purposes
- Use multipart uploads (update metadata and contents at the same time) for improved perfomance & stability
- Bug fixes

### Grive2 v0.4.1

- Bug fixes

### Grive2 v0.4.0

First fork release, by Vitaliy Filippov / vitalif at mail*ru
- Support for the new Google Drive REST API (old "Document List" API is shut down by Google 20 April 2015)
- REAL support for partial sync: syncs only one subdirectory with `grive -d subdir`
- Major refactoring - a lot of dead code removed, JSON-C is not used anymore, API-specific code is split from non-API-specific
- Some stability fixes from Visa Putkinen https://github.com/visap/grive/commits/visa
- Slightly reduce number of syscalls when reading local files.

### Grive v0.3

Bug fix & minor feature release. Fixed bugs:
- #93: missing reference count increment in one of the Json constructors
- #82: retry for HTTP error 500 & 503
- #77: Fixed a bug where grive crashed on the first run.

New features:
- #87: support for revisions
- #86: ~~partial sync (contributed by justin at tierramedia.com)~~ that's not partial sync,
  that's only support for specifying local path on command line
