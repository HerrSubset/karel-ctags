# Karel-ctags

A regex parser for ctags that allows you to generate tags for Karel source
files. To get it working, copy the `karel.ctags` file to one of the 
directories specified in Universal ctags' [Preload option file documentation](http://docs.ctags.io/en/latest/optlib.html#preload-option-file).

This setup was only tested with Universal ctags, and generates tags for the
following items.

## Programs
Instances of `PROGRAM programName` generate a tag.

## Routines
All types of routine definitions should be supported, but routine import
statements are excluded.

```
-- * These generate tags
ROUTINE basicRoutine
ROUTINE routineWithReturnType : STRING
ROUTINE routineWithArgument(i: INTEGER)
ROUTINE routineWithArgumentAndReturnType(s : STRING) : INTEGER
ROUTINE routineWithMultipleArguments(s : STRING; i : INTEGER)
ROUTINE routineWithMultipleArgumentsAndReturnType(s : STRING; i : INTEGER) : STRING

-- * These do not generate tags
ROUTINE firstImport FROM otherFile
ROUTINE secondImport(s : STRING) FROM otherFile
ROUTINE thirdImport(i: INTEGER; s : STRING) FROM otherFile
```

## Structures
The name of a structure definition gets tagged.

```
MyType FROM SomeProgram = STRUCTURE
	myVar : INTEGER
ENDSTRUCTURE
```

## Constants

This is a hacky one, but variable assignments where the variable name only
contains upper case letters and underscores gets tagged as a constant
definition.


```
-- * A constant
	MY_NEW_VALUE = 3

-- * Not a constant
	my_old_value = 26
```

