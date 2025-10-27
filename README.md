> [!IMPORTANT]
> This repo contains a fork of the original ``nest_asyncio`` package,
> which is no longer maintained as [its author has passed away](https://github.com/erdewit/ib_insync?tab=readme-ov-file#notice). :tulip:
>
> At this moment, this fork is not published at PyPI in any form.
>
> Notable changes from original code:
> - Added support for Python 3.14
> - Dropped support for old Python versions, minimum supported version is now 3.9.
> - Removed code for patching tornado asyncio loop.

# Introduction

By design asyncio [does not allow](https://github.com/python/cpython/issues/66435)
its event loop to be nested. This presents a practical problem:
When in an environment where the event loop is
already running it's impossible to run tasks and wait
for the result. Trying to do so will give the error
`RuntimeError: This event loop is already running`.

The issue pops up in various environments, such as web servers,
GUI applications and in Jupyter notebooks.

This module patches asyncio to allow nested use of `asyncio.run` and
`loop.run_until_complete`.

## Installation


```console
$ pip3 install nest_asyncio
```

Python 3.9 or higher is required.

### Usage

```python
import nest_asyncio
nest_asyncio.apply()
```

Optionally the specific loop that needs patching can be given
as argument to `apply`, otherwise the current event loop is used.
An event loop can be patched whether it is already running
or not.

> [!IMPORTANT]
> Only event loops from asyncio can be patched;
> loops from other projects, such as uvloop or quamash,
> generally can't be patched.
