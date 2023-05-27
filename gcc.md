# Commands
- `gcc main.c -o something`
- `gcc -c main.c` (generates object files: machine code main.o)
- Libs
  - `gcc main.c -llib -o something` (where lib is the name of the library)
  - `gcc -Wall main.c -static -I/opt/include -L/opt/lib -o something` (forces to use lib.a instead of lib.so)
- Preprocessor
  - `gcc -DNUM=10 -o main.c` (passing NUM=10 as a macro)
  - `gcc -DMESSAGE="\"Hello, World!\"" -o main.c` (passing MESSAGE="Hello, World" as a macro)
  - `gcc -E main.c` (show the macro values)

---

# Environment variables
### Set in .bashrc, .zshrc, etc
- `export C_INCLUDE_PATH=/some/path:/other/path` (Adds path for library searching like /usr/include)
  - Alternative -I /some/path
- `export LIBRARY_PATH=/some/path:/other/path` (Adds path for library searching like /usr/lib)
  - Alternative -L /some/path
- `export LD_LIBRARY_PATH=/some/path:/other/path` (Adds path for library when not included in /usr/include, as lib.a or lib.so)

---

# Conventions
- lib.a (a means static library)
- lib.so (so means shared object)
