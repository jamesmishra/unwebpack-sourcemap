# unwebpack-sourcemap

### Recover uncompiled TypeScript sources, JSX, and more from Webpack sourcemaps.

This is a Python command line application that parses Webpack sourcemaps and returns uncompiled TypeScript sources.

unwebpack-sourcemap can process source maps on the local filesystem, or it can discover source maps on a remote website.

## Introduction
If you're unfamiliar with source maps, you can read:
* ["Introduction to JavaScript Source Maps"][5] by Google Chrome Developers
* ["Use a source map"][6] by Firefox Source Docs

## Installation
### 1. Create a new Python virtualenv in a directory named `venv`.
```
python3 -m venv venv
```

### 2. Activate the virtualenv.
```
source venv/bin/activate
```

### 3. Install unwebpack-sourcemap from PyPI.
```
python3 -m pip install unwebpack-sourcemap
```
Note: unwebpack-sourcemap comes with Python dependencies that may conflict with the dependencies in your system installation of Python. That is why it is important to **always install unwebpack-sourcemap inside of a virtualenv,**
which won't make any changes to your surrounding system.

### 4. Try running unwebpack-sourcemap.
```
unwebpack-sourcemap --help
```

The below examples assume that you are inside of an **activated virtualenv**.

If you have installed unwebpack-sourcemap in a virtualenv, but want to avoid activating it, you can find the unwebpack-sourcemap command in the location `venv/bin/unwebpack-sourcemap`.

## Usage
These examples use the `--make-directory` flag to create a subdirectory named `output_dir`.
You can omit the `--make-directory` if you want to use an existing empty directory.

### Unpacking a sourcemap on the local filesystem
```
unwebpack-sourcemap --make-directory --local /path/to/source.map output_dir
```

### Unpacking a sourcemap on a remote website
```
unwebpack-sourcemap --make-directory https://pathto.example.com/source.map output_dir
```

### Unpacking a sourcemap on a remote website (*with autodetection*)
To attempt to read all `<script src>` on an HTML page, fetch JS assets, look for `sourceMappingURI`, and pull sourcemaps from remote sources:

This will:
1. read all of the `<script src=>` tags on an HTML page
2. fetch JavaScript assets
3. look for `sourceMappingURI` and pull the sourcemaps that are found.

To do this, the command is:
```
unwebpack-sourcemap --make-directory --detect https://pathto.example.com/spa_root/ output_dir
```

## License and credit
unwebpack-sourcemap was [originally][1] published by [rarecoil][2] under the [MIT license][3].

This repository is a fork of unwebpack-sourcemap maintained by [James Mishra][4] and packaged for PyPI.

This repository is also licensed under the MIT license.

[1]: https://github.com/rarecoil/unwebpack-sourcemap
[2]: https://github.com/rarecoil
[3]: https://github.com/rarecoil/unwebpack-sourcemap/blob/master/LICENSE
[4]: https://github.com/jamesmishra
[5]: https://developer.chrome.com/blog/sourcemaps/
[6]: https://firefox-source-docs.mozilla.org/devtools-user/debugger/how_to/use_a_source_map/index.html