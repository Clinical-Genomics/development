# Conventions

> Code is read much more often than it is written. - A Wise Pythonista

[PEP8][pep8] and 💎 [PEP20][pep20] (``import this``) should be considered as the starting points. Unless specified otherwise, we follow the guidelines laid out there. For a brief overview, read the [Python Guide][python-guide#style]'s entry on the subject.

> The official guide has some very nice tips on [code layout][code-layout]. This can be a nice reference when you are unsure about how to e.g. style your hanging indents.

Futhermore, we use Python 3.7+. We encourage the use of type annotations (even if it doesn't cover 100% of your functions) and the new format strings:

```python
name = 'Paul Anderson'
string = f"Hello {name}!"
```

## Indentation

Use 4 *spaces* to indent code. Never use hard tabs. Spaces are preferred over tabs for the following reason: spaces are spaces on every editor on every operating system. Tabs can be configured to act as 2, 4, 8 "spaces" and this can make code unreadable when being shared.

## Maximum line length: 100 chars

Limit all lines to a maximum of 100 characters. Break down the line if it exceeds the maximum length. For example:

```python
# Python automatically concatenates consecutive strings
a_long_string = ("I am a very long string that can be split across"
                 "multiple lines by automatic string concatenation.")

# multi conditional if-statements can be split into multiple statements
# notice how the code reads a lot like regular English!
first_condition = 'genius' in 'Paul Thomas Anderson'
second_condition = 'genius' in 'Daniel Day-Lewis'

if first_condition and second_condition:
    print('And the Oscar goes to... There Will Be Blood!')
```

### Imports

I like to split up imports into three separate groups: 1. standard library imports, 2. third party imports, 3. intra-package imports.

```python
import os
import re

import numpy as np
from path import path

from .utils import read_config
```

### Variable names

PEP8 recommends to use short variable names. Achieving that can take some coding hygiene and some experience. Get more advice in our [variable hygiene section](./variables.md).

## Folders/packages

A common folder structure for a Python projects looks like:

```bash
myPackage
├── __init__.py
├── exc.py                   <-- custom exceptions
├── cli/
│   ├── __init__.py
│   ├── base.py              <-- read app config, set up logging, import subcommands
│   └── subcommand.py
├── server/
│   ├── templates/
│   ├── __init__.py
│   └── app.py
└── store/
    ├── __init__.py
    ├── api.py
    └── models.py            <-- database models, DB schema definitions
```

The important thing to note is how functionality is split up across the project. It's common that the same or similar functionality is available through many interfaces. For example it might be possible to list all recently added records in a database:

- on the command line printed to the console
- over HTTP through a JSON API
- programmatically through accessing an API class

The `cli` package contains all command line related code and nothing more. Logic such as how to handle and report error messages to the user goes here. **Avoid** putting logic in CLI modules that directly handle things like manually filtering database queries. More generally think [DRY][dry] - avoid doing the same thing manually in both CLI and server code. **Always** go through your Python API to interact with e.g. the database.

## Command line interface (CLI)

We highly recommend implementing the CLI using [Click][click]. It has a very nice Pythonic interface for defining your interface and comes with helpers for reading input, printing colorful output, etc.

## Logging

We recommend using [Coloredlogs][coloredlogs] which makes it _super easy_ to enable logging for your package:

```python
import coloredlogs
coloredlogs.install(level=log_level)
```

Read more in the [logging section](./logging.md)

## Server

If it makes sense, a general app exposes a JSON API over HTTP(S). This API can then be consumed by a client side web app. Sometimes it makes sense to provide a the web interface as part of the Python package and other times it will be consumed by the central web portal interface.

We write our web servers in [Flask][flask] which shares many similarities with [Click][click]. To connect to the store/backend we use [Flask-Alchy][flask-alchy].

We generally configure servers using environment variables which is a flexible and well supported option.

## Store

We start out with a SQL backend unless our needs require something different. We run all production SQL databases in MySQL. For development and testing it's often nice to work against a SQLite copy. For that reason and to make database interactions more pythonic, we make heavy use of the SQLAlchemy-wrapper, [Alchy][alchy].

> Note that Alchy has been **deprecated** in favor of SQLService, however, we have not been able to successfully set up the latter package with Flask to work with the request context which is why we stay with Alchy for now.

### Store API

Alchy shares the database connection with associated model classes. This allows you to perform queries by simply importing them like:

```python
# ... connect to database
from trailblazer.store import models

for record in models.Sample.query:
    print(record)
```

However, this feels a little magic and it's not so clear how the model exactly got access to that database connection. Therefore, we advocate explicitly passing around an API class holding the database connection.

```python
from . import models

class DatabaseAPI():
    Sample = models.Sample

    def __init__(self, uri):
        self.connect(uri)

    def samples(self):
        return self.Sample.query
```

## Exceptions

We recommend that you base all your custom exceptions on a app-specific exception class. This way, 3-party packages that depend on it easily catch all exceptions from your package if they so choose.

```python
class TrailblazerError(Exception):
    def __init__(self, message):
        self.message = message

class MissingFileError(TrailblazerError):
    pass
```

## Helpful tools

We encourage using a *linter* to continuously check the syntax of your code. The Python community maintains a number of linters such as pep8, and [PyFlakes][pyflakes].

If your repo has been set up with continous integration, with for example Travis, you can easily make linting part of the build process together with [Git-Lint][git-lint]. This will give you step wise improvements by automatic linting of those parts of the code that are new or changed. 

Another resource that can greatly ease collaboration is [EditorConfig][editor-config]. It's an effort to provide a cross editor configuration format and in placed in your project and committed to source control. You also need to install a plugin for your favorite editor, e.g. [Sublime][sublime-config].

[pep8]: http://legacy.python.org/dev/peps/pep-0008/
[pep20]: http://legacy.python.org/dev/peps/pep-0020/
[python-guide#style]: http://docs.python-guide.org/en/latest/writing/style/
[code-layout]: http://legacy.python.org/dev/peps/pep-0008/#code-lay-out
[dry]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[click]: http://click.pocoo.org/
[coloredlogs]: https://coloredlogs.readthedocs.io/en/latest/
[flask]: http://flask.pocoo.org/
[alchy]: http://alchy.readthedocs.io/en/latest/
[flask-alchy]: https://github.com/dgilland/flask-alchy
[pyflakes]: https://pypi.python.org/pypi/pyflakes
[editor-config]: http://editorconfig.org/
[sublime-config]: https://github.com/sindresorhus/editorconfig-sublime
[git-lint]: https://github.com/sk-/git-lint

