# Contribution guide

Are you interested in giving a hand? We can't be more excited about it. Thanks in advance!

Notes:

* we are doing everything we can to review pull requests submitted by the community as soon as possible. It can take days (or weeks) to finalize a review, going through rounds of changes, etc... This is why we kindly ask you to be patient during this process.
* no changes are too small. If you want to contribute, even fixing a typo will help.

Here are some guidelines that could help you to get started quickly.

## Considerations

* Monica is written with a great framework, [Laravel](https://github.com/laravel/laravel). We care deeply about keeping Monica very simple on purpose. The simpler the code is, the simpler it will be to maintain it and debug it when needed. That means we don't want to make it a one page application, or add any kind of complexities whatsoever.
* That means we won't accept pull requests that add too much complexity, or written in a way we don't understand. Again, the number 1 priority should be to simplify the maintenance on the long run.
* It's better to move forward fast by shipping good features, than waiting for months and ship a perfect feature.
* Our product philosophy is simple. Things do not have to be perfect. They just need to be shipped. As long as it works and aligns with the vision, you should ship as soon as possible. Even if it's ugly, or very small, that does not matter.

## Design rules

* **Keep it simple**. No new options, please. If you want new options, please talk to use first.
* **Use what already exists in the current stack**. When adding a feature, do not introduce a new software in the existing stack. For instance, at the moment, the current version does not require Redis to be used. If we do create a feature that (for some reasons) depends on Redis, we will need all existing instances to install Redis on top of all the other things people have to setup to install Monica (there are thousands of them). We can't afford to do that.

## Feature branches

We follow [GitHub Flow](https://guides.github.com/introduction/flow/) to manage the development of features.

## Conventional commits

We follow the [conventional commit message](https://conventionalcommits.org/) syntax for our commits. For instance, `feat: allow provided config object to extend other configs` or `feat(lang): added polish language`.

Every feature branch that is squashed onto main branch must follow these rules.

The benefits are:

* a standard way of writing commit messages for every contributor,
* a way to quickly see and understand what the commit does and what it affects,
* automatic changelog creation based on those keywords.

The keywords that support (heavily inspired by [config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)):

* `ci`,
* `chore`,
* `docs`,
* `feat`,
* `fix`,
* `perf`,
* `refactor`,
* `revert`,
* `style`,
* `test`.

Moreover, every commit message needs to be written in lowercase.

* ✅ feat(lang): added polish language
* ❌ feat(lang): Added polish language

All the commits in a pull request are squashed when merged into main branch. That means _only the commit message of the squashed branch needs to follow this commit message convention_. That also means that you don't need to follow this convention for commits within a branch, which will usually contains a lot of commits with a `wip` title.

## Backend

### Convention

The project follows strict [object calisthenics](http://www.slideshare.net/guilhermeblanco/object-calisthenics-applied-to-php), as much as possible and more and more over time. We will soon implement those rules in the Linters and will block a pull request for the code that does not follow those guidelines. Here are the rules (adapted for PHP):

* Only one indentation level per method,
* Do not use the "else" keyword,
* Do not chain different objects, unless if the execution includes getters and setters,
* Keep your entities small: 100 lines per class and no more than 15 classes per package,
* Any class that contains a collection (or array) cannot use any other properties,
* Document your code.

### Services

Monica is architected around **services**. A service is a single class that does one thing, like `CreateAccount`. The same service is called from the web application as well as the (future) API. A service does one thing, and one thing only (even though this thing can be complex). A service is fully unit tested.

The code is somehow based on domains.

### Unit testing

All the backend must and should be 100% unit tested. To run the test locally, you need to setup a test database, document it in the `.env` file, and run `yarn test` locally, which will run the test suit.

## Front end

### Considerations

* If your contribution involves a change in the UI (even if it's very small), please ping @djaiss in an issue _before_ you start working on it, explaining what you want to achieve, why and how. We want to maintain a high level of visual quality in the software and we will dismiss all pull requests that change the front end that have not been discussed before-hand.
* That being said, we'll probably receive pull requests that change the front end before any previous discussion on the topic. In this case, we do not guarantee that we'll accept the pull request, but in order to increase the chances that it will:
  * Make sure to follow the current visual style and layout.
  * Make sure you do not introduce new colors in the UI.
  * Make sure the user experience is consistent with the rest of the application (ie buttons behave the same, modals are like other modals,...).
  * Make sure you don't introduce new CSS classes, unless they are absolutely necessary. In theory, you shouldn't have to use custom CSS.
  * Do not use Jquery. Use plain JS if strictly needed.
  * Unless absolutely necessary, do not add a new package to the front end.

The above comments can seem harsh and we apologize in advance. However you have to understand that we deeply care about providing the best user experience to our users. Features that are purely backend do not have the same impact as the ones that the user interacts with. Features that modify the front end will have a tremendous impact on how users perceive the software. Therefore we want to make sure that anything that touches the frontend is perfect and aligned with our vision.

### Vite

We use Vite to manage the front-end and its dependencies, and also to compile and/watch the assets. **Please note that we should do our best to prevent introducing new dependencies if we can prevent it**.

If you need to add a new dependency, update `package.json` to add it and make sure you commit `package-lock.json` once `package.json` is updated.

### CSS

We use [Tailwind](https://tailwindcss.com/) extensively and prune any unused CSS in views. To compile and run assets on the fly, use `yarn dev`.

### VueJS

We use VueJS to power the frontend. The interaction between the frontend and the backend is done with [InertiaJS](https://inertiajs.com/). Inertia is pretty transparent and there is nothing specific that you need to learn, if you know already Laravel and Vue.

### Architecture

We use the following architecture to serve views from the backend.

* **Controllers** call a view helper, sometimes a [service](contribution-guide.md#services) and render a view.&#x20;
* If the view needs data, **view velpers** prepare the data that is needed. No data should be prepared in a controller directly, so we can test the view helper in isolation.
* Views are VueJS files.

### Localization

Translation is a very important part of the application. No code should be put in production if it contains bits and pieces of text that is not translated. We have [a dedicated guide](translation.md) for this.

