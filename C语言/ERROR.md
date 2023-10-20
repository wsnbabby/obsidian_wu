

## errno
```C
#include <errno.h>

const char * const sys_errlist[];
int sys_nerr;
int errno;       /* Not really declared this way; see errno(3) */
```

## perror
```C
#include <stdio.h>

void perror(const char *s);

#include <errno.h>

const char * const sys_errlist[];
int sys_nerr;
int errno;       /* Not really declared this way; see errno(3) */
```

## strerror
```C
#include <string.h>

char *strerror(int errnum);
```

