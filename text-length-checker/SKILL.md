---
name: text-length-checker
description: Count characters, words, lines, and paragraphs in user-provided text with explicit whitespace and Unicode rules. Use when the user asks for text length, word count, character count, copy limits, or a quick content-size check.
---

# Text Length Checker

## Overview

Measure the supplied text using explicit, reproducible counting rules. Return a compact result and state any non-obvious counting assumptions.

## Workflow

1. Use the exact text provided by the user; do not silently rewrite it.
2. Count characters including spaces and excluding spaces when useful.
3. Count words by splitting on whitespace and ignoring empty segments.
4. Count lines and non-empty paragraphs from the original line breaks.
5. Report the requested metric first, followed by the other metrics when helpful.
6. If the user gives a limit, state whether the text is within that limit.

## Output Format

Use this compact format unless the user asks for a different format:

```text
Characters: <including spaces> (<excluding spaces>)
Words: <count>
Lines: <count>
Paragraphs: <count>
```

## Counting Rules

- Treat consecutive whitespace as one separator when counting words.
- Count punctuation as characters.
- Count a line break as a line separator, not as a visible character.
- Count paragraphs as groups of non-empty lines separated by one or more empty lines.
- Count Unicode characters as user-perceived characters where practical; do not count UTF-16 surrogate pairs twice.
- For empty input, report zero for every metric.
- Preserve the original text when reporting results; do not normalize or trim it silently.
