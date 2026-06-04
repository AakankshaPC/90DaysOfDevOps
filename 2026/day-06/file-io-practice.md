## Day 06 – Linux Fundamentals: Read and Write Text Files

## Commands I Ran & What They Did

### 1. Create the file

```bash
touch notes.txt
```

Creates an empty file named `notes.txt`.

---

### 2. Write the first line (overwrite with `>`)

```bash
echo "Learning Linux takes patience and practice." > notes.txt
```

The `>` operator **overwrites** the file with new content. If the file already had text, it would be replaced.

---

### 3. Append more lines (with `>>`)

```bash
echo "Every command teaches something new." >> notes.txt
echo "Small daily improvements add up over time." >> notes.txt
echo "Mistakes are part of the learning process." >> notes.txt
```

The `>>` operator **appends** to the file without erasing existing content. Each `echo` adds a new line at the bottom.

---

### 4. Write and display at the same time (with `tee`)

```bash
echo "Consistency is the key to mastery." | tee -a notes.txt
```

`tee` reads from standard input and writes to **both the terminal and the file** at the same time.  
The `-a` flag makes it append instead of overwrite.

---

### 5. Read the full file

```bash
cat notes.txt
```

Prints the entire contents of `notes.txt` to the terminal. Good for short files.

**Output:**
```
Learning Linux takes patience and practice.
Every command teaches something new.
Small daily improvements add up over time.
Mistakes are part of the learning process.
Consistency is the key to mastery.
```

---

### 6. Read only the first 2 lines

```bash
head -n 2 notes.txt
```

`head` shows the **top N lines** of a file. Useful when a file is too long to read fully.

**Output:**
```
Learning Linux takes patience and practice.
Every command teaches something new.
```

---

### 7. Read only the last 2 lines

```bash
tail -n 2 notes.txt
```

`tail` shows the **bottom N lines** of a file. Useful for checking recent log entries or appended data.

**Output:**
```
Mistakes are part of the learning process.
Consistency is the key to mastery.
```

---

## Summary Table

| Command | Purpose |
|---|---|
| `touch notes.txt` | Create an empty file |
| `echo "..." > file` | Write (overwrite) to a file |
| `echo "..." >> file` | Append a line to a file |
| `echo "..." \| tee -a file` | Write to file AND display on screen |
| `cat file` | Read the entire file |
| `head -n N file` | Read the first N lines |
| `tail -n N file` | Read the last N lines |
