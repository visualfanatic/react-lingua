# react-lingua ![Build](https://action-badges.now.sh/visualfanatic/react-lingua)

A simple i18n engine for React.

## Installation

```
yarn add react-lingua
```

```
npm i react-lingua
```

## Main goals

* Lightweight & fast
* No dependencies
* Ability to dynamically change locale
* Hooks!
* Placeholder replacement
* Ability to embed HTML & JSX inside translations
* Simple namespacing (using `namespaceName:translationId` notation)

## Usage

```jsx
// src/App.js
import * as React from 'react';
import { render } from 'react-dom';
import { I18nProvider } from 'react-lingua';
import { Main } from './Main';

const translations = {
  'en-US': {
    helloWorld: 'Hello World!',
    welcome: 'Nice to meet you, {name}!',
    info: 'Example paragraph {someComp}.',
    infoPart: 'with JSX inside',
  },
  'pl-PL': {
    helloWorld: 'Witaj Świecie!',
    welcome: 'Miło Cię poznać, {name}!',
    info: 'Przykładowo paragraf {someComp}.',
    infoPart: 'z JSXem w środku',
  },
};

const App = () => (
  <I18nProvider
    initialLocale="en-US"
    translations={translations}
    onChange={(prevLocale, newLocale) => console.log(`Changed from ${prevLocale} to ${newLocale}`)}
  >
    <Main />
  </I18nProvider>
);

render(<App />, document.getElementById('app'));
```

```jsx
// src/Main.js
import * as React from 'react';
import { Translation, useTranslation } from 'react-lingua';

export const Main = () => {
  const { t, locale, setLocale } = useTranslation();

  return (
    <main>
      <h1>{t('helloWorld')}</h1>
      <h2>{t('welcome', { name: 'Dominika' })}</h2>
      <p>
        <Translation
          id="info"
          values={{
            someComp: <strong>{t('infoPart')}</strong>
          }}
        />
      </p>
    </main>
  );
};
```

## TODO

* Prepare live examples (preferably on codesandbox.io)
* Figure out the most efficient way of importing locales that are not used
* Maybe a better directory structure
* A bit more tests
* A bit better typings
* Add a few comments here and there for better DX
* Add API section to README
