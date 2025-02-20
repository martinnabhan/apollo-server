# @apollo/server

## 4.1.1

### Patch Changes

- [#7118](https://github.com/apollographql/apollo-server/pull/7118) [`c835637be`](https://github.com/apollographql/apollo-server/commit/c835637be07929e3bebe8f3b262588c6d918e694) Thanks [@glasser](https://github.com/glasser)! - Provide new `GraphQLRequestContext.requestIsBatched` field to gateways, because we did add it in a backport to AS3 and the gateway interface is based on AS3.

- Updated dependencies [[`c835637be`](https://github.com/apollographql/apollo-server/commit/c835637be07929e3bebe8f3b262588c6d918e694)]:
  - @apollo/server-gateway-interface@1.0.5

## 4.1.0

### Minor Changes

- [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19) Thanks [@glasser](https://github.com/glasser)! - The `cache-control` HTTP response header set by the cache control plugin now properly reflects the cache policy of all operations in a batched HTTP request. (If you write the `cache-control` response header via a different mechanism to a format that the plugin would not produce, the plugin no longer writes the header.) For more information, see [advisory GHSA-8r69-3cvp-wxc3](https://github.com/apollographql/apollo-server/security/advisories/GHSA-8r69-3cvp-wxc3).

- [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19) Thanks [@glasser](https://github.com/glasser)! - Plugins processing multiple operations in a batched HTTP request now have a shared `requestContext.request.http` object. Changes to HTTP response headers and HTTP status code made by plugins operating on one operation can be immediately seen by plugins operating on other operations in the same HTTP request.

- [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19) Thanks [@glasser](https://github.com/glasser)! - New field `GraphQLRequestContext.requestIsBatched` available to plugins.

## 4.0.5

### Patch Changes

- [#7104](https://github.com/apollographql/apollo-server/pull/7104) [`15d8d65e0`](https://github.com/apollographql/apollo-server/commit/15d8d65e018520d3eedc5e42981f19a5f98524e7) Thanks [@glasser](https://github.com/glasser)! - New `ApolloServerPluginSchemaReportingDisabled` plugin which can override the `APOLLO_SCHEMA_REPORTING` environment variable.

- [#7101](https://github.com/apollographql/apollo-server/pull/7101) [`e4e7738be`](https://github.com/apollographql/apollo-server/commit/e4e7738be7c8d35a42342987e180eba5b6f66ca1) Thanks [@glasser](https://github.com/glasser)! - Manage memory more efficiently in the usage reporting plugin by allowing large objects to be garbage collected more quickly.

- [#7101](https://github.com/apollographql/apollo-server/pull/7101) [`e4e7738be`](https://github.com/apollographql/apollo-server/commit/e4e7738be7c8d35a42342987e180eba5b6f66ca1) Thanks [@glasser](https://github.com/glasser)! - The usage reporting plugin now defaults to a 30 second timeout for each attempt to send reports to Apollo Server instead of no timeout; the timeout can be adjusted with the new `requestTimeoutMs` option to `ApolloServerPluginUsageReporting`. (Apollo's servers already enforced a 30 second timeout, so this is unlikely to break any existing use cases.)

- [#7104](https://github.com/apollographql/apollo-server/pull/7104) [`15d8d65e0`](https://github.com/apollographql/apollo-server/commit/15d8d65e018520d3eedc5e42981f19a5f98524e7) Thanks [@glasser](https://github.com/glasser)! - It is now an error to combine a "disabled" plugin such as `ApolloServerPluginUsageReportingDisabled` with its enabled counterpart such as `ApolloServerPluginUsageReporting`.

## 4.0.4

This version has no changes; `@apollo/server` and `@apollo/server-integration-test` are published with matching version numbers and we published a new version of `@apollo/server-integration-test`.

## 4.0.3

### Patch Changes

- [#7073](https://github.com/apollographql/apollo-server/pull/7073) [`e7f524eac`](https://github.com/apollographql/apollo-server/commit/e7f524eacad915cbdadeba22827ff039bd8c7390) Thanks [@glasser](https://github.com/glasser)! - Never interpret `GET` requests as batched. In previous versions of Apollo Server 4, a `GET` request whose body was a JSON array with N elements would be interpreted as a batch of the operation specified in the query string repeated N times. Now we just ignore the body for `GET` requests (like in Apollo Server 3), and never treat them as batched.

- [#7071](https://github.com/apollographql/apollo-server/pull/7071) [`0ed389ce8`](https://github.com/apollographql/apollo-server/commit/0ed389ce81bd1783890d86151b174133f0244c92) Thanks [@glasser](https://github.com/glasser)! - Fix v4 regression: gateway implementations should be able to set HTTP response headers and the status code.

## 4.0.2

### Patch Changes

- [#7035](https://github.com/apollographql/apollo-server/pull/7035) [`b3f400063`](https://github.com/apollographql/apollo-server/commit/b3f4000633a9dc5ef983b97e46cba29507ee2955) Thanks [@barryhagan](https://github.com/barryhagan)! - Errors resulting from an attempt to use introspection when it is not enabled now have an additional `validationErrorCode: 'INTROSPECTION_DISABLED'` extension; this value is part of a new enum `ApolloServerValidationErrorCode` exported from `@apollo/server/errors`.

## 4.0.1

### Patch Changes

- [#7049](https://github.com/apollographql/apollo-server/pull/7049) [`3daee02c6`](https://github.com/apollographql/apollo-server/commit/3daee02c6a0fa34ea0e6f4f18b9a7308539021e3) Thanks [@glasser](https://github.com/glasser)! - Raise minimum `engines` requirement from Node.js v14.0.0 to v14.16.0. This is the minimum version of Node 14 supported by the `engines` requirement of `graphql@16.6.0`.

- [#7049](https://github.com/apollographql/apollo-server/pull/7049) [`3daee02c6`](https://github.com/apollographql/apollo-server/commit/3daee02c6a0fa34ea0e6f4f18b9a7308539021e3) Thanks [@glasser](https://github.com/glasser)! - Require Node.js v14 rather than v12. This change was intended for v4.0.0 and the documentation already stated this requirement, but was left off of the package.json `engines` field in `@apollo/server` inadvertently.

## 4.0.0

### BREAKING CHANGES

Apollo Server contains quite a few breaking changes: most notably, a brand new package name! Read our [migration guide](https://www.apollographql.com/docs/apollo-server/migration/) for more details on how to update your app.

#### Bumped dependencies

The minimum versions of these dependencies have been bumped to provide an improved foundation for the development of future features.

- Dropped support for Node.js v12, which is no longer under [long-term support](https://nodejs.org/en/about/releases/#releases) from the Node.js Foundation.
- Dropped support for versions of the `graphql` library prior to `v16.6.0`.
  - Upgrading `graphql` may require you to upgrade other libraries that are installed in your project. For example, if you use Apollo Server with Apollo Gateway, you should upgrade Apollo Gateway to at least v0.50.1 or any v2.x version for full `graphql` 16 support before upgrading to Apollo Server 4.
- If you use Apollo Server with TypeScript, you must use TypeScript v4.7.0 or newer.

#### New package structure

Apollo Server 4 is distributed in the `@apollo/server` package. This package replaces `apollo-server`, `apollo-server-core`, `apollo-server-express`, `apollo-server-errors`, `apollo-server-types`, and `apollo-server-plugin-base`.

The `@apollo/server` package exports the `ApolloServer` class. In Apollo Server 3, individual web framework integrations had their own subclasses of `ApolloServer`. In Apollo Server 4, there is a single `ApolloServer` class; web framework integrations define their own functions which use a new stable integration API on `ApolloServer` to execute operations.

Other functionality is exported from "deep imports" on `@apollo/server`. `startStandaloneServer` (the replacement for the batteries-included `apollo-server` package) is exported from `@apollo/server/standalone`. `expressMiddleware` (the replacement for `apollo-server-express`) is exported from `@apollo/server/express4`. Plugins such as `ApolloServerPluginUsageReporting` are exported from paths such as `@apollo/server/plugin/usageReporting`.

The `@apollo/server` package is built natively as both an ECMAScript Module (ESM) and as a CommonJS module (CJS); Apollo Server 3 was only built as CJS. This allows ESM-native bundlers to create more efficient bundles.

Other packages have been renamed:

- `apollo-datasource-rest` is now [`@apollo/datasource-rest`](https://www.npmjs.com/package/@apollo/datasource-rest).
- `apollo-server-plugin-response-cache` is now [`@apollo/server-plugin-response-cache`](https://www.npmjs.com/package/@apollo/server-plugin-response-cache).
- `apollo-server-plugin-operation-registry` is now [`@apollo/server-plugin-operation-registry`](https://www.npmjs.com/package/@apollo/server-plugin-operation-registry).
- `apollo-reporting-protobuf` (an internal implementation detail for the usage reporting plugin) is now [`@apollo/usage-reporting-protobuf`](https://www.npmjs.com/package/@apollo/usage-reporting-protobuf).

#### Removed web framework integrations

Prior to Apollo Server 4, the only way to integrate a web framework with Apollo Server was for the Apollo Server project to add an official `apollo-server-x` subclass maintained as part of the core project. Apollo Server 4 makes it easy for users to integrate with their favorite web framework, and so we have removed most of the framework integrations from the core project so that framework integrations can be maintained by users who are passionate about that framework. Because of this, the core project no longer directly maintains integrations for Fastify, Hapi, Koa, Micro, AWS Lambda,Google Cloud Functions, Azure Functions, or Cloudflare. We expect that [community integrations](https://www.apollographql.com/docs/apollo-server/v4/integrations/integration-index/) will eventually be created for most of these frameworks and serverless environments.

Apollo Server's support for the Express web framework no longer also supports its older predecessor [Connect](https://github.com/senchalabs/connect).

#### Removed constructor options

- The `dataSources` constructor option essentially added a post-processing step to your app's context function, creating `DataSource` subclasses and adding them to a `dataSources` field on your context value. This meant the TypeScript type the `context` function returns was _different_ from the context type your resolvers and plugins receive. Additionally, this design obfuscated that `DataSource` objects are created once per request (i.e., like the rest of the context object). Apollo Server 4 removes the `dataSources` constructor option. You can now treat `DataSources` like any other part of your `context` object. See the [migration guide](https://www.apollographql.com/docs/apollo-server/migration/) for details on how to move your `dataSources` function into your `context` function.
- The `modules` constructor option was just a slightly different way of writing `typeDefs` and `resolvers` (although it surprisingly used entirely different logic under the hood). This option has been removed.
- The `mocks` and `mockEntireSchema` constructor options wrapped an outdated version of the [`@graphql-tools/mocks`](https://www.npmjs.com/package/@graphql-tools/mock) library to provide mocking functionality. These constructor options have been removed; you can instead directly incorporate the `@graphql-tools/mock` package into your app, enabling you to get the most up-to-date mocking features.
- The `debug` constructor option (which defaulted to `true` unless the `NODE_ENV` environment variable is either `production` or `test`) mostly controlled whether GraphQL errors responses included stack traces, but it also affected the default log level on the default logger. The `debug` constructor option has been removed and is replaced with `includeStacktraceInErrorResponses`, which does exactly what it says it does.
- The `formatResponse` constructor option has been removed; its functionality can be replaced by the `willSendResponse` plugin hook.
- The `executor` constructor option has been removed; the ability to replace `graphql-js`'s execution functionality is still available via the `gateway` option.

#### Removed features

- Apollo Server 4 no longer responds to health checks on the path `/.well-known/apollo/server-health`. You can run a trivial GraphQL operation as a health check, or you can add a custom health check via your web framework.
- Apollo Server 4 no longer cares what URL path is used to access its functionality. Instead of specifying the `path` option to various Apollo Server methods, just use your web framework's routing feature to mount the Apollo Server integration at the appropriate path.
- Apollo Server 4's Express middleware no longer wraps the `body-parser` and `cors` middleware; it is your responsibility to install and set up these middleware yourself when using a framework integration. (The standalone HTTP server sets up body parsing and CORS for you, but without the ability to configure their details.)
- Apollo Server no longer re-exports the `gql` tag function from `graphql-tag`. If you want to use `gql`, install the `graphql-tag` package.
- Apollo Server no longer defines its own `ApolloError` class and `toApolloError` function. Instead, use `GraphQLError` from the `graphql` package.
- Apollo Server no longer exports error subclasses representing the errors that it creates, such as `SyntaxError`. Instead, it exports an enum `ApolloServerErrorCode` that you can use to recognize errors created by Apollo Server.
- Apollo Server no longer exports the `ForbiddenError` and `AuthenticationError` classes. Instead, you can define your own error codes for these errors or other errors.
- The undocumented `__resolveObject` pseudo-resolver is no longer supported.
- The `requestAgent` option to `ApolloServerPluginUsageReporting` has been removed.
- In the JSON body of a `POST` request, the `variables` and `extensions` fields must be objects, not JSON-encoded strings.
- The core Apollo Server packages no longer provide a landing page plugin for the unmaintained GraphQL Playground UI. We have published an Apollo Server 4-compatible landing page plugin in the package `@apollo/server-plugin-landing-page-graphql-playground`, but do not intend to maintain it further after this one-time publish.

#### Modified functionality

- The `context` function is now provided to your integration function (such as `startStandaloneServer` or `expressMiddleware`) rather than to the `new ApolloServer` constructor.
- The `executeOperation` method now directly accepts a context value, rather than accepting the arguments to your `context` function.
- The `formatError` hook now receives the original thrown error in addition to the formatted error.
- Formatted errors no longer contain the `extensions.exception` field containing all enumerable properties of the originally thrown error. If you want to include more information in an error, specify them as `extensions` when creating a `GraphQLError`. The `stacktrace` field is provided directly on `extensions` rather than nested under `exception`.
- All errors responses are consistently rendered as `application/json` JSON responses, and the `formatError` hook is used consistently.
- Other [changes to error handling outside of resolvers](https://www.apollographql.com/docs/apollo-server/migration/#improvements-to-error-handling-outside-of-resolvers) are described in the migration guide.
- The `parseOptions` constructor option only affects the parsing of incoming operations, not the parsing of `typeDefs`.

#### Plugin API changes

- The field `GraphQLRequestContext.context` has been renamed to `contextValue`.
- The field `GraphQLRequestContext.logger` is now readonly.
- The fields `GraphQLRequestContext.schemaHash` and `GraphQLRequestContext.debug` have been removed.
- The type `GraphQLServiceContext` has been renamed to `GraphQLServerContext`, and the fields `schemaHash`, `persistedQueries`, and `serverlessFramework` have been removed; the latter has been semi-replaced by `startedInBackground`.
- The `http` field on the `GraphQLRequest` object (available to plugins as `requestContext.request` and as an argument to `server.executeOperation`) is no longer based on the Fetch API's `Request` object. It no longer contains an URL path, and its `headers` field is a `Map` rather than a `Headers` object.
- The structure of the `GraphQLResponse` object (available to plugins as `requestContext.response` and as the return value from `server.executeOperation`) has [changed in several ways](https://www.apollographql.com/docs/apollo-server/migration/#graphqlresponse).
- The `plugins` constructor argument does not take factory functions.
- `requestDidStart` hooks are called in parallel rather than in series.
- A few changes have been made which may affect [custom `gateway` and `GraphQLDataSource` implementations](https://www.apollographql.com/docs/apollo-server/migration/#custom-gateway-and-graphqldatasource-implementations).

#### Changes to defaults

- CSRF prevention is on by default.
- HTTP batching is disabled by default.
- The default in-memory cache is bounded.
- The local landing page defaults to the _embedded_ Apollo Sandbox; this provides a user interface for executing GraphQL operations which doesn't require any additional CORS configuration.
- The usage reporting and inline trace plugins mask errors in their reports by default: error messages are replaced with `<masked>` and error extensions are replaced with a single extension `maskedBy`. This can be configured with the `sendErrors` option to `ApolloServerPluginUsageReporting` and the `includeErrors` option to `ApolloServerPluginInlineTrace`. The `rewriteError` option to these plugins has been removed; its functionality is subsumed by the new options.

#### TypeScript-specific changes

- The TypeScript types for the `validationRules` constructor option are more accurate.
- We now use the `@apollo/utils.fetcher` package to define the shape of the Fetch API, instead of `apollo-server-env`. This package only supports argument structures that are likely to be compatible across implementations of the Fetch API.
- The `CacheScope`, `CacheHint`, `CacheAnnotation`, `CachePolicy`, and `ResolveInfoCacheControl` types are now exported from the `@apollo/cache-control-types` package. `CacheScope` is now a pure TypeScript type rather than an enum.
- The type for `ApolloServer`'s constructor options argument is now `ApolloServerOptions`, not `Config` or `ApolloServerExpressConfig`.
- Some other types have been renamed or removed; see the migration guide for details.

### New features

- In TypeScript, you can now declare your server's context value type using generic type syntax, like `new ApolloServer<MyContextType>`. This ensures that the type returned by your context function matches the context type provided to your resolvers and plugins.
- `ApolloServer` now has a well-documented API for integrating with web frameworks, featuring the new `executeHTTPGraphQLRequest` method.
- `ApolloServer` now has explicit support for the "serverless" style of startup error handling. Serverless frameworks generally do not allow handlers to do "async" work during startup, so any failure to load the schema or run `serverWillStart` handlers can't prevent requests from being served. Apollo Server 4 provides a `server.startInBackgroundHandlingStartupErrorsByLoggingAndFailingAllRequests()` method as an alternative to `await server.start()` for use in contexts like serverless environments.
- You can add a plugin to a server with `server.addPlugin()`. Plugins can only be added before the server is `start`ed. This allows you to pass the server itself as an argument to the plugin.
- `ApolloServer` has new public readonly `cache` and `logger` fields.
- When combined with `graphql` v17 (only available as pre-releases as of September 2022), Apollo Server now has experimental support for [incremental delivery](https://www.apollographql.com/docs/apollo-server/workflow/requests/#incremental-delivery-experimental) directives such as `@defer` and `@stream`.
- Apollo Server 4 adds new plugin hooks `startupDidFail`, `contextCreationDidFail`, `invalidRequestWasReceived`, `unexpectedErrorProcessingRequest`, `didEncounterSubsequentErrors`, and `willSendSubsequentPayload`.
- If Apollo Server receives an operation while the server is shutting down, it now logs a warning telling you to properly configure HTTP server draining.
- Apollo Server now supports responses with `content-type: application/graphql-response+json` when requested by clients via the `accept` header, as described in the [GraphQL over HTTP specification proposal](https://github.com/graphql/graphql-over-http).

## Versions prior to 4.0.0

The first version of Apollo Server published in the `@apollo/server` package is v4.0.0. Before this release, all Apollo Server packages tracked their changes in a single file, which can be found at [`CHANGELOG_historical.md`](http://github.com/apollographql/apollo-server/blob/main/CHANGELOG_historical.md).
