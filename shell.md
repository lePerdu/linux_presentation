# Shell Overview / Cheet Sheet

## Moving Around

* `cd <path>`: Change directory to `path`
* `cd`: Change to home directory
* `ls`: List files in current directory
* `ls <path>`: List files in `path`
* `ls -l`: List files with mmore details
* `ls -a`: Also show hidden files (files starting with dot)


## Inspecting files

* `cat <file1> <file2> ...`: Print out the files (can be used to just show a
  single file)
* `head`: Print out the beginning of a file (20*lines by default)
* `tail`: Print out the end of a file (20*lines by default)
* `less`: Open in an interactive viewer
  - Arrow keys or HJKL for moving around
  - `/`: search (using regular expressions)
  - `n`/`N`: next/previous match

## Searching

* Shell patterns:
  - `*`: Match aything (including nothing)
  - `[abc]`: Match `a`, `b`, or `c`
  - `?`: Match any single character
* Regular Expressions:
  - `.`: Match any single character
  - `*`: 0 or more of previous pattern
  - `\+`: 1 or more of previous pattern
  - `\(...\)`: Just for grouping
  - `[abc]`: Match `a`, `b`, or `c`
  - `[^abc]`: Match any character but `a`, `b`, and `c`
  - `[d-k]`: Match any character from `d` to `k` (also works with numbers)
* `find`: Find all files, recursively
* `find -name <pattern>`: Find all files with matching name
* `grep <pattern> <file1> <file2> ...`: Search for `pattern` in `files`
* `grep -r <pattern>`: Search for `pattern` in all files, recursively
* `grep -l <pattern>`: Show files with contain `pattern`
* `grep -v`: Invert the pattern

## Pipes

* `command1 | command2`: Feed output of `command1` to `command2`
* Works with most commands like `head`, `tail`, `grep`, `less`

## Redircets

* `command > file`: Write output of `command` to `file` (clears `file` first)
* `command >> file`: Append output of `command` to `file`

## Stream Operators

* `sort`: What do you think it does?
  - `-n`: Numberic (not just by character)
  - `-R`: Random
  - `-h`: "Human" numeric sort (e.g. 2K, 1G)
* `tr <c1> <c2>`: Converts character `c1` to `c2`
* `sed 's/<pattern>/<replacement>/'`: Search and replace

## Sequencing Commands

* `command1; command2`: Run in sequence
* `command1 && command2`: Run `command2` only if `command1` succedes
* `command1 || command2`: Run `command2` only if `command1` fails
* `command1 & command2`: Run `command1` and `command2` in parallel (output will
  be intermingled)
* `command1 &`: Run `command1` in the background (output will be intermingled
  with typing)

## Conditionals

* `test ...` or `[ ... ]` are the same
* Command succededs or fails with a status code (so they work with `&&` and `||`)
* `a = b`, `a != b`
* `a -eq b`, `a -ne b`, `a -gt b`, `a -lt b`, `a -ge b`, `a -le b`: Compare `a`
  and `b` as numbers (e.g. "01" and "1" will compare as equal)
* `-e <path>`: `path` exists
* `-f <path>`: `path` is a regular file
* `-d <path>`: `path` is a directory

## Variables

* `name=value`: Spaces not allowed around `=` sign
* `$name`: Value of `name`
* `$a+$b`: NOT the value of `a` plus `b`; variables are substituted as strings

## Expansions

* `$(command)`: Expands to output of `command`
* `$(( 1 + 2 ))`: Do math inside (`+`, `-`, `*`, `/`, `%` with integers)
* `${var#pattern}`: `var` with shortest match of `pattern` stripped from the start
* `${var##pattern}`: `var` with longest match of `pattern` stripped from the start
* `${var%pattern}`: `var` with shortest match of `pattern` stripped from the end
* `${var%%pattern}`: `var` with longest match of `pattern` stripped from the end
* Example: `a=123.456.789`
  - `${a#*.}`: `456.789`
  - `${a##*.}`: `789`
  - `${a%.*}`: `123.456`
  - `${a%%.*}`: `123`

## Quoting

* Double quotes
  - Variables are expanded inside
  - Double quote can be escaped with \\: `"\""` is 1 double quote
* Single quotes
  - Nothing is expanded inside
  - Not possible to embed a single quote inside
* Putting strings right by side concatenates them: e.g. `"abc"'123'` is abc123

## Control flow

* `if`
  ```sh
  if command
  then
      ...
  else
      ...
  fi
  ```
* `elif`
  ```sh
  if command1
  then
      ...
  elif command2
      ...
  fi
  ```
* `while`
  ```sh
  while command
  do
      ...
  done
  ```
* `for`
  ```sh
  for var in abc def hij
  do
      ...
  done

  for var in $(command)
  do
      ...
  done
  ```
  If a command is run, each line is used as an iteration
* `case`
  ```sh
  case var in
      pattern1)
          ...
          ;;
      pattern2)
          ...
          ;;
      *) # Match anything
          ...
          ;;
  esac
  ```

