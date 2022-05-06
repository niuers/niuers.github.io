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

7. 输入相似文件名太麻烦
    1. 用花括号括起来的字符串用逗号连接，可以自动扩展，非常有用，直接看例子：```echo {one,two,three}{1,2,3}```
    2. 注意花括号和其中的逗号不可以用空格分隔，否则会被认为是普通的字符串对待。
    3. ```cp /very/long/path/file{,.bak}```: 给 file 复制一个叫做 file.bak 的副本

8. 输入路径名称太麻烦
    1. 特殊命令 `!$` 会替换成上一次命令最后的路径: 
    ```
    # 没有加可执行权限
    $ /usr/bin/script.sh
    zsh: permission denied: /usr/bin/script.sh

    $ chmod +x !$
    chmod +x /usr/bin/script.sh
    ```
    2. 特殊命令 `!*` 会替换成上一次命令输入的所有文件路径
    ```
    # 创建了三个脚本文件
    $ file script1.sh script2.sh script3.sh

    # 给它们全部加上可执行权限
    $ chmod +x !*
    chmod +x script1.sh script2.sh script3.sh

    ```
    3. 可以在环境变量 CDPATH 中加入你常用的工作目录，当 cd 命令在当前目录中找不到你指定的文件/目录时，会自动到 CDPATH 中的目录中寻找。
    ```
    $ export CDPATH='~:/var/log'
    # cd 命令将会在 ～ 目录和 /var/log 目录扩展搜索
    ```
    需要注意的是，以上操作是 bash 支持的，其他主流 shell 解释器当然都支持扩展 cd 命令的搜索目录，但可能不是修改 CDPATH 这个变量，具体的设置方法可以自行搜索
9. 输入重复命令太麻烦: 使用特殊命令 `!!`，可以自动替换成上一次使用的命令：
```
$ apt install net-tools
E: Could not open lock file - open (13: Permission denied)

$ sudo !!
sudo apt install net-tools
[sudo] password for fdl:
```
10. 有的命令很长，一时间想不起来具体参数了怎么办？
    
    1. 对于 bash 终端，可以使用 Ctrl+R 快捷键反向搜索历史命令
    2. 我们最常用的方法是使用 history 命令配合管道符和 grep 命令来寻找某个历史命令. 只要使用 `! +` 你想重用的命令编号即可运行该命令
    3. 我觉得 history 加管道加 grep 这样打的字还是太多，可以在 你的 shell 配置文件中（.bashrc，.zshrc 等） 中写这样一个函数：
    ```
    his()
    {
        history | grep "$@"
    }
    ```
11. 其他小技巧
    1. yes 命令自动输入字符 y 进行确认: `yes | your_cmd`. 这样就会一路自动 y 下去，不会停下让我们输入了。
    2. 特殊变量 $? 记录上一次命令的返回值
    ```
    # 查看文件尾部是否包含关键词
    tail | grep '下一篇' $filename
    # grep 查找到匹配会返回 0，找不到则返回非 0 值
    [ $? -ne 0 ] && { 添加页脚; }
    ```
    3. 特殊变量 $$ 记录当前进程的 PID。在写 shell 脚本时也非常有用，比如说你要在 /tmp 创建临时文件，给文件起名字一直都是非常让人费脑子的，这时候可以使用 $$ 变量扩展出当前进程的 PID 作为临时文件名，PID 在计算机中都是唯一的，所以绝不会重复，也不需要你记住临时文件的名字。

[Solution using AWK with explanations]: https://leetcode.com/problems/transpose-file/discuss/111382/Solution-using-AWK-with-explanations
[LINUX SHELL 的实用小技巧]: https://labuladong.github.io/algo/5/36/