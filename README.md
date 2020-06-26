# pc-lint-plus-cheat-sheet

Cheat sheet aimed at running for an embedded device.


# Running

You can encapsulate options in to a single file, instead of running:
```
pclp64_linux co-gcc.lnt /opt/pclp-1.3/linux/lnt/au-misra3.lnt my-project.lnt
```
Create a file:

my-project-all.lnt:
```
co-gcc.lnt

/opt/pclp-1.3/linux/lnt/au-misra3.lnt

// Other Options
-wlib(4) -wlib(1) // Turn off warnings for library files

my-project.lnt
```

Then to run:
```
pclp64_linux my-project-all.lnt
```


# Library Files

## Check the classification of files

See what files are classified as libraries using ```-vf```:
```
pclp64_linux -vf co-gcc.lnt /opt/pclp-1.3/linux/lnt/au-misra3.lnt my-project.lnt
```
Note that you main want to grep for a specific file:
```
pclp64_linux -vf co-gcc.lnt /opt/pclp-1.3/linux/lnt/au-misra3.lnt my-project.lnt | grep main.h
```
Output:
```
// If it's being treated as a library
Including file Inc/main.h (library)

// If it's being treated as a header:
Including file Inc/main.h (hdr)
```

## Set the classification of files

Inhibit treating a file as a library

```
// Correct
-libh(main.h)

// Wrong! - Doesn't seem to support paths, even though it reports the paths
-libh(inc/main.h)
```


## Suppressions

Suppress messages 438 and 529 within the body of foo
```
void foo() {
/*lint --e{438, 529} */
int i = 0;
}
```
