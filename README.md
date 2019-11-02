# postcss-ts-classnames

[PostCSS][] plugin to generate TypeScript types from **your** CSS class names.

[postcss]: https://postcss.org/

It generates a global `ClassNames` type which is a union of all classes
used in your project whether written by you or from a framework such as
Bootstrap or Tailwind.

Ex. for css

```css
.button {
    background: green;
}

.button-danger {
    background: red;
}
```

you'll get

```ts
type ClassNames = "button" | "button-danger";
```

With it you can create a helper function like

```ts
function cn(...args: ClassNames[]) {
    return args.join(" ");
}
```

and have your editor autocomplete and validate the class names:

> TODO add gifs

## ts-classnames

There's also a `ts-classnames` module which is re-exported version of the
original [classnames][] which uses the generated `ClassNames` type to
validate the class names

[classnames]: https://www.npmjs.com/package/classnames

Install

    npm install ts-classname

Import

```ts
import { cn } from "ts-classnames";
```

## Setup

Install the plugin

    npm install postcss-ts-classnames

In your PostCSS config add it close to the end before optimizing plugins such
as cssnano or purgecss:

```js
module.exports = {
    plugins: [
        require("postcss-import"),
        require("tailwindcss"),

        require("postcss-ts-classnames")({
            dest: "src/classnames.d.ts",
        }),

        require("@fullhuman/postcss-purgecss")({
            content: ["./src/**/*.html"],
        }),
    ],
};
```
