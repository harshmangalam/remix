# `@remix-run/serve`

## 2.0.0

### Major Changes

- `remix-serve` now picks an open port if 3000 is taken ([#7278](https://github.com/remix-run/remix/pull/7278))
  - If `PORT` env var is set, `remix-serve` will use that port
  - Otherwise, `remix-serve` picks an open port (3000 unless that is already taken)
- Integrate manual mode in `remix-serve` ([#7231](https://github.com/remix-run/remix/pull/7231))
- Remove undocumented `createApp` Node API ([#7229](https://github.com/remix-run/remix/pull/7229))
  - `remix-serve` is a CLI, not a library
- Require Node >=18.0.0 ([#6939](https://github.com/remix-run/remix/pull/6939))
- Promote the `future.v2_dev` flag in `remix.config.js` to a root level `dev` config ([#7002](https://github.com/remix-run/remix/pull/7002))
- Default to `serverModuleFormat: "esm"` and update `remix-serve` to use dynamic import to support ESM and CJS build outputs ([#6949](https://github.com/remix-run/remix/pull/6949))
- Preserve dynamic imports in `remix-serve` for external bundle ([#7173](https://github.com/remix-run/remix/pull/7173))
- For preparation of using Node's built in fetch implementation, installing the fetch globals is now a responsibility of the app server ([#7009](https://github.com/remix-run/remix/pull/7009))

  - If you are using `remix-serve`, nothing is required
  - If you are using your own app server, you will need to install the globals yourself

    ```js filename=server.js
    import { installGlobals } from "@remix-run/node";

    installGlobals();
    ```

- `source-map-support` is now a responsibility of the app server ([#7009](https://github.com/remix-run/remix/pull/7009))

  - If you are using `remix-serve`, nothing is required
  - If you are using your own app server, you will need to install [`source-map-support`](https://www.npmjs.com/package/source-map-support) yourself.

    ```sh
    npm i source-map-support
    ```

    ```js filename=server.js
    import sourceMapSupport from "source-map-support";
    sourceMapSupport.install();
    ```

### Patch Changes

- Update `remix-serve` usage error message to support ESM projects ([#7400](https://github.com/remix-run/remix/pull/7400))
- Updated dependencies:
  - `@remix-run/node@2.0.0`
  - `@remix-run/express@2.0.0`

## 1.19.3

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.19.3`
  - `@remix-run/node@1.19.3`

## 1.19.2

### Patch Changes

- Install `source-map-support` ([#7039](https://github.com/remix-run/remix/pull/7039))
- Updated dependencies:
  - `@remix-run/node@1.19.2`
  - `@remix-run/express@1.19.2`

## 1.19.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.19.1`
  - `@remix-run/node@1.19.1`

## 1.19.0

### Patch Changes

- Updated dependencies:
  - `@remix-run/node@1.19.0`
  - `@remix-run/express@1.19.0`

## 1.18.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/node@1.18.1`
  - `@remix-run/express@1.18.1`

## 1.18.0

### Minor Changes

- stabilize v2 dev server ([#6615](https://github.com/remix-run/remix/pull/6615))

### Patch Changes

- fix(types): better tuple serialization types ([#6616](https://github.com/remix-run/remix/pull/6616))
- Updated dependencies:
  - `@remix-run/node@1.18.0`
  - `@remix-run/express@1.18.0`

## 1.17.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.17.1`
  - `@remix-run/node@1.17.1`

## 1.17.0

### Patch Changes

- Add `HeadersArgs` type to be consistent with loaders/actions/meta and allows for using a `function` declaration in addition to an arrow function expression ([#6247](https://github.com/remix-run/remix/pull/6247))

  ```tsx
  import type { HeadersArgs } from "@remix-run/node"; // or cloudflare/deno

  export function headers({ loaderHeaders }: HeadersArgs) {
    return {
      "x-my-custom-thing": loaderHeaders.get("x-my-custom-thing") || "fallback",
    };
  }
  ```

- Updated dependencies:
  - `@remix-run/node@1.17.0`
  - `@remix-run/express@1.17.0`

## 1.16.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/node@1.16.1`
  - `@remix-run/express@1.16.1`

## 1.16.0

### Patch Changes

- add `@remix-run/node/install` side-effect to allow `node --require @remix-run/node/install` ([#6132](https://github.com/remix-run/remix/pull/6132))
- Updated dependencies:
  - `@remix-run/express@1.16.0`
  - `@remix-run/node@1.16.0`

## 1.15.0

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.15.0`

## 1.14.3

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.14.3`

## 1.14.2

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.14.2`

## 1.14.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.14.1`

## 1.14.0

### Patch Changes

- Allow configurable `NODE_ENV` with `remix-serve` ([#5540](https://github.com/remix-run/remix/pull/5540))
- Sync `FutureConfig` interface between packages ([#5398](https://github.com/remix-run/remix/pull/5398))
- Updated dependencies:
  - `@remix-run/express@1.14.0`

## 1.13.0

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.13.0`

## 1.12.0

### Minor Changes

- Added a new development server available in the Remix config under the `unstable_dev` flag. [See the release notes](https://github.com/remix-run/remix/releases/tag/remix%401.12.0) for a full description. ([#5133](https://github.com/remix-run/remix/pull/5133))

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.12.0`

## 1.11.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.11.1`

## 1.11.0

### Patch Changes

- Introduces the `defer()` API from `@remix-run/router` with support for server-rendering and HTTP streaming. This utility allows you to defer values returned from `loader` functions by returning promises instead of resolved values. This has been refered to as _"sending a promise over the wire"_. ([#4920](https://github.com/remix-run/remix/pull/4920))

  Informational Resources:

  - <https://gist.github.com/jacob-ebey/9bde9546c1aafaa6bc8c242054b1be26>
  - <https://github.com/remix-run/remix/blob/main/decisions/0004-streaming-apis.md>

  Documentation Resources (better docs specific to Remix are in the works):

  - <https://reactrouter.com/en/main/utils/defer>
  - <https://reactrouter.com/en/main/components/await>
  - <https://reactrouter.com/en/main/hooks/use-async-value>
  - <https://reactrouter.com/en/main/hooks/use-async-error>

- Updated dependencies:
  - `@remix-run/express@1.11.0`

## 1.10.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.10.1`

## 1.10.0

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.10.0`

## 1.9.0

### Patch Changes

- Fix `TypedResponse` so that Typescript correctly shows errors for incompatible types in `loader` and `action` functions. ([#4734](https://github.com/remix-run/remix/pull/4734))
- Updated dependencies:
  - `@remix-run/express@1.9.0`

## 1.8.2

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.8.2`

## 1.8.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.8.1`

## 1.8.0

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.8.0`

## 1.7.6

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.6`

## 1.7.5

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.5`

## 1.7.4

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.4`

## 1.7.3

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.3`

## 1.7.2

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.2`

## 1.7.1

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.1`

## 1.7.0

### Minor Changes

- We've added a new type: `SerializeFrom`. This is used to infer the ([#4013](https://github.com/remix-run/remix/pull/4013))
  JSON-serialized return type of loaders and actions.
- `MetaFunction` type can now infer `data` and `parentsData` types from route loaders ([#4022](https://github.com/remix-run/remix/pull/4022))

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.7.0`

## 1.6.8

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.6.8`

## 1.6.7

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.6.7`

## 1.6.6

### Patch Changes

- Updated dependencies:
  - `@remix-run/express@1.6.6`

## 1.6.5

### Patch Changes

- Updated dependencies
  - `@remix-run/express@1.6.5`
