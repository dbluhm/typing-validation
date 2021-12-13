# Template for Python repositories

[![Generic badge](https://img.shields.io/badge/python-3.7+-green.svg)](https://docs.python.org/3.7/)
[![PyPI version shields.io](https://img.shields.io/pypi/v/typing-validation.svg)](https://pypi.python.org/pypi/typing-validation/)
[![PyPI status](https://img.shields.io/pypi/status/typing-validation.svg)](https://pypi.python.org/pypi/typing-validation/)
[![Checked with Mypy](http://www.mypy-lang.org/static/mypy_badge.svg)](https://github.com/python/mypy)
[![Python package](https://github.com/hashberg-io/typing-validation/actions/workflows/python-pytest.yml/badge.svg)](https://github.com/hashberg-io/typing-validation/actions/workflows/python-pytest.yml)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [API](#api)
- [Contributing](#contributing)
- [License](#license)


## Install

You can install the latest release from PyPI as follows:

```
pip install typing-validation
```

## Usage

The core functionality of this library is provided by the `validate` function:

```py
>>> from typing_validation import validate
```

The `validate` function is invoked with a value and a type as its arguments and it returns nothing when the given value is valid for the given type:

```py
>>> validate(12, int)
# nothing is returned => 12 is a valid int
```

If the value is invalid for the given type, the `validate` function raises a `TypeError`:

```py
>>> validate(12, str)
TypeError: For type <class 'str'>, invalid value: 12
```

For nested types (e.g. parametric collection/mapping types), the full chain of validation failures is shown by the type error:

```py
>>> validate([0, 1, "hi"], list[int])
TypeError: For type list[int], invalid value: [0, 1, 'hi']
  For type <class 'int'>, invalid value: 'hi'
```

For union types, detailed validation failures are shown for individual union member types, where available:

```py
>>> from typing import *
>>> validate([[0, 1, 2], {"hi": 0}], list[Union[Collection[int], dict[str, str]]])
TypeError: For type list[typing.Union[typing.Collection[int], dict[str, str]]],
invalid value: [[0, 1, 2], {'hi': 0}]
  For type typing.Union[typing.Collection[int], dict[str, str]], invalid value: {'hi': 0}
    Detailed failures for member type typing.Collection[int]:
      For type <class 'int'>, invalid value: 'hi'
    Detailed failures for member type dict[str, str]:
      For type <class 'str'>, invalid value: 0
```

## API

The [API documentation](https://hashberg-io.github.io/typing-validation/typing_validation/index.html) for this package is automatically generated by [pdoc](https://pdoc3.github.io/pdoc/). Detailed examples can be found in the [notebooks folder](./notebooks) folder.


## Contributing

Please see [the contributing file](./CONTRIBUTING.md).


## License

[MIT © Hashberg Ltd.](LICENSE)