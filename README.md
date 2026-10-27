*This project has been created as part of the 42 curriculum by sjaradat.*

## 🌟 Description

Welcome to **get_next_line**! This project is about learning how to read a file one line at a time using the C programming language.

The goal is to create a function that returns one line on each call, including the newline character (`\n`) when it exists. It helps develop a better understanding of file descriptors, memory allocation, static variables, and string manipulation.

Through this project, I practice working with the `read()` function, handling different file-reading situations, and managing dynamically allocated memory.

## 🚀 Instructions

### 🔨 Compilation

Compile the source files with a test program:

```bash
cc -Wall -Wextra -Werror get_next_line.c get_next_line_utils.c main.c -o test
```

You can also choose a custom buffer size during compilation:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c main.c -o test
```

### ▶️ Usage

Include the header file in your program:

```c
#include "get_next_line.h"
```

Call `get_next_line()` repeatedly to read the file line by line:

```c
char    *line;

while ((line = get_next_line(fd)))
{
    printf("%s", line);
    free(line);
}
```

**Return values:**
- Returns a dynamically allocated string containing the next line.
- Includes `\n` when a newline is present in the returned line.
- Returns `NULL` when there is nothing left to read or when an error occurs.

Remember to free each returned line after using it.

## ⚙️ Function Overview

### Main Function

#### `char *get_next_line(int fd)`

- Reads and returns one line from the given file descriptor.
- Uses a static variable to keep the remaining content between calls.
- Calls helper functions to read, extract, and update the stored content.
- Returns `NULL` when the reading process reaches its end or encounters an error.

### Helper Functions

#### `static char *fill_buffer(int fd, char *read_buffer)`

- Reads data in chunks using `read()`.
- Continues reading until a newline is found or the end of the file is reached.
- Joins the newly read content with the previously stored data.
- Handles memory cleanup if an error occurs.

#### `static char *retreive_line(char *str)`

- Extracts the next line from the stored string.
- Includes the newline character when available.
- Allocates memory for the returned line.
- Returns `NULL` if there is no line to extract.

#### `static char *shift_buffer(char *str)`

- Removes the line that has already been returned.
- Keeps any remaining characters for the next call.
- Frees the stored string when no content remains.

#### `static size_t line_len(char *str, size_t i)`

- Determines the length of a line.
- Stops at the newline character or the end of the string.
- Helps identify which part of the buffer should be returned or preserved.

## 🛠️ Utility Functions

### `size_t ft_strlen(const char *str)`

Calculates the length of a string without counting the terminating `\0`.

### `char *ft_strchr(const char *str, int c)`

Searches for a specific character in a string. It is used to check whether the buffer contains a newline character.

### `char *ft_strdup(const char *s)`

Creates a new dynamically allocated copy of a string. This helps initialize or preserve string content without relying on the original memory.

### `char *ft_strjoin(char *buffer, char *content)`

Combines two strings into a newly allocated string. In this implementation, it also frees the old buffer after joining, so the caller must handle ownership of the memory correctly.

### `char *free_all(char *buffer1, char *buffer2)`

Frees two allocated memory blocks and returns `NULL`. This helps simplify cleanup when an error occurs.

## 📚 What I Learned

Working on get_next_line helps me practice:

- Reading files using file descriptors and `read()`.
- Understanding static variables and preserving data between function calls.
- Allocating and freeing memory with `malloc()` and `free()`.
- Manipulating strings and handling buffers.
- Managing end-of-file conditions and reading errors.
- Organizing a C project into source files and a header file.

## 🌐 Useful Resources

- The official 42 get_next_line subject.
- `man 2 read`
- `man 3 malloc`
- `man 3 free`
- GNU C Library documentation.

## 🤖 AI Assistance

AI tools were used to help review the README's wording, organization, and explanations. The project code was implemented and studied as part of my learning process.

---

**Author:** sjaradat

**Project:** get_next_line

**School:** 42

