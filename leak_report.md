# Leak report

## Leak 0:
  In strip (check_whitespace.c:41) 
  by is_clean (check_whitespace.c:62)
  by main (check_whitespace.c:87)

_Leak description_
  main() calls is_clean(strings[i]) in its for loop, which in turn calls strip(str) on the input string str. strip() calls calloc and assigns the variable result to its output. It is never unallocated.

_Fix description_
  Free memory from the pointer in is_clean() that is assigned the pointer from strip(). This is done immediately after the line
 `result = strcmp(str, cleaned);` because we no longer need to access the data stored at pointer `cleaned`. 
