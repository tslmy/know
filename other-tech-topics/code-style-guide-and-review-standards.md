# Code Style Guide and Review Standards



Run [linters](https://www.testim.io/blog/what-is-a-linter-heres-a-definition-and-quick-start-guide/). They provide pre-defined sets of rules.

1. Run [pre-commit](https://pre-commit.com/) hooks.
2. Follow [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).
3. Run [SonarLint](https://www.sonarlint.org/). It checks for &gt;600 rules that can be found on [SonarSource](https://rules.sonarsource.com/java/). These rules are identified like this: `RSPEC-12345`.

Implementations.

1. [Return early](http://www.itamarweiss.com/personal/2018/02/28/return-early-pattern.html).
   * **Why**: To reduce [arrow code](https://blog.codinghorror.com/flattening-arrow-code/), an anti-pattern.
2. Add a TODO for removing the feature toggle after A/B testing. Best practices of implementing feature toggles can be found [here](https://martinfowler.com/articles/feature-toggles.html).
3. File extension names should represent the syntax \(e.g., `.json`\), rather than the semantics \(e.g., `.content`, `.expected`, `.test`\). 
   * Mitigation: If you really want, use double-extension **names**, such as `.expected.json`.
   * **Why**: So that automated tools can kick in and verify the syntax.
4. TODOs should include a Jira Ticket ID. Derived from [Google C++ Style](https://google.github.io/styleguide/cppguide.html#TODO_Comments).
   * **Example**: `TODO(SRCH-12345): Change the function signature here after Feature B is enabled.`
   * **Mitigation**: If you absolutely cannot create a Jira Ticket for this TODO, use your username instead: `// TODO(mingyli@): Refactor this block of code into its own function when the demand increases.`.
   * **Why**: Jira should be the only tool for task management.

Tests.

1. Distinguish between [test doubles](https://martinfowler.com/articles/mocksArentStubs.html). Dummies, fakes, stubs, spies, and mocks all have different meanings.
2. Use [`isEqualToComparingFieldByFieldRecursively`](https://joel-costigliola.github.io/assertj/assertj-core-features-highlight.html#field-by-field-recursive) from [AssertJ](https://assertj.github.io/doc/) to compare two complex objects.
   * **When**: When testing a method that returns a complex object, you may choose to compare the returned object with an object parsed from a JSON file. 
   * **Why**: JSON is order-insensitive, and you should not compare JSON strings line-by-line.

