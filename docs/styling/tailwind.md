---
title: Tailwind
---

# Tailwind

Perhaps the most popular way to style a Remix application in the community is to use [Tailwind CSS][tailwind].

Remix supports tailwind automatically if `tailwind.config.js` is present in the root of your project. You can disable it in [Remix Config][remix-config]

Tailwind has the benefits of inline-style co-location for developer ergonomics and is able to generate a CSS file for Remix to import. The generated CSS file generally caps out to a reasonable size, even for large applications. Load that file into the `root.tsx` links and be done with it.

If you don't have any CSS opinions, this is a great approach.

To use Tailwind, first install it as a dev dependency:

```sh
npm install -D tailwindcss
```

Then initialize a config file:

```sh
npx tailwindcss init --ts
```

Now we can tell it which files to generate classes from:

```ts filename=tailwind.config.ts lines=[4]
import type { Config } from "tailwindcss";

export default {
  content: ["./app/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
} satisfies Config;
```

Then include the `@tailwind` directives in your CSS. For example, you could create a `tailwind.css` file at the root of your app:

```css filename=app/tailwind.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Then add `tailwind.css` to your root route's `links` function:

```tsx filename=app/root.tsx
import type { LinksFunction } from "@remix-run/node"; // or cloudflare/deno

// ...

import styles from "./tailwind.css";

export const links: LinksFunction = () => [
  { rel: "stylesheet", href: styles },
];
```

With this setup in place, you can also use [Tailwind's functions and directives][tailwind-functions-and-directives] anywhere in your CSS. Note that Tailwind will warn that no utility classes were detected in your source files if you never used it before.

Tailwind doesn't compile CSS for older browsers by default, so if you'd like to achieve this using a PostCSS-based tool like \[Autoprefixer]\[autoprefixer], you'll need to leverage Remix's [built-in PostCSS support][built-in-post-css-support]. When using both PostCSS and Tailwind, the Tailwind plugin will be automatically included if it's missing, but you can also choose to manually include the Tailwind plugin in your PostCSS config instead if you prefer.

If you're using VS Code, it's recommended you install the [Tailwind IntelliSense extension][tailwind-intelli-sense-extension] for the best developer experience.

## Avoiding Tailwind's `@import` syntax

It's recommended that you avoid Tailwind's `@import` syntax (e.g. `@import 'tailwindcss/base'`) in favor of Tailwind directives (e.g. `@tailwind base`).

Tailwind replaces its import statements with inlined CSS but this can result in the interleaving of styles and import statements. This clashes with the restriction that all import statements must be at the start of the file.

Alternatively, you can use [PostCSS][built-in-post-css-support] with the [postcss-import] plugin to process imports before passing them to esbuild.

[tailwind]: https://tailwindcss.com
[tailwind-functions-and-directives]: https://tailwindcss.com/docs/functions-and-directives
[tailwind-intelli-sense-extension]: https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss
[built-in-post-css-support]: ./postcss
[postcss-import]: https://github.com/postcss/postcss-import
[remix-config]: ../file-conventions/remix-config#tailwind
