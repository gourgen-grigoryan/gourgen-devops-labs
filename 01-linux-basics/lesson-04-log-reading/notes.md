# Lesson 04 - Log Reading

## Commands learned

- `cat file` prints the full file content.
- `less file` opens a file for scrolling and searching.
- `head file` shows the beginning of a file.
- `head -n 5 file` shows the first 5 lines.
- `tail file` shows the end of a file.
- `tail -n 5 file` shows the last 5 lines.
- `tail -f file` follows a file live.
- `wc -l file` counts lines in a file.

## DevOps usage

Logs are one of the first places to check when an application, service or server has a problem.

## Important keys in less

- `q` exits less.
- `/word` searches inside the file.
- `Space` moves forward.
- `b` moves backward.

## Important safety note

For large log files, `less`, `head` and `tail` are usually better than `cat`.
