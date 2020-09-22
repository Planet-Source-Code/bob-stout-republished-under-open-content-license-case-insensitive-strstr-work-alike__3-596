<div align="center">

## Case\-insensitive strstr\(\) work\-alike


</div>

### Description

StriStr--This function is an ANSI version of strstr() with case insensitivity.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Bob Stout \(republished under Open Content License\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/bob-stout-republished-under-open-content-license.md)
**Level**          |Beginner
**User Rating**    |3.7 (11 globes from 3 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Strings](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/strings__3-26.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/bob-stout-republished-under-open-content-license-case-insensitive-strstr-work-alike__3-596/archive/master.zip)





### Source Code

```
/* +++Date last modified: 05-Jul-1997 */
/*
** Designation: StriStr
**
** Call syntax: char *stristr(char *String, char *Pattern)
**
** Description: This function is an ANSI version of strstr() with
**        case insensitivity.
**
** Return item: char *pointer if Pattern is found in String, else
**        pointer to 0
**
** Rev History: 07/04/95 Bob Stout ANSI-fy
**        02/03/94 Fred Cole Original
**
** Hereby donated to public domain.
*/
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include "snip_str.h"
typedef unsigned int uint;
#if defined(__cplusplus) && __cplusplus
 extern "C" {
#endif
char *stristr(const char *String, const char *Pattern)
{
   char *pptr, *sptr, *start;
   uint slen, plen;
   for (start = (char *)String,
      pptr = (char *)Pattern,
      slen = strlen(String),
      plen = strlen(Pattern);
      /* while string length not shorter than pattern length */
      slen >= plen;
      start++, slen--)
   {
      /* find start of pattern in string */
      while (toupper(*start) != toupper(*Pattern))
      {
         start++;
         slen--;
         /* if pattern longer than string */
         if (slen < plen)
            return(NULL);
      }
      sptr = start;
      pptr = (char *)Pattern;
      while (toupper(*sptr) == toupper(*pptr))
      {
         sptr++;
         pptr++;
         /* if end of pattern then pattern was found */
         if ('\0' == *pptr)
            return (start);
      }
   }
   return(NULL);
}
#if defined(__cplusplus) && __cplusplus
 }
#endif
#ifdef TEST
int main(void)
{
   char buffer[80] = "heLLo, HELLO, hello, hELLo, HellO";
   char *sptr = buffer;
   while (0 != (sptr = stristr(sptr, "hello")))
      printf("Found %5.5s!\n", sptr++);
   return(0);
}
#endif /* TEST */
```

