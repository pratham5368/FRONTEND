
Next.js has built-in support for Sass using both the `.scss` and `.sass` extensions. You can use component-level Sass via CSS Modules and the `.module.scss`or `.module.sass` extension.

First, install [`sass`](https://github.com/sass/sass):

```bash filename="Terminal"
npm install --save-dev sass
```


### Customizing Sass Options

If you want to configure the Sass compiler, use `sassOptions` in `next.config.js`.

```js filename="next.config.js"
const path = require('path')

module.exports = {
  sassOptions: {
    includePaths: [path.join(__dirname, 'styles')],
  },
}
```

### Sass Variables

Next.js supports Sass variables exported from CSS Module files.

For example, using the exported `primaryColor` Sass variable:

```scss filename="app/variables.module.scss"
$primary-color: #64ff00;

:export {
  primaryColor: $primary-color;
}
```

<AppOnly>

```jsx filename="app/page.js"
// maps to root `/` URL

import variables from './variables.module.scss'

export default function Page() {
  return <h1 style={{ color: variables.primaryColor }}>Hello, Next.js!</h1>
}
```

</AppOnly>

<PagesOnly>

```jsx filename="pages/_app.js"
import variables from '../styles/variables.module.scss'

export default function MyApp({ Component, pageProps }) {
  return (
    <Layout color={variables.primaryColor}>
      <Component {...pageProps} />
    </Layout>
  )
}
```

</PagesOnly>