# webpack-feature-flags-plugin

Webpack plugin for Feature Flags development.

### Usage

1. Add plugin in webpack config

```js

  plugins: [
    new FeatureFlagsWebpackPlugin([
      {
        value: 'FEATURE_1',
        component: 'Button',
      },
    ]),
  ],

```

2. Create a function that returns false by default

```ts
export function isFeatureEnabled(_feature: { value: string; component: string }): boolean {
  return false
}
```

3. Add new feature in your component. The plugin checking the call `isFeatureEnabled` function and replaces its call to `true` or `false`, depending on the flag passed to it

```tsx
import React from 'react';

export const Button = () => {
    if (isFeatureEnabled({ value: 'FEATURE_1', component: 'Button' })) {
        return <button>Button with new feature</button>
    }

    return <buttton>Regular button</button>
}
```