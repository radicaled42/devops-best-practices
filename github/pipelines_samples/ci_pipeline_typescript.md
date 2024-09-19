# Sample pipeline for Javascript/Typescript

```yaml
name: TypeScript CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  typescript-ci:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16.x, 18.x]
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}

      - name: Install dependencies
        run: yarn install

      - name: Lint code (Yarn)
        run: yarn lint

      - name: Build project
        run: yarn build

      - name: Run TypeScript tests
        run: |
          yarn test --ci --reporters=jest-junit

      - name: Upload test results
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: jest-test-results
          path: ./test-results/junit.xml
```

## Explanation:

- **Checkout code**: Uses actions/checkout@v3 to clone the repository's code.
- **Set up Node.js**: The setup-node@v3 action sets up the specified Node.js version from the matrix, ensuring the correct environment is used.
- **Install dependencies**: Runs npm install to install the dependencies from package.json.
- **Run TypeScript tests**: Uses npm test to run the unit tests. The --ci flag ensures it runs in a CI environment, and --reporters=jest-junit produces test results in JUnit format.
- **Upload test results**: This uploads the Jest test results as an artifact for later review.

### Why is this important?

- Linting: Running yarn lint or npm run lint ensures that your TypeScript code adheres to best practices and catches issues such as unused variables, incorrect formatting, or potential bugs.
- Build: The yarn build or npm run build step ensures that your TypeScript code compiles correctly into JavaScript. This is essential for production-ready applications.
- Install Dependencies: Running yarn install or npm install ensures that all required packages are installed in the CI environment before testing or building.

`src/sum.ts`
```typescript
export function add(x: number, y: number): number {
  return x + y;
}
```

`src/sum.test.ts`
```ts
import { add } from '../src/sum';

test('adds 1 + 2 to equal 3', () => {
  expect(add(1, 2)).toBe(3);
});

test('adds -1 + 1 to equal 0', () => {
  expect(add(-1, 1)).toBe(0);
});

test('adds 0 + 0 to equal 0', () => {
  expect(add(0, 0)).toBe(0);
});
```
