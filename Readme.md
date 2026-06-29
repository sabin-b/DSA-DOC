# DSA-DOC

A structured documentation site for Data Structures & Algorithms problems, built with [Zensical](https://github.com/anomalyco/zensical) — a static site generator for MkDocs.

## Intent

This repo serves as a personal reference for DSA problem-solving patterns. Each problem includes:

- Problem description with test cases
- Multiple approaches with time & space complexity
- TypeScript implementations
- Pattern classification (e.g. Hash Map, Two Pointers, Recursion)

## Structure

Problems are organized by **topic** and **difficulty**:

```
docs/
├── Arrays/Easy/          (16 problems)
├── LinkedList/
│   ├── Easy/             (8 problems)
│   └── Medium/           (3 problems)
├── Recursion/
│   ├── Easy/             (6 problems)
│   └── Medium/           (1 problem)
├── Search/Easy/          (2 problems)
├── Sorting/easy/         (2 problems)
└── Strings/Easy/         (6 problems)
```

## Usage

```sh
# Build the site
python -m zensical build --clean

# Open generated output
open site/index.html
```

## Tech Stack

- **SSG:** Zensical (Python)
- **Language:** TypeScript
- **Pre-commit:** Husky → `npm run build:docs`
