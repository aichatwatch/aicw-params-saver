---
title: Contributing
description: How to build the script, run the tests and send a change.
---

The source code is TypeScript in the `src` folder. The tests are in the `tests` folder. Tests use Vitest with jsdom, a browser simulation for Node.js.

## Set up

<Steps>
  <Step title="Clone the repository">
    ```sh
    git clone https://github.com/aichatwatch/aicw-params-saver.git
    ```
  </Step>
  <Step title="Go to the folder">
    ```sh
    cd aicw-params-saver
    ```
  </Step>
  <Step title="Install the dependencies">
    ```sh
    npm install
    ```
  </Step>
</Steps>

## Commands

Run each command from the project folder.

To build the files in `dist`:

```sh
npm run build
```

To rebuild when a file changes:

```sh
npm run build:watch
```

To run the tests one time:

```sh
npm test
```

To run the tests again when a file changes:

```sh
npm run test:watch
```

To check the types:

```sh
npm run typecheck
```

## Send a change

Open a pull request on [GitHub](https://github.com/aichatwatch/aicw-params-saver). Report bugs and ask questions in [GitHub issues](https://github.com/aichatwatch/aicw-params-saver/issues).

The project uses the MIT license.
