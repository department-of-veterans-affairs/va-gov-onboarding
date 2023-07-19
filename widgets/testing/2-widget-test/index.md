---
previous: /widgets/testing/1-react-test
---

# Write a Unit Test for the Widget's "Create" Function

Create a test file for the "create" function:

```sh
touch src/applications/static-pages/hello-world/tests/createHelloWorldWidget.unit.spec.js
```

Add the following contents to the file:

```jsx
import React from "react";
import { render } from "@testing-library/react";
import { expect } from "chai";
import { createHelloWorldWidget } from "../createHelloWorldWidget";
import widgetTypes from "../../widgetTypes";

describe("createHelloWorldWidget", () => {
  it("mounts the widget when the container is present", async () => {
    const { getByText } = render(
      <div data-widget-type={widgetTypes.HELLO_WORLD} />
    );

    await createHelloWorldWidget();

    getByText("Hello World!");
  });

  it("does not mount the widget when the container is not present", async () => {
    const { queryByText } = render(
      <div data-widget-type="unknown-widget-type" />
    );

    await createHelloWorldWidget();

    const widget = queryByText("Hello World");
    expect(widget).to.be.null;
  });
});
```

The above code are two unit tests. The first unit test will:
1. Render the widget by its data-widget-type that we previously defined in widgetTypes
2. Check to see if "Hello World!" appears in the application

The second unit test will:
1. Render the widget by its data-widget-type of "unknown-widget-type"
2. Check to see that nothing appears in the application

Run the test:

```sh
yarn test:unit src/applications/static-pages/hello-world/tests/createHelloWorldWidget.unit.spec.js
```

They should pass. These tests should be enough to cover your "create" function behavior.

## You Made It!

Thanks for following along with this tutorial. You now have a basic understanding of how to create a VA.gov React widget.
