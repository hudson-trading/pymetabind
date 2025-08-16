# pymetabind: interoperability between different Python <-> C-ish binding frameworks

pymetabind is a single C header file that defines structures and simple inline
functions which are intended to allow different Python binding frameworks
(nanobind, pybind11, Boost.Python, SWIG, pyo3, ...), as well as different ABI
versions of the same framework, to interoperate with each other. That is,
functions bound using framework A can accept and return objects whose types
are bound using framework B. (Different ABI versions of the same framework
are treated like different frameworks would be.)
Each participating framework can use this header to:

* publish lightweight information about its bound types, along with function
  pointers that allow other frameworks to interact with them, to a
  shared data structure located via a Python capsule object; and

* discover and use bindings published in this way by other frameworks.

Individual frameworks must implement support for pymetabind in order to
be used with it. It is possible to implement only support for publishing
bindings, or only support for using other frameworks' bindings, though of
course the greatest interoperability benefits come from implementing both.

## Status

Currently, we are soliciting input from framework maintainers in order
to confirm that the proposed interface will be widely
implementable. **You are encouraged to not publish any official
release with pymetabind support during this time**, since the ABI may
still change. Experimentation, and PRs that make pymetabind a better
fit for your framework, are welcome and encouraged!

## Documentation

All documentation is contained in the header file, ``pymetabind.h``.

## Installation

Copy [pymetabind.h](pymetabind.h) into the implementation of your binding
framework and use the structures and inline functions found therein.
To avoid coordination problems around installation, every framework is
expected to keep its own copy. After a 1.0 release, we intend for changes
to be very minimal and backward-compatible, so it is anticipated that
keeping a copy up-to-date will not be burdensome.

## License and attribution

pymetabind is licensed under the MIT license, which is included in a comment
at the top of the single header file.

pymetabind was written by Joshua Oreman as part of his work with
[Hudson River Trading](https://www.hudsonrivertrading.com/).
