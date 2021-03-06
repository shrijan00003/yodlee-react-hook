yodlee-react-hook
=================

[Yodlee](https://www.yodlee.com/) [FastLink 3.0](https://developer.yodlee.com/docs/fastlink/3.0/product-guide) React hook.

This tiny library helps you to use Yodlee FastLink v3.0 in your React projects.

Installation
============

```bash
# with npm
npm install yodlee-react-hook
# with yarn
yarn add yodlee-react-hook
```

Usage
=====

Generate `accessToken` or `jwtToken` with your `clientId`, `secret` and `userName` on your backend and pass it down to your client below to open iframe. 

```jsx
import { useYodlee } from 'yodlee-react-hook';

const MyComponent = () => {
  const { ready, init } = useYodlee({
    containerId: 'container-fastlink',
    fastLinkOptions: {
      fastLinkURL: 'https://node.sandbox.yodlee.com/authenticate/restserver',
      token: {
        tokenType: 'AccessToken',
        tokenValue: 'foo'
      }
    }
  });

  return (
    <div className="container">
      <div id="container-fastlink"></div>
      { ready ? <button onClick={() => init()}>Open Yodlee</button> : 'Loading...' }
    </div>
  );
}
```

Test
====

```bash
# with npm
npm run test
# with yarn
yarn test
```

Details
=======

### `useYodlee` hook arguments:

- containerId (`string`): Id for DOM Element to load iframe into.
- createScriptTag (`boolean`, default = true): If you set this to false then hook will not add script element to component. It's suitable for react apps having script element already added to the page e.g. `<script defer async src="https://cdn.yodlee.com/fastlink/v3/initialize.js"></script>`. If you receive [cross-origin error from React](https://reactjs.org/docs/cross-origin-errors.html) then this would be the preferred solution for you.
- fastLinkOptions (`FastLinkOptionsType`) 
  - fastLinkURL (`string`): FastLink URL to be used. Please see URLs below from Yodlee codepen solution.
    - USA: https://node.sandbox.yodlee.com/authenticate/restserver
    - UK: https://node.sandbox.yodlee.uk/authenticate/uksandbox
    - ANZ: https://sandbox-node.yodlee.com.au/authenticate/anzdevexsandbox
  - token: (`TokenType`): 
    - tokenType: (`'AccessToken' | 'JwtToken'`): Your token type
    - tokenValue: (`string`): Your token value
  - userExperienceFlow (`UserExperienceFlowType`, default = Verification):
    - Verification: Aggregate account profile information required to perform user profile verification.
    - Aggregation: Aggregate account summary-level information and transactions.
    - Aggregation plus Verification: Aggregate account summary-level information and transactions, along with account profile information.
-  onSuccess, onError, onExit, onEvent: Additional callback functions if you would like to add customer implementation.

Please consult to Yodlee fastlink.open() [instructions](https://developer.yodlee.com/docs/fastlink/3.0/getting-started) for details.

### `useYodlee` hook return values:

- init (method): Method to initiate FastLink which creates an iframe
- ready (boolean): Yodlee FastLink library is loaded or not
- active (boolean): Init method called or not 
- data (any): Customer data received from onSuccess event
- error (any): This is the error if Yodlee FastLink intercepts with any error

You can find typescript definitions in `index.d.ts` file.
