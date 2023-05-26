# Commands
- `gcc main.c -o something`
- `gcc -c main.c` (generates object files: machine code)
- `gcc main.c -llib -o something` (where lib is the name of the library)

# Environment variables
### Set in .bashrc, .zshrc, etc
- `export C_INCLUDE_PATH=/some/path:/other/path` (Adds path for library searching like /usr/include)
  - Alternative -I /some/path
- `export LIBRARY_PATH=/some/path:/other/path` (Adds path for library searching like /usr/lib)
  - Alternative -L /some/path
- `export LD_LIBRARY_PATH=/some/path:/other/path` (Adds path for library when not included in /usr/include, as lib.a or lib.so)

# Conventions
- lib.a (a means static library)
- lib.so (so means shared object)
