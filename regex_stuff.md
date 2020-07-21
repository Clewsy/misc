# regex expressions
```shell
.	#will match any character
[ ]	#will match a range of characters
[^ ]	#will match all character except for the one mentioned in braces
*	#will match zero or more of the preceding items
+	#will match one or more of the preceding items
?	#will match zero or one of the preceding items
{n}	#will match ‘n’ numbers of preceding items
{n,}	#will match ‘n’ number of or more of preceding items
{n m}	#will match between ‘n’ & ‘m’ number of items
{ ,m}	#will match less than or equal to m number of items
\	#is an escape character, used when we need to include one of the metcharacters is our search.
```

# Example uses of `rename`
```shell
rename 's/-[^ ]*.mp4/.mp4/' *.mp4
```
If name contains "-", then characters, then ".mp4", except if the "-" is succeded by a space, remove all characters after the "-" except the final ".mp4".

```shell
rename -n -v 's/ \([a-zA-Z0-9 ]*\)//' *.mp4
```
If name contains characters (including a space) within paretheses, remove these characters and the parentheses.

