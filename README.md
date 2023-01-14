# A guide to practical usage of PHP FFI
Code and support files for article "A guide to practical usage of PHP FFI"

## Repository content

- [Dockerfile](Dockerfile) - docker file for kambo22/php-ffi-duckdb-article image.
- [duckdb.h](duckdb.h) - original header file for duckDB.
- [duckdb.php](duckdb.php) - complete source code of example.
- [duckdb-ffi.h](duckdb-ffi.h) - resolved file for PHP FFI, can be directly used in PHP.
- [libduckdb.so](libduckdb.so) - DuckDB database binary.
- [README.md](README.md) - instruction.

## How to use docker image

Prefix the header file with the #define FFI_LIB "./libduckdb.so" directive:
```bash
docker run --rm -v "$PWD":/tmp/example -w /tmp/example kambo22/php-ffi-duckdb-article echo '#define FFI_LIB "./libduckdb.so"' >> duckdb-ffi.h
```

Resolve macros in header file:
```bash
docker run --rm -v "$PWD":/tmp/example -w /tmp/example kambo22/php-ffi-duckdb-article cpp -P -C -D"attribute(ARGS)=" duckdb.h >> duckdb-ffi.h
```

Run DuckDB example "duckdb.php":
```bash
docker run --rm -v "$PWD":/tmp/example -w /tmp/example kambo22/php-ffi-duckdb-article php duckdb.php
```
