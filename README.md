# A React-Static plugin that adds tailwind support

[![npm version](https://badge.fury.io/js/react-static-plugin-tailwindcss.svg)](https://badge.fury.io/js/react-static-plugin-tailwindcss)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Installation

In an existing react-static site run:

```bash
$ yarn add react-static-plugin-tailwindcss-purgecss -D
```

Then add the plugin to your static.config.js:

```js
export default {
  plugins: ["react-static-plugin-tailwindcss-purgecss"],
};
```

Now you can add @tailwind directives to your .css files

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### CSS-in-JS

If you're wanting to use tailwind in conjuction with styled-components for example

```bash
yarn add tailwind.macro@next
```

static.config.js

```js
export default {
  plugins: [
    [
      "react-static-plugin-tailwindcss",
      {
        cssInJs: true,
      },
    ],
  ],
};
```

Create a babel-plugin-macros.config.js file

```js
module.exports = {
  tailwind: {
    config: "./tailwind.config.js",
    format: "auto",
  },
};
```

Now you can use the tw macro inside styled components

```js
import tw from "tailwind.macro";
import styled from "styled-components";

export const Header = styled.h1`
  ${tw`text-4xl font-bold text-center text-blue-500`}
`;
```

### Autoprefixer

If you already handle auto prefixer or dont want to use it

```js
export default {
  plugins: [
    [
      "react-static-plugin-tailwindcss",
      {
        autoPrefixer: false,
      },
    ],
  ],
};
```

### PurgeCSS

If you want to remove unused Tailwind CSS, enable https://github.com/FullHuman/postcss-purgecss plugin

```js
export default {
  plugins: [
    [
      "react-static-plugin-tailwindcss",
      {
        purgeCss: true,
        purgeCssOptions: {
          content: ["**/*.tsx"],
          defaultExtractor: (content) => content.match(/[\w-/:]+(?<!:)/g) || [],
        },
      },
    ],
  ],
};
```

Create a purgecss.config.js file

```js
module.exports = {
  content: ["./**/*.html"],
  css: ["./src/app.css"],
};
```

- This is equivalent of setting `purgeCssOptions` in the example above.
- But due to [#296](https://github.com/FullHuman/purgecss/issues/296), it is not being loaded atm.
