## Group Activity

> Work in group to solve these tasks.

## End-to-end testing (E2E)

End-to-end testing (E2E) was always a tedious task with testing frameworks from the past. However, nowadays many people are using [Cypress.io](https://cypress.io) for it. Their documentation has a high quality and their API is concise and clean. Let's use Cypress for this React testing tutorial.

First, you have to install it on the command line to your dev dependencies:

```bash
npm install --save-dev cypress
```

then add an npm-script to run it:

```js
{
  // ...
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "cypress:open": "cypress open"
    },
  // ...
}
```

Unlike the frontend's unit tests, Cypress tests can be in the frontend or the backend repository, or even in their own separate repository.

The tests require the tested system to be running. Unlike our backend integration tests, Cypress tests do not start the system when they are run.

When the frontend are running (`npm start`), we can start Cypress with the command: `npm run cypress:open`

When we first run Cypress, it creates a cypress directory. It contains an e2e subdirectory, where we will place our tests. Cypress creates a bunch of example tests for us in two subdirectories: the e2e/1-getting-started and the e2e/2-advanced-examples directory. We can delete both directories and make our own test in file App.cy.js:

Next, add your first test to it. It's not really an end-to-end test, but only the simplest assertion you can make to verify that Cypress is working for you.

```js
describe('App E2E', () => {
  it('should assert that true is equal to true', () => {
    expect(true).to.equal(true)
  })
})
```

You already know the "describe"- and "it"-blocks which enable you to encapsulate your tests in blocks. These blocks are coming from Mocha, which is used by Cypress, under the hood. The assertions such as `expect()` are used from Chai. _"Cypress builds on these [popular tools and frameworks](https://docs.cypress.io/guides/references/bundled-tools.html) that you hopefully already have some familiarity and knowledge of."_

Cypress finds your test and you can either run the single test by clicking it or run all of your tests by using their dashboard.

Run your test and verify that true is equal to true. Hopefully it turns out to be green for you. Otherwise there is something wrong. In contrast, you can checkout a failing end-to-end test too.

```js
describe('App E2E', () => {
  it('should assert that true is equal to true', () => {
    expect(true).to.equal(false)
  })
})
```

If you want, you can change the script slightly for Cypress to run every test by default without opening the additional window.

```json
{
  "scripts": {
    "cypress:open": "cypress open",
    "cypress:run": "cypress run"
  }
}
```

As you can see, when you run Cypress again on the command line, all your tests should run automatically. In addition, you can experience that there is some kind of video recording happening. The videos are stored in a folder for you to experience your tests first hand. You can also add screenshot testing to your Cypress end-to-end tests. Find out more about [the video and screenshot capabilities of Cypress.io](https://docs.cypress.io/guides/guides/screenshots-and-videos.html). You can suppress the video recording in your Cypress configuration file in your project folder. It might be already generated by Cypress for you, otherwise create `cypress.json` in the root folder, add the `video` flag and set it to false.

In case you want to find out more about the configuration capabilities of Cypress, [checkout their documentation](https://docs.cypress.io/guides/references/configuration.html).

Eventually you want to start to test your implemented React application with Cypress. Since Cypress is offering end-to-end testing, you have to start your application first before visiting the website with Cypress. You can use your local development server for this case.

Finally, you can visit your running application with Cypress in your end-to-end test. Therefore you will use the global `cy` cypress object. In addition, you can also add your first E2E test which verifies your header tag (h1) from your application.

```js
describe('App E2E', () => {
  it('should have a header', () => {
    cy.visit('http://localhost:8080')

    cy.get('h1').should('have.text', 'My Counter')
  })
})
```

Basically, that's how a selector and assertion in Cypress work. Now run your test again on the command line. It should turn out to be successful.

The second E2E test you are going to implement will test the two interactive buttons in your React application. After clicking each button, the counter integer which is shown in the paragraph tag should change. Let's begin by verifying that the counter is 0 when the application just started.

```js
describe('App E2E', () => {
  it('should have a header', () => {
    cy.visit('http://localhost:3000/')

    cy.get('h1').should('have.text', 'My Counter')
  })

  it('should increment and decrement the counter', () => {
    cy.visit('http://localhost:3000/')

    cy.get('p').should('have.text', '0')
  })
})
```

Now, by [interacting with the buttons](https://docs.cypress.io/guides/core-concepts/interacting-with-elements.html), you can increment and decrement the counter.

```js
describe('App E2E', () => {
  it('should have a header', () => {
    cy.visit('http://localhost:3000/')

    cy.get('h1').should('have.text', 'My Counter')
  })

  it('should increment and decrement the counter', () => {
    cy.visit('http://localhost:3000/')

    cy.get('p').should('have.text', '0')

    cy.contains('Increment').click()
    cy.get('p').should('have.text', '1')

    cy.contains('Increment').click()
    cy.get('p').should('have.text', '2')

    cy.contains('Decrement').click()
    cy.get('p').should('have.text', '1')
  })
})
```

That's it. You have written your first two E2E tests with Cypress. You can navigate from URL to URL, interact with HTML elements and verify rendered output. Two more things:

- If you need to provide sample data for your E2E tests, checkout the best practice of using fixtures in Cypress.
- If you need to spy, stub or mock functions in Cypress, you can use Sinon for it. Cypress comes with built-in Sinon to test your asynchronous code.

## Ref

[1](https://www.robinwieruch.de/react-testing-cypress/)