# CodeceptJS

![](img/cjs-base.png)

[codecept.io](https://codecept.io)

---

## CodeceptJS

* **end to end** testing framework
* helpers for popular testing backend
* high-level **unified APIs** for all backends
* **~50K** weekly installations 

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

### Architecture

![](img/codeceptjs-backends.svg)

---

## Meta-Framework

* Tests can be run by Selenium, Puppeteer, TestCafe, Appium, Protractor,...
* Tests use the same interface
* If a new tool emerges it's easy to add it 
* If an edgecase is hit, it's easy to migrate tests

---

## Problems to Solve

* Flaky Actions
* Flaky Locators
* Complex Locators
* Debugging
* Reporting
* Parallel Execution
* Data Management

---

### Solution 👉 Flaky actions

* Use `autoRety` plugin
* Explicitly retry flaky steps

```js
I.retry(2).click('Link');
```
* Use wait* commands

```js
I.waitForElement('.modal');
```

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

## Simplify Complex Locators

```js
locate('//table')
  .find('a')
  .withText('Edit')
  .as('edit button')

// transformed to XPath  
```

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
I.amOnPage('/checkout');
pause();
```

![](img/pause.gif)

---

### Debugging

* Pause execution whenever you want
* Automatically saved screenshot on fail

```js
After(pause);
```

---

### Data Management

Generate and store all data via **REST** or **GraphQL**

```js
const product = await I.have('product');
const review = await I.have('review', { product_id: product.id });
```

---

### Parallel Execution

```
npx codeceptjs run-workers 3
```

---

### Reporting

![](img/allure.png)

Allure report integrated

---

## Writing a Test

<video controls="" src="img/codeceptjs_demo.mp4" style="width:100%;padding:20px"></video>

---

## Conclusions

* CodeceptJS is a meta framework
* CodeceptJS solves real testing problems
* CodeceptJS simplifies end to end testing

---


## Questions

* **Michael Bodnarchuk @davert**
* CodeceptJS: [codecept.io](https://codecept.io)

