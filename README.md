# SEC Directory Screens Client

[![Test and Build](https://github.com/seas-computing/sec-directory-client/actions/workflows/test-build.yml/badge.svg)](https://github.com/seas-computing/sec-directory-client/actions/workflows/test-build.yml)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v1.4%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)
[![BSD License](https://img.shields.io/github/license/seas-computing/mark-one)](LICENSE)

This is the react-based client application for the Directory Screen on the SEAS Allston Campus. It was bootstrapped with [Create React App][cra] using the default Typescript template.

This is meant to be used in conjunction with the [sec-directory-server][server] project, which is responsible for populating the Algolia database, and will be displayed on the SEAS Allston campus.

## Setup

1. Clone this repo
2. Run `npm install` to get all dependencies
3. Copy `.env.example` to `.env` and populate with the desired Algolia details

## Algolia

The backend of the application is the Algolia search index defined in the `REACT_APP_ALGOLIA_INDEX`/`REACT_APP_ALGOLIA_APP_ID` environment variable. You'll also need to provide an API key in `REACT_APP_ALGOLIA_API_KEY`, which should only have "search" permissions for the specified index. **This API key will be included verbatim in the client code, so you should never use an admin key, or any key with write permission.** Best practice is [to create a "Secured API Key"][api-key] scoped only to the index you want to use.

## Local Development

`npm run start` will bring up a live development environment with hot-reloading. Once it's started, you can view the app in the browser at http://localhost:3000/.

As we're building for specific 55" touch screen displays ([Planar PS5561T][planar]) in portrait mode, the design of the page is fixed to a 1080x1920 rectangle with scrolling and pinch-to-zoom disabled. To view the application on a standard screen, you can use the [Responsive Design Mode][rdm] built into most browsers to emulate a 1080x1920 viewport.

The only outbound data connections are to Algolia, so the server project does not need to be running at the same time.

### Development Index

Ideally, each developer working on the project should create their own Algolia index (and corresponding API Key) to use while developing. You can use the same index for both client and server operations, though the server application does require an API key with write permission. As noted above, you should use a [Secured API Key][api-key] and not an admin key.

## Testing

`npm run test` will run the Jest test suite. By default, Jest will run in watch mode and re-run tests whenever the code changes on disk. For more information on Jest and its features, see [the project homepage][jest].

### Test Index

You can optionally create a file called `.env.test` if you want to specify a separate index for testing. This is recommended, as some of the end-to-end tests defined in `src/__tests__/e2e.test.tsx` expect the index to include to include actual data, and keeping a separate test index can reduce phantom test failures.

## Production Build

`npm run build` will compile the full application in `/build`.

The official build of our code is handled by GitHub actions, and will be published to the [releases section][releases] on every push to our main branch if all the tests pass.

In production, the app will be server from an Amazon S3 bucket behind CloudFront.

[cra]: https://create-react-app.dev/
[server]: https://github.com/seas-computing/sec-directory-server
[api-key]: https://www.algolia.com/doc/guides/security/api-keys/#secured-api-keys
[planar]: https://www.planar.com/products/large-format-displays/ps4k/planar-ps5561t/
[rdm]: https://developer.mozilla.org/en-US/docs/Tools/Responsive_Design_Mode
[jest]: https://jestjs.io/
[rtl]: https://testing-library.com/docs/react-testing-library/intro/
[releases]: https://github.com/seas-computing/sec-directory-client/releases
