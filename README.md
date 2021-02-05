# 📦 Offshore

Offshore is a simple and ergonomic data persistence mechanism for small-scale Python (3.7+) projects and scripts. You can use Offshore to persist state between runs or expose data to other Python tasks.

# Installation

You can install this package using `pip` or build it from source using `poetry`:

    # Using pip
    pip install offshore

    # Using poetry
    pip install poetry
    poetry build

# Snapshots

```python
from offshore import Offshore, Exportable
from typing import Any

state = Offshore()  # Initialise the state container
standard: Any = "hello_world"
special: Exportable = "magic"

state.snapshot()
standard = "brave_new_world"
special = "sorcery"

state.restore()
assert standard == "brave_new_world"  # The regular variable (correctly) remains changed
assert special == "magic"             # The exportable variable is (correctly) restored
```

# Manual Use

```python
from offshore import Offshore

state = Offshore()  # Initialise the state container

# Item-based usage
state["key"] = "value"
assert state["key"] == "value"

# Attribute-based usage
state.key = "value"
assert state.key == "value"

# Persist state
state.dump()

# Mutate local state
state["key"] = "new_value"

# Recover state
state.load()

# Confirm recovery
assert state["key"] == "value"
```

# Autosave

```python
from offshore import Offshore

state = Offshore(autosave=True)  # Initialise the state container
state["key"] = "value"

# Unrelated program

from offshore import Offshore

state = Offshore(autosave=True)  # Initialise the state container
assert state["key"] == "value"
```

# Autoload

```python
from offshore import Offshore

state = Offshore(autoload=True)  # Initialise the state container
state["key"] = "value"

# Unrelated program mutates state
# Key `key` is set to `new_value`

assert state["key"] == "new_value"
```

# License
```text
BSD 3-Clause License

Copyright (c) 2021, Phil Demetriou
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the copyright holder nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```