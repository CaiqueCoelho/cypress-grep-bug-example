Replicating the following problem: https://github.com/cypress-io/cypress/issues/28189

### Current behavior

Today I have some tests without tags, for example:

`file1.cy.test.js` -> Spec file 1

```js
describe('Describe block file 1', () => {
  it('Test 1', () => {});
  it('Test 2', () => {});
});
```

And I have other tests with tags on the describe block:
`file2.cy.test.js` -> Spec file 2

```js
describe('Describe block file 2', { tags: '@burn' }, () => {
  it('Test 3', () => {});
  it('Test 4', () => {});
});
```

And I want to run only the tests without tag on file 1, but with the two options bellow all tests
are running

1. I've tried running Cypress with:
   `npx cypress run --browser chrome --env grepTags=-@burn`

But all tests are running including the ones with `@burn` on the describe block(test 3 and 4)

2. I also tried running Cypress with:
   `npx cypress run --browser chrome --env grepUntagged=true`
   But I still have all tests running including the ones with `@burn` on the describe block(test 3 and 4)

Looking into the logs looks like when using `grepUntagged=true` cypress-grep filters out all tests even the ones without tags on it and describe block, and because cypress-grep is running all tests

### Desired behavior

1. Running with `npx cypress run --browser chrome --env grepTags=-@burn` we should see only the tests in file 1 being executed because we want to run all tests without the tag @burn, becase file 2 has the tag burn on the describe block
2. Running with `npx cypress run --browser chrome --env grepUntagged=true` we should tun only the tests without tags, in this case also the tests on file 1, becase file 2 has the tag burn on the describe block
