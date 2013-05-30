install_name\_prefix\_tool
========================

Shell script for Mac OS X which changes the library prefix for a series of shared libraries in a folder.

Overview
--------

This is a simple bash script which processes a series of Mac OS X shared libraries (.dylib) in a directory and uses [install\_name\_tool](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/install_name_tool.1.html) to modify the binary library link names.

The use-case for this script is usually to modify a series of existing shared libraries for loading from a relative location.

Example
-------

Say you have a couple of libraries which dependent upon each other and installed them in a directory "/usr/local/lib/".

Now you want to package these libraries with your main application. If you check each libraries link dependencies using "otool -L [LIBRARY_FILE]", you'll notice they point to "/usr/local/lib/".

Using this script, you can now modify all of the library links at once for instance to some local folder next to the main binary. If you copy all libraries to a "lib/" folder next to your main application binary, you can run the following command to make all shared libraries load and reside in "lib/".
<pre>
$ install_name_prefix_tool.sh ./lib /usr/local/lib @executable_path/lib
</pre>

If you now verify the links using otool again, you'll notice that it now uses the new prefix to lookup dependent libraries.

Handy, ain't it?