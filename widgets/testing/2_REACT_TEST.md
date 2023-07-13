---
permalink: /widgets/testing/react-test
---

## Write a Unit Test for the React Component

Make a directory for unit tests:

```sh
mkdir hello-world/tests
```

Create a test file `hello-world/tests/HelloWorldWidget.unit.spec.jsx` with the following contents:

```javascript
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
yarn test:unit src/applications/static-pages/hello-world/tests/HellowWorldWidget.unit.spec.jsx
```

It should pass. Add more tests as you develop your widget.

[Continue](./3_WIDGET_TEST.md)

[Back](./1_START.md)
