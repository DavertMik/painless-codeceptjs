
## There is a solution...

(not perfect, but who is perfect in this world?)

---

# CodeceptJS

![](img/cjs-base.png)

[codecept.io](https://codecept.io)

---

## CodeceptJS

* **end to end** testing framework
* helpers for popular testing backend
* high-level **unified APIs** for all backends
* **~15K** week installations 

[codecept.io](https://codecept.io)

---

### Sample Test

```js
Scenario('todomvc', (I) => {
  I.amOnPage('http://todomvc.com/examples/react/');
  I.waitForElement('.new-todo');
  I.dontSeeElement('.todo-count');
  I.fillField('What needs to be done?', 'Write a guide');
  I.pressKey('Enter');
  I.see('Write a guide', '.todo-list');
  I.see('1 item left', '.todo-count');
  I.fillField('What needs to be done?', 'Write a test');
  I.pressKey('Enter');
  I.see('Write a test', '.todo-list');
  I.see('2 items left', '.todo-count');
  I.fillField('What needs to be done?', 'Write a code');
  I.pressKey('Enter');
  I.see('Write a code', '.todo-list');
  I.see('3 items left', '.todo-count');
});
```

---

![](img/todo.gif)

---

## Problems to be solved

* What framework to choose?
* Actions Are flaky
* Locators Are Flaky
* Readability

---

### Architecture

![](img/codeceptjs-backends.svg)

---

## Multi-Backend Framework

* CodeceptJS is a meta-framework
* Tests can be run by Selenium, Puppeteer, Appium, Protractor,...
* Tests use the same interface
* If a new tool emerges it's easy to add it 
* If an edgecase is hit, it's easy to migrate tests

---

### Flaky actions

* Retry flaky steps

```js
I.retry(2).click('Link');
```
* Auto-retry plugin
* Use wait* commands

```js
I.waitForElement('.modal');
```

* SmartWait

---

### Flaky Locators

* Focus on semantic locators
  * placholders
  * links
  * buttons
  * form element names
* Use CSS/XPath for stable parts
* Locator builder

---

### Readability

* Focus on user actions
* Hide implementation
* Use semantic elements
* Scenarios are easy to follow

---

### Readability Example

```js
I.amOnPage('/');
I.click('Sign in', 'header');
I.see('Sign in', 'h1');
I.fillField('Username or email address', 'something@totest.com');
I.fillField('Password', '123456');
I.click('Sign in');
I.see('Welcome!');
```

---

### Readability & Reusability 

```js
Scenario('publish an article', async (I, loginPage) => {  
  const user = await I.have('user', { name: 'davert' });
  loginPage.login(davert);
  I.see('User logged in', loginPage.messageBox);
  I.click('New', '.articles');
  within('.new-article', () => {
    I.fillField('title', 'My new article');
    I.fillField('body', 'Very important message');
    I.click('Publish');
  });
  I.see('Article was published', '.message');
});
```

---

### BDD: +1 Abstraction Layer

```gherkin
  Scenario:
    Given I have product with $600 price in my cart
    And I have product with $1000 price
    When I go to checkout process
    Then I should see that total number of products is 2
    And my order amount is $1600
```

---

### CodeceptJS has built in Cucumber

* To write business scenarios
* To automate business sceanrios as tests
* To combine regression tests and business scenarios

---

### Promises

```js
I.amOnPage('/validation_code');
I.see('Your Validation Code:');
let code = await I.grabValueFrom('#code')
```

* Browser commands are asynchronous
* Global promise recorder
* `await` is used when execution should be interrupted

---

### Live Development

```js
I.amOnPage('/');
pause();
```

* Call `pause()` to interrupt the test
* Use interactive shell to try different commands
* Copy successful commands into a test

---

### Other Notable Features

* Multi session testing
* Data management
* Allure reports
* Official Docker image
* Mobile tests

---

## Conclusions

* CodeceptJS is a meta framework
* CodeceptJS focused on readability
* CodeceptJS simplifies end to end testing

---

## Taking it further...

* Meet [EasyTesting.io](https://easytesting.io)...

---

## CodeceptJS As A Service

![](img/easytesting.png)

---

### EasyTesting

* Online IDE for End to End tests
* Runs tests in cloud
* Easy to get for non-developers
* Fully compatible with CodeceptJS

---

## Questions

* **Michael Bodnarchuk @davert**
* CodeceptJS: [codecept.io](https://codecept.io)
* EasyTesting: [easytesting.io](https://easytesting.io)
 
