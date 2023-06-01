# Examples
- [Makefile](https://github.com/javiorfo/cheatsheets/blob/master/c/make/Makefile)

# Basics:
- main.c as prerequisite
```makefile
something: main.c
  gcc main.c -o executable
```
- Steps
```makefile
blah: blah.o
	cc blah.o -o blah # Runs third

blah.o: blah.c
	cc -c blah.c -o blah.o # Runs second

# Typically blah.c would already exist, but I want to limit any additional required files
blah.c:
	echo "int main() { return 0; }" > blah.c # Runs first
```
- Clean
```makefile
some_file: 
	touch some_file

clean:
	rm -f some_file
```
- Variables
```makefile
files := file1 file2
some_file: $(files)
	echo "Look at this variable: " $(files)
	touch some_file

file1:
	touch file1
file2:
	touch file2

clean:
	rm -f file1 file2 some_file
```
```makefile
a := one two # a is set to the string "one two"
b := 'one two' # Not recommended. b is set to the string "'one two'"
all:
	printf '$a'
	printf $b
Reference variables using either ${} or $()
```
```makefile
x := dude

all:
	echo $(x)
	echo ${x}

	# Bad practice, but works
	echo $x 
```
```makefile
one = export blah="I was set!"; echo $$blah

define two
export blah="I was set!"
echo $$blah
endef

all: 
	@echo "This prints 'I was set'"
	@$(one)
	@echo "This does not print 'I was set' because each command runs in a separate shell"
	@$(two)
- Targets
```
```makefile
all: one two three # all contains targets, it runs by default

one:
	touch one
two:
	touch two
three:
	touch three

clean:
	rm -f one two three
```
- Wildcards
```makefile
# Print out file information about every .c file
print: $(wildcard *.c)
	ls -la  $?
```
```makefile
hey: one two
	# Outputs "hey", since this is the target name
	echo $@

	# Outputs all prerequisites newer than the target
	echo $?

	# Outputs all prerequisites
	echo $^

	touch hey

one:
	touch one

two:
	touch two
```
- Conditional
```makefile
foo = ok

all:
ifeq ($(foo), ok)
	echo "foo equals ok"
else
	echo "nope"
endif
```
```makefile
nullstring =
foo = $(nullstring) # end of line; there is a space here

all:
ifeq ($(strip $(foo)),)
	echo "foo is empty after being stripped"
endif
ifeq ($(nullstring),)
	echo "nullstring doesn't even have spaces"
endif
```
```makefile
```
- Makeflags
```makefile
all:
# Search for the "-i" flag. MAKEFLAGS is just a list of single characters, one per flag. So look for "i" in this case.
ifneq (,$(findstring i, $(MAKEFLAGS)))
	echo "i was passed to MAKEFLAGS"
endif
```
- Functions
```makefile
# substitution string
bar := ${subst not, totally, "I am not superman"}
all: 
	@echo $(bar)
```
```makefile
foo := who are you
# For each "word" in foo, output that same word with an exclamation after
bar := $(foreach wrd,$(foo),$(wrd)!)

all:
	# Output is "who! are! you!"
	@echo $(bar)
```
```makefile
# if function
foo := $(if this-is-not-empty,then!,else!)
empty :=
bar := $(if $(empty),then!,else!)

all:
	@echo $(foo)
	@echo $(bar)
```
```makefile
# call a function
sweet_new_fn = Variable Name: $(0) First: $(1) Second: $(2) Empty Variable: $(3)

all:
	# Outputs "Variable Name: sweet_new_fn First: go Second: tigers Empty Variable:"
	@echo $(call sweet_new_fn, go, tigers)
```
