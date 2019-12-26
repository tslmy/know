# Notes on testing Polymer elements with Jasmine

## Dealing with `dom-if`

* When selecting by ID an `Element` that is dynamically added to the DOM with `dom-if`, use `parentElement.querySelector('#id')` instead of `parentElement.$['id']`.
* When you have elements only visible through a toggle, and you would like it to be available during a test, don't forget to `flush` after appending your Component to the `document.body`:

  ```markup
  <template is="dom-if" if="[[showButton]]">
  <button id="button"> Button </button>
  </template>
  ```

  ```typescript
  // Script.
  @property({type: Boolean}) showButton: boolean = false;
  ```

  ```typescript
  // Test.
  it('should make use of button correctly', () => {
    const comp = new MyPolymerComponent();
    comp.set('showButton', true);
    document.body.appendChild(comp);
    // A flush is needed to resolve `dom-if`s.
    flush();
  // ...
  ```

## Dealing with `async` behavior

In each execution, all tests of a suite are performed on a single `document`. This means that you should clean up the `document` just before each test finishes, ensuring that you leave the document in the same state it was before conducting this very test. This may imply the following:

* If you have appended an `Element` to the `document.body`, remember to `document.body.removeChild` this element.
* Be cautious if your business logic code has `setTimeout`: Tests are \(generally\) performed really fast, completing and quitting well before a delayed function is called. Of course, you can wait for the delayed function to be called in your test code, but remember that tests are supposed to be run frequently, and the additional delay could accummulate to a considerable waste of time. Therefore, I would generally warn against using `setTimeout` at all.
* You might feel like to test `@polymer/app-route`, which interacts with the URL. This can be really tricky, as the URL of the testing `document` is probably some random HTML file. I still have not yet found a nice way to test routing behaviors.

