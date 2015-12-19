# Redux Persist - Except "ing"s [![npm version](https://img.shields.io/npm/v/redux-persist-except-ings.svg?style=flat-square)](https://www.npmjs.com/package/redux-persist-except-ings)

Ignore event states that contains "ing", avoids stalemate occured by app restarting during events (something like `{ profileRefreshing: true }`).

Using this transform will prevent persisting (neither save or restore) all states with the `ing` keyword in it's name.

For example,

```js
{
  profile: {
    name: "Pokai Chang",
    updatedAt: "2015-12-19T16:20:40.575Z",
    updating: true
  }
}
```

will become:

```js
{
  profile: {
    name: "Pokai Chang",
    updatedAt: "2015-12-19T16:20:40.575Z"
  }
}
```

## Install

```bash
npm install redux-persist-except-ings --save
```

## Usage

```js
import { compose } from 'redux';
import { persistStore, autoRehydrate } from 'redux-persist';
import reduxPersistExpectIngs from 'redux-persist-except-ings';

const reducer = combineReducers(reducers);
const store = compose(autoRehydrate(), createStore)(reducer);

persistStore(store, { transforms: [reduxPersistExpectIngs] });
```
