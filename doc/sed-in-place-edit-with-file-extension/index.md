# Sed in-place edit with file extension

The `sed` command has a `-i` option for in-place edit. 

Example:

```sh
$ sed -i.backup 's/x/y/' example.txt
```

The GNU `sed` implementation can omit the extension:

```sh
$ sed -i 's/x/y/' example.txt
```

The macOS `sed` implementation of `-i` requires an extension, otherwise `sed` fails:

```sh
$ sed -i 's/x/y/' example.txt
sed: 1: "environment": invalid command code e
```

A macOS workaround is to use a blank extensions:

```sh
$ sed -i '' 's/x/y/' example.txt
```

But that workaround fails on Linux.

Therefore our coding style is to provide an extension, then delete the file.

We use the file extension `tmp` to indicate the file is a temporary file.

Example:

```sh
$ sed -i.tmp 's/x/y/' example.txt; rm example.tmp
```
