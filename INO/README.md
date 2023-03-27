Software updates over the iss's ino original code by stan

Major updates:
- fillx() accepts custom 8-bit test patterns
- first fills the entire DRAM with the test pattern, then reads back and verifies (readx() func) in a second pass
- stops after MAX_ERRORS count of errors, not after first error
- added Auto-find 4164/41256. The jumper is no longer required, but if closed, will force a 4164 test. This is not the best auto-find solution though, as it writes/reads only one bit.
- readAddress and writeAddress routines rewritten for direct port manipulation - significant speed increase

## normal TEST vs slow TEST

As you already know, DRAMs need their content to be refreshed within some time period.

In 4164/41256 this is done by just toggling every row once in the specified period which is ~4 microseconds.


Look at this code:
```
 for (r = 0; r < max_r; r++) {
    for (c = 0; c < max_c; c++) {
      writeAddress(r, c, v);
      if (readAddress(r, c) != v)
        if (error(r, c))
          return;
    }
```
Because rows are advancing in the outer loop, a row is accessed only after max_r x max_c times.

This is a way too slow - tens and hundreds times slower than the spec depending on memory size - 64 or 256.

Nevertheless, most of DRAMs I've tested pass the tests. Only a few fail with a screenshot similar to one I've posted.


IF: **you want a very slow refresh test** THEN: **leave code as is**

ELSE IF: **you want normal refresh test** THEN: **switch places of r and c variables as shown below**


```
 for (c = 0; c < max_c; c++) {
    for (r = 0; r < max_r; r++) {
      writeAddress(r, c, v);
      if (readAddress(r, c) != v)
        if (error(r, c))
          return;
    }
```
Similar loops can be found in the following functions:

void fill(byte v)

void fillx(byte pattern)

void readx(byte pattern)

---

In short:

if you want a very slow refresh test then use slow TEST version

if you want normal refresh test then use normal TEST version
