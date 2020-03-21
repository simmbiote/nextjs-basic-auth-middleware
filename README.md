# nextjs-basic-auth-middleware

Adds basic auth to a NextJS project on a document level.
Options can be set on the basic auth middleware and overriden using environment variables.

This project was bootstrapped with [TSDX](https://github.com/jaredpalmer/tsdx).

## Installation

Run either of the following commands to add the package, based on your package manager of choice:

```sh
# NPM
npm install nextjs-basic-auth-middleware

# Yarn
yarn add nextjs-basic-auth-middleware
```

## Usage

> **NOTE**
> This library requires you to set an experimental config option for
> middleware support on a document level.

Set the following configuration option in your `next.config.js`:

```js
    experimental: {
        documentMiddleware: true
    }
```

Then add the middleware to the `getInitialProps` method of your document:

```js
    Document.getInitialProps = async ({req, res}) => {
        await basicAuthMiddleware(req, res)
        ...
    }
```

### Setting environment variables
If you want to override credentials you can use the `BASIC_AUTH_CREDENTIALS` environment variable:

```sh
# Enables basic auth for user `test` with password `password`
BASIC_AUTH_CREDENTIALS=user:password

# You can set multiple accounts using `|` as a delimiter
BASIC_AUTH_CREDENTIALS=user:password|user2:password2
```

Users set using environment variables will override and thus disable users set in options.

## API
### basicAuthMiddleware()
```basicAuthMiddleware(reg: http.IncomingMessage, res: http.ServerResponse, options)```

The options object can contain any of the following options:

option | description | default value
------ | ----------- | -------------
`realm`| The name of the basic auth realm | `'Protected'`
`users`| A list of users that can authenticate | `[]`

The user object consists of the following required fields:

field | description | type
----- | ----------- | ----
`name`| The username | `string`
`password`| The password | `string`


## Local Development

Below is a list of commands you will probably find useful.

### `npm start` or `yarn start`

Runs the project in development/watch mode. Your project will be rebuilt upon changes. TSDX has a special logger for your convenience. Error messages are pretty printed and formatted for compatibility VS Code's Problems tab.

<img src="https://user-images.githubusercontent.com/4060187/52168303-574d3a00-26f6-11e9-9f3b-71dbec9ebfcb.gif" width="600" />

Your library will be rebuilt if you make edits.

### `npm run build` or `yarn build`

Bundles the package to the `dist` folder.
The package is optimized and bundled with Rollup into multiple formats (CommonJS, UMD, and ES Module).

<img src="https://user-images.githubusercontent.com/4060187/52168322-a98e5b00-26f6-11e9-8cf6-222d716b75ef.gif" width="600" />

### `npm test` or `yarn test`

Runs the test watcher (Jest) in an interactive mode.
By default, runs tests related to files changed since the last commit.
