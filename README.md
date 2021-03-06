# OMERO PyFileSystem2 implementation
[![Build Status](https://travis-ci.com/manics/fs-omero-pyfs.svg?branch=master)](https://travis-ci.com/manics/fs-omero-pyfs)
[![PyPI](https://img.shields.io/pypi/v/fs-omero-pyfs)](https://pypi.org/project/fs-omero-pyfs/)

A [Python filesystem abstraction](https://www.pyfilesystem.org/) layer that stores files in [OMERO](https://www.openmicroscopy.org/omero/).


## Installation

```
pip install fs-omero-pyfs
```


## Example

```python
import fs
fs_url = 'omero://{username}:{password}@{omerohost}'
root = fs.open_fs(fs_url)
```

OMERO websockets are supported:
```python
fs_url = 'omero+wss://{username}:{password}@{omerohost}/omero-ws'
```

Caching is highly recommended.
`cache_ttl` is specified in seconds, `0` disables caching.
```python
fs_url = 'omero://{username}:{password}@{omerohost}?cache_ttl=120'
```

The OMERO group can be changed by passing a query parameter `groupid=1234`.


## Development notes

Directories are stored as `TagAnnotation`s in a dedicated namespace.
Sub-directories are linked by an `AnnotationAnnotationLink` to the parent directory.

Files are stored as `OriginalFile`s, linked by an `OriginaFileAnnotationLink` to the parent directory.
The `path` property of the `OriginalFile` is ignored, only `name` is used.
