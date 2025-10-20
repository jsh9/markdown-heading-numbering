# markdown-heading-numbering

CLI formatter and pre-commit hook that adds hierarchical numbering to Markdown
headings.

______________________________________________________________________

**Table of Contents:**

<!--TOC-->

- [1. Why add numbering to markdown headings?](#1-why-add-numbering-to-markdown-headings)
- [2. How to use this tool?](#2-how-to-use-this-tool)
  - [2.1. As a command-line tool](#21-as-a-command-line-tool)
  - [2.2. As a pre-commit hook](#22-as-a-pre-commit-hook)
- [3. Compatibility with other formatters](#3-compatibility-with-other-formatters)
  - [3.1. With markdown-toc-creator](#31-with-markdown-toc-creator)
  - [3.2. With mdformat](#32-with-mdformat)

<!--TOC-->

______________________________________________________________________

## 1. Why add numbering to markdown headings?

Here are some benefits of numbering markdown headings:

1. Improve readability
   - Numbering naturally indicate hierarchy: "3.1.6" is the child of "3.1"
   - Without numbering, we'd rely on font style & size to tell hierarchy, which
     is not reliable
2. Reduce communication overhead in a team setting
   - You can reference the section by "Section 2.3.5" instead of "the section
     named 'Monthly Sales Trend and What That Means for Our Business in the
     Long Run'"
3. Make diffs clearer
   - Renumbered headings reveal structural edits instead of hiding content
     changes in walls of text

## 2. How to use this tool?

### 2.1. As a command-line tool

First, install it from PyPI:

```bash
pip install markdown-heading-numbering
```

And then:

```bash
markdown-heading-numbering \
  --start-from-level 2 \
  --end-at-level 5 \
  --initial-numbering 1 \
  docs/README.md
```

Options:

- `--start-from-level` (`int`, default `2`): first heading level to number.
- `--end-at-level` (`int`, default `6`): last heading level to number
  (inclusive).
- `--initial-numbering` (`int`, default `1`): starting value for the top-most
  numbered heading.

Any existing numbering is removed before the formatter applies the new
sequence.

### 2.2. As a pre-commit hook

This repository ships a `.pre-commit-hooks.yaml` that points to the CLI. Add
the hook to your `.pre-commit-config.yaml`:

```yaml
- repo: https://github.com/jsh9/markdown-heading-numbering
  rev: <commit-or-tag>
  hooks:
    - id: markdown-heading-numbering
      args:
        - --start-from-level=2
        - --end-at-level=4
        - --initial-numbering=1
```

The hook shares the same options as the CLI and formats files in place.

## 3. Compatibility with other formatters

### 3.1. With [markdown-toc-creator](https://github.com/jsh9/markdown-toc-creator)

If you are also using
[markdown-toc-creator](https://github.com/jsh9/markdown-toc-creator) as a
pre-commit hook to for create tables of contents in your markdown files, put
that hook **after** this one.

### 3.2. With [mdformat](https://github.com/hukkin/mdformat)

This tool is fully compatible with
[mdformat](https://github.com/hukkin/mdformat) as pre-commit hooks.
