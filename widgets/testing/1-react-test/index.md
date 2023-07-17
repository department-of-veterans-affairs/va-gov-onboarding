---
previous: /widgets/testing
next: /widgets/testing/2-widget-test
---

# Write a Unit Test for the React Component

Make a directory for unit tests:

```sh
mkdir src/applications/static-pages/hello-world/tests
```

Create a test file for the React component:

```sh
touch src/applications/static-pages/hello-world/tests/HelloWorldWidget.unit.spec.jsx
```

Add the following contents to the file:

```jsx
import React from "react";
import { render } from "@testing-library/react";
import { HelloWorldWidget } from "../components/HelloWorldWidget";

describe("HelloWorldWidget", () => {
  it('renders "Hello World!"', () => {
    const { getByText } = render(<HelloWorldWidget />);

    getByText("Hello World!");
  });
});
```

Run the test:

```sh
yarn test:unit src/applications/static-pages/hello-world/tests/HelloWorldWidget.unit.spec.jsx
```

It should pass. Add more tests as you develop your widget.
