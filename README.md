# Demo of Header forwarding in Cabal

This repository contains two Cabal projects `proj-a` and `proj-b`.

`proj-a` contains a header file `lib/include/header.h` and defines a library
and an executable target. The library target defines `include-dirs:
lib/include` so that the header can be included as `header.h`. The executable
target depends on the library target and includes the header file as
`header.h`.

`proj-b` contains an executable target that depends on the `proj-a` library and
includes `proj-a`'s header file as `header.h`.

All targets compile successfully with Cabal.

```
$ cabal new-build proj-a:lib:proj-a
$ cabal new-build proj-a:exe:proj-a
$ cabal new-build proj-b:exe:proj-b
```

This means that Cabal forwards the header file and the `include-dirs` defined
in `proj-a:lib` to both `proj-a:exe:proj-a` and to `proj-b:exe:proj-b`.
