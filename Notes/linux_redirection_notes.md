# Linux Redirection Notes

## 1. What is Redirection?

In Linux, most commands follow a simple workflow:

```bash
input -> command -> output
```

A command usually takes some input, processes it, and then gives output.

By default:

- **Standard input** comes from the keyboard.
- **Standard output** goes to the terminal screen.
- **Standard error** also goes to the terminal screen.

Redirection allows us to change where the input comes from or where the output goes.

For example, instead of showing command output on the screen, we can save it inside a file.

---

## 2. The Three Main I/O Streams

Linux uses numbers to represent input, output, and error streams.

| Number | Name | Meaning | Default Location |
|---|---|---|---|
| `0` | Standard Input | Input given to a command | Keyboard |
| `1` | Standard Output | Normal output from a command | Screen |
| `2` | Standard Error | Error messages from a command | Screen |

These numbers are important when working with redirection, especially when handling errors.

---

## 3. Standard Input Redirection

Standard input means the data that a command receives.

Normally, this input comes from the keyboard. But using redirection, we can make a command take input from a file instead.

The symbol used for input redirection is:

```bash
<
```

### Example

```bash
cat < input.txt
```

### Explanation

This command tells `cat` to read data from the file `input.txt` instead of waiting for keyboard input.

The content of `input.txt` will be displayed on the terminal.

---

## 4. Creating a File Using `cat`

The `cat` command can also be used to create a file and add text into it.

To create a file and type content into it, use:

```bash
cat > input.txt
```

After pressing Enter, the terminal waits for you to type text.

Example text:

```text
This is me adding some text from the keyboard.
```

After typing the text, press:

```bash
Ctrl + D
```

This tells the terminal that you have finished entering text.

### Full Example

```bash
cat > input.txt
This is me adding some text from the keyboard.
Ctrl + D
```

### Important Note

The `>` symbol means output redirection. In this case, the output from the `cat` command is saved into `input.txt`.

If `input.txt` does not already exist, Linux will create it.

If `input.txt` already exists, its old content will be replaced.

---

## 5. Viewing the File Content

After creating the file, we can display its content using `cat`.

```bash
cat < input.txt
```

or simply:

```bash
cat input.txt
```

Both commands will show the content of the file.

### Example Output

```text
This is me adding some text from the keyboard.
```

---

## 6. Standard Output Redirection

Standard output is the normal result produced by a command.

For example, the `ls` command shows the files and folders in the current directory.

Normally, this output appears on the screen.

Example:

```bash
ls
```

Output may look like this:

```text
input.txt
projects
archive
```

With output redirection, we can save this output into a file instead of showing it on the screen.

The symbol used for standard output redirection is:

```bash
>
```

---

## 7. Saving Command Output to a File

Example:

```bash
ls -l > output.txt
```

### Explanation

The command has three parts:

```bash
ls -l
```

This lists files and folders in long format.

```bash
>
```

This redirects the output.

```bash
output.txt
```

This is the file where the output will be saved.

So instead of printing the `ls -l` result on the screen, Linux saves it inside `output.txt`.

If `output.txt` does not exist, it will be created automatically.

---

## 8. Reading the Output File

To view the saved output, use:

```bash
cat output.txt
```

or:

```bash
less output.txt
```

The `less` command is useful for reading longer files because it lets you scroll through the content.

---

## 9. Standard Error Redirection

Errors happen when a command fails.

For example, if we try to list a directory that does not exist, Linux shows an error message.

Example:

```bash
ls -l /bin/usr
```

Output:

```text
ls: cannot access '/bin/usr': No such file or directory
```

This message is not normal output. It is an error message.

In Linux, error messages use the standard error stream, which is represented by the number:

```bash
2
```

---

## 10. Why Normal Output Redirection Does Not Capture Errors

If we run:

```bash
ls -l /bin/usr > error.txt
```

The error message may still appear on the screen.

Why?

Because `>` only redirects standard output, which is stream `1`.

But the error message belongs to standard error, which is stream `2`.

So the error is not saved in `error.txt` unless we specifically redirect standard error.

---

## 11. Redirecting Errors to a File

To save error messages into a file, use:

```bash
2>
```

Example:

```bash
ls -l /bin/usr 2> error.txt
```

### Explanation

```bash
ls -l /bin/usr
```

This tries to list a directory.

```bash
2>
```

This redirects standard error.

```bash
error.txt
```

This is where the error message will be saved.

Now, instead of showing the error on the screen, Linux writes it into `error.txt`.

To view the error file:

```bash
less error.txt
```

or:

```bash
cat error.txt
```

---

## 12. Redirecting Both Output and Errors

Sometimes we want to save both successful output and error messages into the same file.

This is useful for logs.

Example:

```bash
ls -l /bin/usr > error_output.txt 2>&1
```

### Explanation

This command looks complicated, but it can be understood step by step.

```bash
ls -l /bin/usr
```

This runs the command.

```bash
> error_output.txt
```

This redirects normal output to `error_output.txt`.

```bash
2>&1
```

This redirects standard error `2` to the same place as standard output `1`.

So both normal output and error messages are saved into the same file.

---

## 13. Important Redirection Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `<` | Read input from a file | `cat < input.txt` |
| `>` | Send normal output to a file | `ls -l > output.txt` |
| `2>` | Send error output to a file | `ls wrongdir 2> error.txt` |
| `2>&1` | Send error output to the same place as normal output | `ls wrongdir > log.txt 2>&1` |

---

# Complete Examples

## Example 1: Create a Text File Using `cat`

### Goal

Create a file called `input.txt` and save typed text inside it.

### Command

```bash
cat > input.txt
```

### Then Type

```text
This is me adding some text from the keyboard.
```

### Finish Input

Press:

```bash
Ctrl + D
```

### Explanation

The `cat` command accepts typed input from the keyboard.

The `>` symbol redirects that input into the file `input.txt`.

If the file does not exist, it is created automatically.

### View the File

```bash
cat input.txt
```

### Output

```text
This is me adding some text from the keyboard.
```

---

## Example 2: Save `ls -l` Output into a File

### Goal

Save the long listing of the current directory into `output.txt`.

### Command

```bash
ls -l > output.txt
```

### Explanation

The `ls -l` command normally prints file details on the screen.

The `>` symbol redirects that output into `output.txt`.

So the result is saved in a file instead of being displayed on the terminal.

### View the Saved Output

```bash
cat output.txt
```

### Example Output

```text
total 8
-rw-r--r-- 1 user user 45 Jan 1 10:00 input.txt
-rw-r--r-- 1 user user 98 Jan 1 10:05 output.txt
```

---

## Example 3: Save Error Messages into a File

### Goal

Run a command that causes an error and save the error message into `error.txt`.

### Command

```bash
ls -l /bin/usr 2> error.txt
```

### Explanation

The directory `/bin/usr` does not exist in this example.

Because of that, the `ls` command produces an error.

The `2>` symbol redirects the error message into `error.txt`.

### View the Error File

```bash
cat error.txt
```

### Example Output

```text
ls: cannot access '/bin/usr': No such file or directory
```

---

## Example 4: Save Both Output and Errors into One File

### Goal

Save both normal output and error output into a single log file.

### Command

```bash
ls -l /bin/usr > error_output.txt 2>&1
```

### Explanation

The `>` part saves normal output into `error_output.txt`.

The `2>&1` part sends error messages to the same place as normal output.

This is useful when creating log files because both successful output and errors are saved together.

### View the Log File

```bash
cat error_output.txt
```

---

# Summary

Redirection is a powerful Linux feature that allows us to control input, output, and error messages.

The main ideas are:

- Standard input is represented by `0`.
- Standard output is represented by `1`.
- Standard error is represented by `2`.
- Use `<` to read input from a file.
- Use `>` to save normal output to a file.
- Use `2>` to save error messages to a file.
- Use `2>&1` to save both normal output and error messages together.

Redirection is very useful when saving command results, creating files, reading files, and storing error logs.
