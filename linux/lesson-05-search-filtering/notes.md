# Lesson 05 — Search and Filtering

## Main Commands

### grep
`grep` is used to search text inside files.

Examples:

```bash
grep "ERROR" system.log
grep -i "error" system.log
grep -n "ERROR" system.log
grep -v "INFO" system.log
grep -r "ERROR" .
grep -E "ERROR|WARNING" system.log
