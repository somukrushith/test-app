# Quiz CLI

An interactive command-line quiz game for learning JavaScript, Node.js, and general programming concepts. The game presents multiple-choice questions, explains answers, tracks a score, and offers a review of incorrect answers.

> **Repository layout warning:** The entry point currently imports modules from `src/` and loads questions from `data/`, but the repository file listing places these files at the root. See [Known setup issue](#known-setup-issue) before trying to run the app.

## Table of contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Setup](#setup)
- [Usage](#usage)
- [Question data](#question-data)
- [Project structure](#project-structure)
- [Tests](#tests)
- [Known setup issue](#known-setup-issue)
- [License](#license)

## Overview

Quiz CLI is a Node.js terminal quiz application written with JavaScript ES modules. It includes question sets for JavaScript Basics, Node.js Fundamentals, and General Programming. The codebase also demonstrates concepts such as asynchronous input handling, promises, classes, array operations, file-system access, and error handling.

## Features

- Choose from three quiz categories.
- Play all questions or choose a 3-question or 5-question round when the category has enough questions.
- Answer numbered multiple-choice prompts in the terminal.
- See immediate correctness feedback and an explanation when provided.
- Track progress and view a final score and performance message.
- Review incorrect answers and play another round.
- Display terminal styling using built-in ANSI escape codes; no color package is used.

## Requirements

- Node.js 18.0.0 or newer, as specified by `package.json`.
- A terminal capable of interactive standard input/output.

The project declares no third-party package dependencies. Its code uses Node.js built-in modules.

## Setup

Clone the repository and change into its directory:

```sh
git clone <repository-url>
cd <repository-directory>
```

No dependency installation is indicated by the manifest. Once the repository layout issue described below is corrected, start the game with:

```sh
npm start
```

## Usage

The intended command is:

```sh
npm start
```

The game flow is:

1. Choose a category by entering its displayed number.
2. Choose all questions, 3 questions, or 5 questions (the shorter choices appear only when the category contains enough questions).
3. Press Enter to begin, then enter the number corresponding to each answer.
4. Review feedback and explanations after each answer.
5. View the final score and any incorrect answers, then answer `y` or `n` when asked whether to play again.

**Current limitation:** With the files in their listed root-level locations, the start command is expected to fail before this interaction begins. See [Known setup issue](#known-setup-issue).

## Question data

The question bank is JSON organized under a top-level `categories` object. Each category has a display `name` and a `questions` array. A question contains `question` text, an `options` array, a zero-based `answer` index into that array, and an optional `explanation` string. The quiz shuffles the selected questions before presenting them.

The checked-in data provides five questions in each of these categories:

- `javascript` — JavaScript Basics
- `nodejs` — Node.js Fundamentals
- `general` — General Programming

## Project structure

The repository listing shows these project files at the root:

```text
.
├── colors.js       # ANSI terminal color helpers
├── index.js        # Application entry point and main interaction loop
├── input.js        # Readline prompts, selections, and confirmations
├── package.json    # Project metadata, scripts, and Node.js engine requirement
├── questions.json  # Quiz categories and question data
└── quiz.js         # Quiz state, question flow, scoring, and result display
```

`.DS_Store` is also present in the repository listing; it is a macOS metadata file and is not used by the application.

## Tests

The manifest defines this test command:

```sh
npm test
```

It invokes Node's built-in test runner (`node --test`). No test files are present in the repository listing, so the available test coverage cannot be established from the inspected files.

## Known setup issue

The checked-in paths do not currently agree:

- `index.js` imports `./src/input.js`, `./src/quiz.js`, and `./src/colors.js`.
- `index.js` reads `data/questions.json` relative to its own directory.
- The repository listing instead shows `input.js`, `quiz.js`, `colors.js`, and `questions.json` at the root, with no `src/` or `data/` directories.

As a result, the documented `npm start` command is not expected to work with the current layout. The import paths and question-data path need to be made consistent with the actual file locations before the CLI can be used. This README records the discrepancy; it does not claim the application or tests were executed.

## Configuration and external services

No environment variables, external services, or separate configuration files are indicated by the inspected source and package manifest. Quiz content is stored in `questions.json`.

## License

`package.json` declares the project license as MIT. A separate license text file was not present in the repository listing.