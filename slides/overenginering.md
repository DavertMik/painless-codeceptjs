## What's wrong with End 2 End Tests?

### In JavaScript <!-- .element: class="fragment" data-fragment-index="1" -->

---

👇

```js
product.element.all(by.xpath(cons.xpathproductRate())).then(function (products) {
    var i = products.length;
    (function loop() {
        product.sleep(1000);
        var product = cons.xpathproductRate(i);
        product.element(by.xpath(product)).click().then(function () {
            main.waitForElementAndClick(product, cons.linkRemoveproduct).then(function () {
                main.waitForElementAndClick(product, cons.radiobtnRemoveAll).then(function () {
                    main.waitForElementAndClick(product, cons.btnRemoveproduct).then(function () {
                        i = i - 1;
                        if (i > 0) {
                            loop();
                        }
                    });
                });
            });
        });
    })();
});
```

---

## Solution


```gherkin
When I remove all products from a list
```

* Use Cucumber & BDD! <!-- .element: class="fragment" data-fragment-index="1" -->

---

### Behind The Scene

```js
When('I remove all products from a list', function() {
  
  product.element.all(by.xpath(cons.xpathproductRate())).then(function (products) {
      var i = products.length;
      (function loop() {
          product.sleep(1000);
          var product = cons.xpathproductRate(i);
          product.element(by.xpath(product)).click().then(function () {
              main.waitForElementAndClick(product, cons.linkRemoveproduct).then(function () {
                  main.waitForElementAndClick(product, cons.radiobtnRemoveAll).then(function () {
                      main.waitForElementAndClick(product, cons.btnRemoveproduct).then(function () {
                          i = i - 1;
                          if (i > 0) {
                              loop();
                          }
                      });
                  });
              });
          });
      })();
  });
});
```

---

![](img/hide.jpg)

---

## Overengineering

* Focused on browser control <!-- .element: class="fragment" data-fragment-index="1" -->
* Focused on tools: Protractor/Cypress/webdriverio <!-- .element: class="fragment" data-fragment-index="2" -->
* Asynchronity / Promises <!-- .element: class="fragment" data-fragment-index="3" -->

---

## Focus on test scenario!

---

I am on page "/login"

---

I fill field "Username" with "davert"

---

I click "Login"

---

I see "Welcome, davert"

---

## Usually a test consists of actions:

* open a page
* click
* see text / element
* fill field
* ...

---

## Keep Code Simple

* Make a test follow user scenario
* Use highly flexible predefined actions
* Follow line-by-line structure
* Don't care of how it will be executed

---

## A test should look like this

```js
Scenario('Create a new store', (I, SettingsPage) => {
  SettingsPage.open();
  const storeName = faker.lorem.slug();
  I.dontSee(storeName, '.settings');                          // Assert text not present inside an 
  I.click('Add', '.settings');                                // Click link by text inside element (located by CSS)
  I.fillField('Store Name', storeName);                       // Fill fields by labels or placeholders
  I.fillField('Email', faker.internet.email());
  I.fillField('Telephone', faker.phone.phoneNumberFormat());
  I.selectInDropdown('Status', 'Active');                     // Use custom methods
  I.click('Create');                                 // Auto-retry flaky step
  I.waitInUrl('/settings/setup/stores');                      // Explicit waiter
  I.see(storeName, '.settings');                              // Assert text present inside an element (located by CSS)
}).tag('stores');
```

---

## How it is executed?

* Is that WebDriver?
* Is that Cypress?
* Is that TestCafe?
* Is that Puppeteer?

### ANY OF THOSE! <!-- .element: class="fragment" data-fragment-index="1" -->
