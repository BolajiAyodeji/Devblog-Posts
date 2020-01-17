## Accessibility Auditing with Axe for automated Web UI testing

Accessibility has become widely know and sort-for topic with a lot of developers and organizations advocating for the need to focus more on it towards building for the Next Billion Users.

An accessible site is one whose content can be accessed regardless of any user's impairments and whose functionality can also be operated by the most diverse range of users possible.

In this article, I'll introduce you to the Axe Library and how you can use it for auditing your application(s) on Web Browsers, CLI, Android, React.js, and Vue.js.

New to Web Accessibility? You should read my previous article :).

%[https://bolajiayodeji.com/introduction-to-web-accessibility-cjwum18h600007ds1wreswp3q]

---

A critical aspect of accessibility is **Auditing**. The best way to know if your application is inaccessible is to test and measure it; this way, you ascertain if there is a need for any modification(s) before it is released to production.

Most developers [Definition of Done](https://www.agilealliance.org/glossary/definition-of-done/) excludes accessibility tasks, and I ran into this amazing tweet, which says it all.

%[https://twitter.com/marcysutton/status/1202307488650891264]

Your application is not "Done" until you have tested to be sure it complies with all the accessibility standards and guidelines.


## What is Auditing?

Technical Audit (TA) is an audit performed by an auditor, engineer or subject-matter expert evaluates deficiencies or areas of improvement in a process, system or proposal ~ [Wikipedia](https://en.wikipedia.org/wiki/Technical_audit)

Accessibility Audit (AA) is an audit performed by a developer, engineer, or accessibility expert, which evaluates deficiencies or areas of improvement in building websites that comply with the [web accessibility guidelines](https://www.w3.org/WAI/intro/wcag).

As an enthusiastic developer with a great focus for accessibility, it would take a while for you to master all the guidelines and be capable of building an accessible application from scratch without any errors. Just like learning any other skill, you need to practice, and eventually, you get used to these A11y standards. One way to practice here is to Audit your application during development and fix all flagged errors as they surface.

> Checking for accessibility issues during Development is a great way to fix errors before production.

Some auditing libraries, such as `react-axe` and `eslint-plugin-jsx-a11y` are great tools you can use during the development of your React application to automatically check for accessibility issues and get notified as they surface.

## Why Audit?

Most accessibility tools are meant to be run on applications that have been deployed already, and this can result in delays and serious debugging issues.
 
- It is more of a command
- To save time
- To avoid extra debugging
- Towards mastering the art of building accessible applications

## Introduction to Axe Library

Axe is an accessibility testing engine for websites and other HTML-based user interfaces. It's fast, secure, lightweight, and was built to seamlessly integrate with any existing test environment so you can automate accessibility testing alongside your regular functional testing.
~ [Axe Docs](https://github.com/dequelabs/axe-core)

One important feature of Axe is that it works with all modern browsers, tools, CLI, and testing environments, allowing you to check for accessibility issues during development in your terminal and after deploy.

Other automated auditing tools like [Lighthouse](https://github.com/GoogleChrome/lighthouse) and [storybook-addon-a11y](https://github.com/storybooks/storybook/tree/master/addons/a11y) uses the Axe core engine which is [open sourced](https://github.com/dequelabs/axe-core).

![axe_console.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1575619602113/G1z3KkyEk.png)

## Getting Started with Axe for Browsers

Axe is available via some browser via extensions:

- [Axe Chrome Extension](https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd)
- [Axe Firefox Extension](https://addons.mozilla.org/en-US/firefox/addon/axe-devtools/)

## Getting Started with [Axe for Android](https://github.com/dequelabs/axe-android)

Axe also has an accessibility analysis tool and library for Android.

- [Download the App](https://play.google.com/store/apps/details?id=com.deque.axe.android)
- [Checkout the WCAG Accessibility compliance library for Android](https://github.com/dequelabs/axe-android)

## Getting Started with [Axe for CLI](https://github.com/dequelabs/axe-cli)

Axe also has a command-line interface for the aXe accessibility testing engine.

- Install the package

```sh
#npm
npm install axe-cli -g

#yarn
yarn install axe-cli -g
```
- Test a website with its URL

```sh
axe https://bolajiayodeji.com
```
- Test with specific rules

```sh
axe https://bolajiayodeji.com --rules color-contrast
```

## Getting Started with [Axe for React.js](https://github.com/dequelabs/react-axe)

- Install the package

```sh
#npm
npm install --save-dev react-axe

#yarn
yarn install --save-dev react-axe
```
- Initialize the module

```js
import React from 'react';
import ReactDOM from 'react-dom';

if (process.env.NODE_ENV !== 'production') {
  let axe = require('react-axe');
  axe(React, ReactDOM, 1000);
} else {
  ReactDOM.render(<App />, document.getElementById('root'));
}
```
- Add configuration rules

```js
let config = {
  rules: [
    { id: 'heading-order', enabled: true },
    { id: 'label-title-only', enabled: true },
    { id: 'link-in-text-block', enabled: true },
    { id: 'region', enabled: true },
    { id: 'skip-link', enabled: true }
  ]
};

axe(React, ReactDOM, 1000, config);
```
- Check the available Axe core configuration rules [here](https://github.com/dequelabs/axe-core/blob/master/doc/API.md#api-name-axeconfigure) and add based on your needs.

- The errors are logged with priority levels
  - Minor
  - Moderate
  - Serious
  - Critical

> **react-axe** uses advanced console logging features and works best in the Chrome browser, with limited functionality in Safari and Firefox.

## Getting Started with [Axe for Vue.js](https://github.com/vue-a11y/vue-axe)

- Install the package

```sh
#npm
npm install -D vue-axe

#yarn
yarn add -D vue-axe
```
- Initialize the module

```js
import Vue from 'vue'

if (process.env.NODE_ENV !== 'production') {
  const VueAxe = require('vue-axe')
  Vue.use(VueAxe, {
    config: {
      // ...
      rules: [
        { id: 'heading-order', enabled: true },
        { id: 'label-title-only', enabled: true },
        // and more
      ]
    }
  })
}
```

- Check the available Axe core configuration rules [here](https://github.com/dequelabs/axe-core/blob/master/doc/API.md#api-name-axeconfigure) and add based on your needs.

## Bonus: Linting with [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y)

Axe logs issues to the DevTools console on the final rendered DOM, which is great. What if you want to see these errors right in your editor or terminal? Well, you would need to set up a linter that would allow you to see accessibility issues in your JSX.

- Install [ESLint](http://eslint.org/)

```sh
# npm
npm install eslint --save-dev

# yarn
yarn add eslint --d
```

- Install the plugin

```sh
# npm
npm install eslint-plugin-jsx-a11y --save-dev

# yarn
yarn add eslint-plugin-jsx-a11y --dev
```

- Add `jsx-a11y` to your `.eslintrc` configuration file

```
{
  "plugins": [
    "jsx-a11y"
  ]
}
```

- Include all the recommended rules by the plugin 

```
{
  "extends": [
    "plugin:jsx-a11y/recommended"
  ]
}
```

- To check for more stricter rules

```
{
  "extends": [
    "plugin:jsx-a11y/strict"
  ]
}
```
See the difference between 'recommended' and 'strict' mode [here](https://github.com/evcohen/eslint-plugin-jsx-a11y#difference-between-recommended-and-strict-mode)

![eslint_demo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1575578691938/XcsL_SYl2.png)

**eslint-plugin-jsx-a11y** will also display the errors in your DevTools console if you prove to be adamant :).

![eslint_console.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1575620397277/DicVWv2Hl.png)

If your App was bootstrapped with [Create-React-App](https://github.com/facebook/create-react-app) then worry less, `eslint-jsx-a11y` is included already.

## Conclusion

The web can only become an accessible, inclusive space if developers are empowered to take responsibility for accessibility testing and accessible coding practices. ~ [Axe](https://www.deque.com/axe/)

Check out the following checklists to manually determine how accessible your site is and what accessible sites entail:

- [Checklist from The A11Y Project](https://a11yproject.com/checklist.html)
- [WCAG checklist from Wuhcag](https://www.wuhcag.com/wcag-checklist/)
- [WCAG checklist from WebAIM](https://webaim.org/standards/wcag/checklist)

Want to build better Accessible JavaScript Applications with React and Gatsby? Check out this amazing course by [Marcy](https://twitter.com/marcysutton) on FrontendMasters.

%[https://frontendmasters.com/courses/javascript-accessibility/]