## So you decided to start end to end testing...

![](img/thinking.jpg)



---

## Questions to be asked

* what language to choose <!-- .element: class="fragment" data-fragment-index="1" -->
* how to execute tests <!-- .element: class="fragment" data-fragment-index="2" -->
* how to interact with page <!-- .element: class="fragment" data-fragment-index="3" -->
* how to locate elements on page <!-- .element: class="fragment" data-fragment-index="4" -->
* what to check <!-- .element: class="fragment" data-fragment-index="5" -->

---

## What language to choose?

* Java
* Ruby
* Python
* JavaScript

---

## JavaScript!

* Rich ecosystem <!-- .element: class="fragment" data-fragment-index="1" -->
* Not limited to Selenium <!-- .element: class="fragment" data-fragment-index="2" -->
* In browser execution <!-- .element: class="fragment" data-fragment-index="3" -->
* [Drawback] Learn how to deal with promises <!-- .element: class="fragment" data-fragment-index="4" -->

---

## What framework to choose?

* webdriverio
* Protractor
* Cypress
* Puppeteer
* TestCafe
* Nightwatch
* Nightmare
* ...

---

## Whatever you choose, you lose!

* New testing frameworks emerge <!-- .element: class="fragment" data-fragment-index="1" -->
* Cool fancy library will be legacy tomorow <!-- .element: class="fragment" data-fragment-index="2" -->
* You hit issues with edge cases <!-- .element: class="fragment" data-fragment-index="3" -->
* Different API <!-- .element: class="fragment" data-fragment-index="4" -->
* You can't migrate your code <!-- .element: class="fragment" data-fragment-index="5" -->

---

## What To Do

* open pages
* act: `click`, `fillField`, `selectOption`, ...
* assert: text, elements, urls
* wait: `waitForElement`, `waitForText`
* take information from page

---

## Actions Are flaky

* At what point page is loaded? <!-- .element: class="fragment" data-fragment-index="1" -->
* Is JavaScript event attached to link? <!-- .element: class="fragment" data-fragment-index="2" -->
* Are HTTP requests finished? <!-- .element: class="fragment" data-fragment-index="3" -->
* Is DOM ready? <!-- .element: class="fragment" data-fragment-index="4" -->

---

## How to Locate Elements

* CSS
* XPath

---

## Locators Are Flaky

* CSS - rely on classes/ids <!-- .element: class="fragment" data-fragment-index="1" -->
* XPath - rely on element position <!-- .element: class="fragment" data-fragment-index="2" -->

---

## Readability

* Is it easy to follow?
* Is it easy to update?
* Does it correspond to business scenario?

---

## You end up like...

![](img/despair.jpg)
