# @apollo/server-integration-testsuite

## 4.1.1

### Patch Changes

- Updated dependencies [[`c835637be`](https://github.com/apollographql/apollo-server/commit/c835637be07929e3bebe8f3b262588c6d918e694)]:
  - @apollo/server@4.1.1

## 4.1.0

### Minor Changes

- [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19) Thanks [@glasser](https://github.com/glasser)! - The `cache-control` HTTP response header set by the cache control plugin now properly reflects the cache policy of all operations in a batched HTTP request. (If you write the `cache-control` response header via a different mechanism to a format that the plugin would not produce, the plugin no longer writes the header.) For more information, see [advisory GHSA-8r69-3cvp-wxc3](https://github.com/apollographql/apollo-server/security/advisories/GHSA-8r69-3cvp-wxc3).

- [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19) Thanks [@glasser](https://github.com/glasser)! - Plugins processing multiple operations in a batched HTTP request now have a shared `requestContext.request.http` object. Changes to HTTP response headers and HTTP status code made by plugins operating on one operation can be immediately seen by plugins operating on other operations in the same HTTP request.

- [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19) Thanks [@glasser](https://github.com/glasser)! - New field `GraphQLRequestContext.requestIsBatched` available to plugins.

- [#7114](https://github.com/apollographql/apollo-server/pull/7114) [`c1651bfac`](https://github.com/apollographql/apollo-server/commit/c1651bfacf8d310615be79e9246d7f0bd9bfa926) Thanks [@trevor-scheer](https://github.com/trevor-scheer)! - Directly depend on Apollo Server rather than as a peer

### Patch Changes

- Updated dependencies [[`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19), [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19), [`2a2d1e3b4`](https://github.com/apollographql/apollo-server/commit/2a2d1e3b4bbb1f2802b09004444029bd1adb9c19)]:
  - @apollo/server@4.1.0

## 4.0.5

### Patch Changes

- Updated dependencies [[`15d8d65e0`](https://github.com/apollographql/apollo-server/commit/15d8d65e018520d3eedc5e42981f19a5f98524e7), [`e4e7738be`](https://github.com/apollographql/apollo-server/commit/e4e7738be7c8d35a42342987e180eba5b6f66ca1), [`e4e7738be`](https://github.com/apollographql/apollo-server/commit/e4e7738be7c8d35a42342987e180eba5b6f66ca1), [`15d8d65e0`](https://github.com/apollographql/apollo-server/commit/15d8d65e018520d3eedc5e42981f19a5f98524e7)]:
  - @apollo/server@4.0.5

## 4.0.4

### Patch Changes

- [#7080](https://github.com/apollographql/apollo-server/pull/7080) [`540f3d97c`](https://github.com/apollographql/apollo-server/commit/540f3d97c30a4892cd4b9a87ba2b26464df74a82) Thanks [@martinnabhan](https://github.com/martinnabhan)! - Recognize malformed JSON error messages from Next.js.

- Updated dependencies []:
  - @apollo/server@4.0.4

## 4.0.3

### Patch Changes

- [#7073](https://github.com/apollographql/apollo-server/pull/7073) [`e7f524eac`](https://github.com/apollographql/apollo-server/commit/e7f524eacad915cbdadeba22827ff039bd8c7390) Thanks [@glasser](https://github.com/glasser)! - Never interpret `GET` requests as batched. In previous versions of Apollo Server 4, a `GET` request whose body was a JSON array with N elements would be interpreted as a batch of the operation specified in the query string repeated N times. Now we just ignore the body for `GET` requests (like in Apollo Server 3), and never treat them as batched.

- [#7071](https://github.com/apollographql/apollo-server/pull/7071) [`0ed389ce8`](https://github.com/apollographql/apollo-server/commit/0ed389ce81bd1783890d86151b174133f0244c92) Thanks [@glasser](https://github.com/glasser)! - Fix v4 regression: gateway implementations should be able to set HTTP response headers and the status code.

- Updated dependencies [[`e7f524eac`](https://github.com/apollographql/apollo-server/commit/e7f524eacad915cbdadeba22827ff039bd8c7390), [`0ed389ce8`](https://github.com/apollographql/apollo-server/commit/0ed389ce81bd1783890d86151b174133f0244c92)]:
  - @apollo/server@4.0.3

## 4.0.2

### Patch Changes

- [#7035](https://github.com/apollographql/apollo-server/pull/7035) [`b3f400063`](https://github.com/apollographql/apollo-server/commit/b3f4000633a9dc5ef983b97e46cba29507ee2955) Thanks [@barryhagan](https://github.com/barryhagan)! - Errors resulting from an attempt to use introspection when it is not enabled now have an additional `validationErrorCode: 'INTROSPECTION_DISABLED'` extension; this value is part of a new enum `ApolloServerValidationErrorCode` exported from `@apollo/server/errors`.

- [#7066](https://github.com/apollographql/apollo-server/pull/7066) [`f11d55a83`](https://github.com/apollographql/apollo-server/commit/f11d55a83cf0300cf31674311e72cb7703c70040) Thanks [@trevor-scheer](https://github.com/trevor-scheer)! - Add a test to validate error message and code for invalid operation names via GET

- [#7055](https://github.com/apollographql/apollo-server/pull/7055) [`d0d8f4be7`](https://github.com/apollographql/apollo-server/commit/d0d8f4be705065745bd3767a62b8025abe774842) Thanks [@trevor-scheer](https://github.com/trevor-scheer)! - Fix build configuration issue and align on CJS correctly

- Updated dependencies [[`b3f400063`](https://github.com/apollographql/apollo-server/commit/b3f4000633a9dc5ef983b97e46cba29507ee2955)]:
  - @apollo/server@4.0.2

## 4.0.1

### Patch Changes

- [#7049](https://github.com/apollographql/apollo-server/pull/7049) [`3daee02c6`](https://github.com/apollographql/apollo-server/commit/3daee02c6a0fa34ea0e6f4f18b9a7308539021e3) Thanks [@glasser](https://github.com/glasser)! - Raise minimum `engines` requirement from Node.js v14.0.0 to v14.16.0. This is the minimum version of Node 14 supported by the `engines` requirement of `graphql@16.6.0`.

- Updated dependencies [[`3daee02c6`](https://github.com/apollographql/apollo-server/commit/3daee02c6a0fa34ea0e6f4f18b9a7308539021e3), [`3daee02c6`](https://github.com/apollographql/apollo-server/commit/3daee02c6a0fa34ea0e6f4f18b9a7308539021e3)]:
  - @apollo/server@4.0.1

## 4.0.0

Initial release of `@apollo/server-integration-testsuite`.
