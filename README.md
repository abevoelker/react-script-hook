# react-script-hook

> React hook to dynamically load an external script and know when its loaded

## Install

```sh
// with npm
npm install react-script-hook

// with yarn
yarn add react-script-hook
```

## How to use

```javascript
import React from 'react';
import { StripeProvider } from 'react-stripe-elements';
import useScript from 'react-script-hook';

import MyCheckout from './my-checkout';

function App() {
    const [loading, error] = useScript({ src: 'https://js.stripe.com/v3/' });

    if (loading) return <h3>Loading Stripe API...</h3>;
    if (error) return <h3>Failed to load Stripe API: {error.message}</h3>;

    return (
        <StripeProvider apiKey="pk_test_6pRNASCoBOKtIshFeQd4XMUh">
            <MyCheckout />
        </StripeProvider>
    );
}

export default App;
```

## Use with callbacks

```js
useScript({
    src: 'https://js.stripe.com/v3/',
    onload: () => console.log('Script loaded!'),
});
```

## Check for Existing

If you're in an environment where the script may have already been loaded, pass
the `checkForExisting` flag to ensure the script is only placed on the page
once by querying for script tags with the same src. Useful for SSR or SPAs with
client-side routing.

```js
const [loading, error] = useScript({
    src: 'https://js.stripe.com/v3/',
    checkForExisting: true,
});
```

## Conditionally calling a script

If you want to conditionally call a script you can do so by setting the src value to either the script or null. Note that the script is not removed if the src is set to null after it was previously set to a value causing the script to be appended.

```js
const [loading, error] = useScript({
    /** Only append stripeJS script when shouldLoadStripe is true */
    src: shouldLoadStripe ? 'https://js.stripe.com/v3/' : null,
});
```

## License

[MIT](LICENSE)
