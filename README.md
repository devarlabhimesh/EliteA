# Quiz CLI

An interactive command-line quiz game for learning and reviewing JavaScript, Node.js, and general programming concepts.

## Project Overview

Quiz CLI is a small, dependency-free Node.js application that presents multiple-choice questions in a terminal interface. Users can select a quiz category, choose the number of questions, answer interactively, receive immediate feedback and explanations, and review incorrect answers at the end.

The project is also designed as an educational example of modern JavaScript development. Its implementation demonstrates ES modules, asynchronous programming, file-system access, classes, array methods, destructuring, template literals, error handling, and terminal formatting.

### Intended Audience

- Developers learning JavaScript or Node.js fundamentals
- Students practicing programming concepts
- Testers validating an interactive CLI workflow
- Contributors looking for a small example of a Node.js ES-module application

## Features

- Interactive terminal-based quiz experience
- Three categories: JavaScript Basics, Node.js Fundamentals, and General Programming
- Quiz lengths of all available questions, three questions, or five questions when enough questions exist
- Randomized question order using the Fisher–Yates algorithm
- Number-based answer selection with input validation
- Immediate correct/incorrect feedback and answer explanations
- Progress bar and question counter
- Score percentage and performance message
- Review of incorrect answers after the quiz
- Option to play multiple rounds in one session
- ANSI-colored terminal output without external runtime dependencies
- Questions stored separately in JSON for straightforward content updates

## Technology Stack

### Runtime and Language

- JavaScript using native ES modules
- Node.js 18 or newer
- Node.js built-in modules: `node:fs/promises`, `node:url`, `node:path`, and `node:readline`

### Dependencies

The application has no third-party runtime or development dependencies. Package management is provided by npm through `test-app/package.json`.

### Testing and CI/CD

The package defines a Node.js test command using the built-in test runner. No test files or CI/CD workflow files were identified in the repository.

## Prerequisites

- Node.js 18.0.0 or later
- npm, included with standard Node.js installations
- An interactive terminal that supports ANSI escape codes for colored output

## Setup Instructions

### Clone the Repository

```bash
git clone <repository-url>
cd EliteA
```

### Install Dependencies

There are currently no external dependencies. To initialize the npm project locally:

```bash
cd test-app
npm install
```

`npm install` does not need to download packages because `package.json` contains no dependency entries.

### Start the Application

```bash
npm start
```

Alternatively:

```bash
node index.js
```

## Usage

After starting the application:

1. Choose a category by entering its number.
2. Choose all questions, three questions, or five questions where available.
3. Press Enter to begin.
4. Select each answer by entering the corresponding option number.
5. Read the result and explanation, then press Enter to continue.
6. Review the final score and any incorrect answers.
7. Choose whether to play again.

Example session flow:

```text
Choose a category:
  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 1
```

Questions are loaded from `test-app/data/questions.json`, so quiz content can be updated without changing the application logic.

## Project Structure

```text
EliteA/
├── test-app/
│   ├── data/
│   │   └── questions.json   # Categories, questions, options, answers, explanations
│   ├── src/
│   │   ├── colors.js        # ANSI color and text-style helpers
│   │   ├── input.js         # Readline prompts and input validation
│   │   └── quiz.js          # Quiz state, scoring, progress, and results
│   ├── index.js             # Application entry point and main game loop
│   └── package.json         # npm metadata and scripts
└── README.md
```

The repository also contains macOS metadata files under `__MACOSX/` and `.DS_Store` files. They are not used by the application.

## Configuration

The application does not use environment variables or external configuration files. Quiz content is configured in `test-app/data/questions.json`.

Each question contains:

- `question`: question text
- `options`: ordered answer choices
- `answer`: zero-based index of the correct option
- `explanation`: optional explanation displayed after answering

When adding questions, ensure that `answer` points to an entry in `options`.

## Testing

The npm test script is configured as follows:

```bash
npm test
```

It runs Node.js's built-in test runner. No automated test files were identified in the repository, so the command may report that no tests are present.

For manual testing, launch the application with `npm start` and verify category selection, invalid input handling, answer feedback, scoring, review output, and replay behavior.

## Build and Deployment

### Build

No compilation or build step is required. The application runs directly from its JavaScript source files.

### Deployment

No deployment manifests, Dockerfiles, cloud configuration, or CI/CD workflows were identified. The CLI can be distributed as the `test-app` directory and run on any environment with Node.js 18 or later.

## Architecture

The application is a local, single-process CLI with three main responsibilities:

1. `index.js` loads JSON data, presents the main menus, controls the application loop, and handles top-level errors.
2. `src/input.js` wraps Node's readline API with Promise-based prompts, selection validation, confirmation, and pause behavior.
3. `src/quiz.js` owns quiz state, shuffles questions, evaluates answers, tracks progress, and renders results.
4. `src/colors.js` provides terminal formatting helpers used by the interface.

There is no database, network API, authentication layer, or external service integration.

## Troubleshooting

### `node: command not found`

Install Node.js 18 or newer and ensure the `node` executable is available on your `PATH`.

### The application cannot find the questions file

Run the command from the `test-app` directory and confirm that `data/questions.json` exists:

```bash
cd test-app
npm start
```

### Colors or box characters display incorrectly

Use a terminal with UTF-8 and ANSI escape-code support. The game remains usable in terminals that do not render colors perfectly, although the presentation may be degraded.

### Invalid menu input

Enter a number corresponding to one of the displayed options. The application repeats the prompt until a valid number is entered.

## Contributing

Contributions are welcome. A typical workflow is:

1. Create a feature or fix branch.
2. Make focused changes.
3. Update `test-app/data/questions.json` when adding quiz content.
4. Run `npm test` and perform a manual interactive run with `npm start`.
5. Submit a pull request describing the change.

When adding questions, preserve the existing JSON structure and use zero-based answer indexes.

## License

The project is licensed under the MIT License, as declared in `test-app/package.json`. No separate `LICENSE` file was identified in the repository.

## Additional Notes

- Question order is randomized for each quiz instance, but the question set is currently selected from the first three or five entries before shuffling when a limited quiz length is chosen.
- Scores and answers exist only for the current process; there is no persistent history.
- The repository contains no identified automated test implementation, so manual verification is currently important.
- Information in this README is based on the files present in the repository. No unsupported external services or deployment behavior are assumed.
