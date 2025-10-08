# File Handling in Python

File handling is an essential part of any web application or programming task. Python has several functions for creating, reading, updating, and deleting files.

---

## 1. Opening and Reading Files

The key function for working with files in Python is `open()`. It takes two main parameters: the `filename` and the `mode`.

### Modes for Opening a File

-   `"r"` - **Read**: Default value. Opens a file for reading, returns an error if the file does not exist.
-   `"a"` - **Append**: Opens a file for appending, creates the file if it does not exist.
-   `"w"` - **Write**: Opens a file for writing, creates the file if it does not exist. **Warning:** This will overwrite the entire content of the file if it already exists.
-   `"x"` - **Create**: Creates the specified file, returns an error if the file exists.

You can also specify if the file should be handled in binary (`"b"`) or text (`"t"`) mode. `"t"` is the default.

### The `with` Statement (Recommended)

The recommended way to open a file is by using the `with` statement. It ensures that the file is automatically closed when the block inside the `with` statement is exited, even if errors occur.

```python
# Assume we have a file named "example.txt" with the content:
# Hello, World!
# This is a test file.

with open("example.txt", "r") as file:
    content = file.read()  # Reads the entire file content into a string
    print(content)
```

### Reading Methods

-   **`file.read()`**: Reads the entire content of the file.
-   **`file.readline()`**: Reads a single line from the file.
-   **`file.readlines()`**: Reads all the lines into a list of strings.

```python
with open("example.txt", "r") as file:
    # Read line by line
    for line in file:
        print(line.strip()) # .strip() removes leading/trailing whitespace, including the newline character
```

---

## 2. Writing to Files

To write to a file, you must open it in write (`"w"`) or append (`"a"`) mode.

### Write Mode (`"w"`)

This mode will **overwrite** any existing content in the file. If the file doesn't exist, it will be created.

```python
with open("new_file.txt", "w") as file:
    file.write("This is the first line.\n")
    file.write("This is the second line.")

# After running this, "new_file.txt" will contain:
# This is the first line.
# This is the second line.
```

If you run the same code again with different text, the old content will be completely replaced.

### Append Mode (`"a"`)

This mode will add new content to the **end** of the file without deleting the existing content.

```python
with open("new_file.txt", "a") as file:
    file.write("\nThis line was appended.")

# "new_file.txt" will now contain:
# This is the first line.
# This is the second line.
# This line was appended.
```

---

## 3. Deleting Files and Directories

To delete files, you need to use Python's built-in `os` module.

### Checking if a File Exists

Before trying to delete a file, it's good practice to check if it exists to avoid errors.

```python
import os

if os.path.exists("new_file.txt"):
    print("File exists.")
else:
    print("File does not exist.")
```

### Deleting a File

Use `os.remove()` to delete a file.

```python
import os

if os.path.exists("file_to_delete.txt"):
    os.remove("file_to_delete.txt")
    print("File deleted successfully.")
else:
    print("The file does not exist.")
```

### Deleting a Directory

You can only remove an **empty** directory using `os.rmdir()`.

```python
import os

# Create a directory first
os.mkdir("my_empty_folder")

# Then remove it
os.rmdir("my_empty_folder")
```

To remove a directory that is **not empty**, you need to use the `shutil` module.

```python
import shutil

# This will delete the folder and everything inside it. Use with caution!
# shutil.rmtree("my_non_empty_folder")
```

---

## 4. Working with File Paths

The `os` module also provides tools for working with file paths in a way that is compatible across different operating systems (Windows, macOS, Linux).

```python
import os

# Get the current working directory
current_directory = os.getcwd()
print(f"Current Directory: {current_directory}")

# Join path components in an OS-agnostic way
file_path = os.path.join(current_directory, "data", "my_file.csv")
print(f"Full Path: {file_path}")

# Get the directory name and file name from a path
dir_name = os.path.dirname(file_path)
file_name = os.path.basename(file_path)
print(f"Directory: {dir_name}, File: {file_name}")
```
Using `os.path.join()` is highly recommended over manually concatenating strings with `/` or `\` because it handles the path separators correctly for the operating system your code is running on.
