---
title: "Shell Script"
date: 2021-08-13
categories:
  - blog
tags:
  - algorithm
  - shell script
  - summary
---

1. `tr -s ' ' '\n' `
    * Translate or delete characters
    * `-s ' ' '\n'`: replace multiple spaces by one `'\n'`.

2. `uniq -c`: get unique values and count

3. `sort -r`: sort in reverse order
    * `-n`: compare according to string numerical value, so `10` is larger than `9`

4. `awk '{ print $2, $1 }'`: format output, note the comma is not printed
    * or you can replace comma by space, i.e. `awk '{ print $2 " " $1 }'`
    * `NR` means number of records (i.e. current line number) that's accumulated across multiple files read
        * `awk 'NR==11' file.txt`: print out the 11th line in `file.txt`
    * `FNR`: When awk reads from the multiple input file, `awk NR` variable will give the total number of records relative to all the input file. `Awk FNR` will give you number of records for each input file.
        * `awk 'FNR==1' file.txt tt.txt  t.txt`: print out the first line in each file. If you use `NR`, it'll print out the first record of all records from all files, which is the first record in `file.txt`
    * `NF` is a predefined variable whose value is the number of fields in the current record
    * The code block with an "END" prefix is only executed after the last line is read; similarly, a code block with a "BEGIN" prefix will be executed before any line reads.
    * [AWK is line-based][Solution using AWK with explanations]: the main code block (the code block without prefix) processes one line of input at a time.
    * Concatenation: just use `s " " $b`, it will concatenate `s` with variable `$b`
    * Example code
    ```
    awk '
    {
        for(i=1;i<=NF;i++) {
            if (NR==1) {
                s[i] = $i
            } else {
                s[i] = s[i] " " $i #N.B. concatenate s[i] with space and $i
            }
        }
    }

    END { #N.B. Can't move { to next line. END must be followed by an action
        for(i=1;s[i]!="";i++) {
            print s[i] # print(s[i]) seems to work as well
        }
    }
    ' file.txt
    ```

5. `grep -e '^[0-9]\{3\}-[0-9]\{3\}-[0-9]\{4\}$' -e '^([0-9]\{3\}) [0-9]\{3\}-[0-9]\{4\}$' file.txt`:
    * `-e PATTERNS`: Use  PATTERNS as  the patterns.  If this option is used multiple times or is combined with the -f (--file) option, search for all patterns given. This option can be used to protect a pattern beginning with “-”.
    * `{3}` is used to denote to match exactly `3` times of the previous regex
    * `(...)` is used to group pattern together
    * Use `\` to escape next character such as `{`, `(` to indicate that they are not part of the pattern.

6. `tail`:
    * `-n+10`: output starting with line 10 and to the end of the input. 
        * If the file has less than 10 lines, then outpout nothing

    


[Solution using AWK with explanations]: https://leetcode.com/problems/transpose-file/discuss/111382/Solution-using-AWK-with-explanations