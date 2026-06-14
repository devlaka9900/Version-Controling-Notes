# Notes: Using `grep` in Linux

## 1. What is `grep`?

`grep` stands for **global regular expression print**.

It is a Linux command used to **search for text patterns** inside files or command outputs.

You can use `grep` to search:

- Inside a single file
- Inside multiple files
- Across folders
- From the output of another command using pipes

In simple words, `grep` helps you **find matching text quickly**.

---

## 2. Basic Idea of `grep`

The basic syntax of `grep` is:

```bash
grep pattern filename
```

### Meaning

```bash
grep Sam names.txt
```

This command searches for the word or pattern `Sam` inside the file `names.txt`.

If matching lines are found, `grep` prints those lines on the screen.

---

## 3. Example File: `names.txt`

Assume we have a file called `names.txt`.

We can check the files in the current directory using:

```bash
ls -l
```

Example output:

```bash
-rw-r--r--  1 user user  120 names.txt
```

This shows that `names.txt` exists in the current directory.

To view the content of the file, we can use:

```bash
less names.txt
```

The file contains a list of first names. The names are not arranged alphabetically.

---

## 4. Standard Search with `grep`

To search for names that contain `Sam`, use:

```bash
grep Sam names.txt
```

### Explanation

- `grep` is the search command.
- `Sam` is the pattern we are searching for.
- `names.txt` is the file where we are searching.

### Example output

```bash
Sam
Samuel
Samantha
Samson
```

This returns lines that contain the pattern `Sam`.

---

## 5. `grep` is Case Sensitive

By default, `grep` is **case sensitive**.

This means uppercase and lowercase letters are treated as different characters.

For example:

```bash
grep Sam names.txt
```

is different from:

```bash
grep sam names.txt
```

### Explanation

- `Sam` starts with uppercase `S`.
- `sam` starts with lowercase `s`.

So, if the file contains `Sam`, but you search for `sam`, it may not match the same lines.

Example:

```bash
grep sam names.txt
```

This may return names where lowercase `sam` appears somewhere in the line, or it may return no result depending on the file content.

---

## 6. Ignore Case with `grep -i`

To ignore uppercase and lowercase differences, use the `-i` flag.

```bash
grep -i Sam names.txt
```

### Explanation

The `-i` flag means **ignore case**.

So this command matches:

- `Sam`
- `sam`
- `SAM`
- `sAm`

### Example output

```bash
Sam
samuel
Samantha
hansam
SAMSON
```

This is useful when you do not know whether the text is written in uppercase or lowercase.

---

## 7. Exact Word Match with `grep -w`

Sometimes we only want to match the exact word.

For example, if we search for `Sam`, we may not want to match `Samuel` or `Samantha`.

To match the exact word, use the `-w` flag.

```bash
grep -w Sam names.txt
```

### Explanation

The `-w` flag means **word match**.

It only returns lines where `Sam` appears as a complete word.

### Example output

```bash
Sam
```

This ignores partial matches like:

```bash
Samuel
Samantha
Samson
```

because those are not exactly the word `Sam`.

---

## 8. Using `grep` with Pipes

A pipe is written using the vertical bar symbol:

```bash
|
```

A pipe sends the output of one command as the input to another command.

Example:

```bash
ls /bin | grep zip
```

### Explanation

This command works in two steps:

1. `ls /bin` lists the files inside the `/bin` directory.
2. `grep zip` filters the output and shows only lines containing `zip`.

This is useful when a command gives a lot of output and we only want specific results.

---

## 9. Searching Executable Files in `/bin`

The `/bin` directory contains many executable programs.

To list all files inside `/bin`, use:

```bash
ls /bin
```

This may return a long list of results.

To filter only files that contain `zip`, use:

```bash
ls /bin | grep zip
```

### Example output

```bash
gzip
zip
zipcloak
zipgrep
zipinfo
```

This makes the result smaller and easier to read.

---

# Complete Examples

## Example 1: Search for a Name in a File

### Goal

Find all names that contain `Sam` inside `names.txt`.

### Command

```bash
grep Sam names.txt
```

### Explanation

The command searches inside the file `names.txt` and prints every line that contains `Sam`.

### Possible output

```bash
Sam
Samuel
Samantha
Samson
```

### Result

All matching names containing `Sam` are displayed.

---

## Example 2: Search Without Caring About Uppercase or Lowercase

### Goal

Find all names that contain `Sam`, `sam`, or any other case variation.

### Command

```bash
grep -i Sam names.txt
```

### Explanation

The `-i` flag ignores case sensitivity.

This means the command matches both uppercase and lowercase versions of the pattern.

### Possible output

```bash
Sam
samuel
Samantha
SAMSON
hansam
```

### Result

The search becomes more flexible because it does not care about letter case.

---

## Example 3: Search for an Exact Word

### Goal

Find only the exact word `Sam`, not names like `Samuel` or `Samantha`.

### Command

```bash
grep -w Sam names.txt
```

### Explanation

The `-w` flag matches only complete words.

So it will match:

```bash
Sam
```

But it will not match:

```bash
Samuel
Samantha
Samson
```

### Possible output

```bash
Sam
```

### Result

Only exact matches are displayed.

---

## Example 4: Use `grep` with a Pipe

### Goal

Find executable files inside `/bin` that contain the word `zip`.

### Command

```bash
ls /bin | grep zip
```

### Explanation

The command `ls /bin` lists all files inside the `/bin` directory.

The pipe `|` sends that output to `grep zip`.

Then `grep zip` filters the list and only shows lines containing `zip`.

### Possible output

```bash
gzip
zip
zipgrep
zipinfo
```

### Result

Only executable file names containing `zip` are shown.

---

# Useful `grep` Flags

| Flag | Meaning | Example |
|---|---|---|
| `-i` | Ignore case sensitivity | `grep -i Sam names.txt` |
| `-w` | Match exact word | `grep -w Sam names.txt` |
| `-n` | Show line numbers | `grep -n Sam names.txt` |
| `-v` | Show lines that do not match | `grep -v Sam names.txt` |
| `-r` | Search recursively inside folders | `grep -r Sam .` |

---

# Important Notes

## `grep` searches line by line

When `grep` finds a match, it prints the whole line that contains the pattern.

## `grep` is case sensitive by default

`Sam` and `sam` are not the same unless you use `-i`.

## `grep` can find partial matches

Searching for `Sam` can match:

```bash
Sam
Samuel
Samantha
Samson
```

To avoid partial matches, use `-w`.

## `grep` works well with pipes

You can combine `grep` with other commands to filter large outputs.

Example:

```bash
ls /bin | grep zip
```

---

# Summary

`grep` is a powerful Linux command used to search for text patterns. It can search inside files, folders, and command outputs. By default, `grep` is case sensitive, but the `-i` flag can ignore case. The `-w` flag helps search for exact words only. Pipes allow `grep` to filter the output of other commands, making it very useful when working with large lists or directories.

