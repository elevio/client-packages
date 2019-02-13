# client-packages

This repository contains all the packages to install [Elev.io](https://elev.io/) into your site using a npm package.
Currently there are two packages, one that gives you imperative functions to call and the other is a React integration.

## Usage

### Npm module

Install the package with

```
npm i elevio
```

### Normal api usage (non-React)

Then you can pull in the Elevio package

```js
import Elevio from 'elevio/client';
```

or

```js
import { client as Elevio } from 'elevio';
```

Then make sure before you call any other functions you call the `load` function and pass in your account id see the [installation](https://app.elev.io/installation) page to get our account id. This loads the Elevio javascript and sets up the javascript ready to use.

**NOTE:** You are free to use the `on` function to setup any event listens at any time you like, so you dont' have to wait for the `load` function to complete before calling that.

```js
Elevio.load('my-account-id').then(() => {
  console.log('Elevio has loaded, ready to use!');
});
```

Then you are free to call any functions you like, so if you want to open the assistant you can do this

```js
Elevio.open();
Elevio.setKeywords(['keyword1', 'keyword2']);
```

To subscribe to events you can use the `on` function, like so

```js
Elevio.on('widget:opened', () => {
  console.log('Elevio has opened!!!');
});

Elevio.on('widget:closed', () => {
  console.log('Elevio has closed!!!');
});
```

### React usage

Import the package

```jsx
import Elevio from 'elevio/react';
```

Then drop the Elevio component into your component hierarchy, making sure you pass the required account id.

```jsx
<div>
  <Elevio accountId="MY_ACCOUNT_ID" />
</div>
```

You can also pass any `on` functions you like to get notified of when things occur. See [https://github.com/elevio/client-packages/blob/master/src/react.tsx](https://github.com/elevio/client-packages/blob/master/src/react.tsx) for the documentation of available props.

**_NOTE_**
you can also use a combination of the standard client usage if you want to do something imperative or something that isn't supported by the React wrapper.

## Building

To build these packages first close this repository and then install all the decencies.

```bash
npm i
```

Then you can rebuild all the packages by running the npm script `build`.

```
npm run build
```

This the package and puts the build files in the `dist` folder.

## Running examples

First install all dependencies by running `npm install`.

Then run one of the example scripts.
Have a look in the examples directory for a list of the examples.

For the simple example run `npm run example:simple`.
To run the React example run `npm run example:react-simple`.

## Submitting issues / pull requests

If you find an issue or something missing with these packages please feel free to open a ticket. It's helpful if you can describe how the issue is occurring and what your desired outcome is.

## Typescript support

These packages have been built using Typescript and the type definitions are included in the package.

NOTE due to a limitation of TS (currently using TS 3.3) to get type safety for the callback function of the `on` you have to provide the string on the event you want to use as a generic, so for example, if you want to set a `'load'` callback you would:

```typescript
Elevio.on<'load'>('load', elev => {
  // Now the elev variable is correctly typed to the particular callback.
});
```