# Lesson 02 - Linux Paths

## Absolute path

An absolute path starts from `/`.

Example:

`/home/phantom/devops-labs`

It works from anywhere because it describes the full location.

## Relative path

A relative path starts from the current directory.

Example:

`cd 01-linux-basics`

This works only if I am currently inside `~/devops-labs`.

## Special path symbols

- `.` means current directory.
- `..` means parent directory.
- `~` means my home directory: `/home/phantom`.

## Important DevOps rule

Before running commands that create, edit or delete files, I should always check my current location with `pwd`.
