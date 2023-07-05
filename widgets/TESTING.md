#   Tutorial: Make a New VA.gov React Widget - Testing

## Write a Unit Test for the React Component

Make a directory for unit tests:

```sh
mkdir hello-world/tests
```

Create a test file `hello-world/tests/HelloWorldWidget.unit.spec.jsx` with the following contents:

```javascript
import React from 'react';
import { render } from '@testing-library/react';
import { HelloWorldWidget } from '../components/HelloWorldWidget';

describe('HelloWorldWidget', () => {
  it('renders "Hello World!"', () => {
    const { getByText } = render(<HelloWorldWidget />);

    getByText('Hello World!');
  });
});
```

Run the test:

```sh
yarn test:unit src/applications/static-pages/hello-world/tests/HellowWorldWidget.unit.spec.jsx
```

It should pass. Add more tests as you develop your widget.

## Write a Unit Test for the Widget's "create" Function

Create a test file `hello-world/tests/createHelloWorldWidget.unit.spec.js` with the following contents:

```javascript
import React from 'react';
import { render } from '@testing-library/react';
import { expect } from 'chai';
import { createHelloWorldWidget } from '../createHelloWorldWidget';
import widgetTypes from '../../widgetTypes';

describe('createHelloWorldWidget', () => {
  it('mounts the widget when the container is present', async () => {
    const { getByText } = render(
      <div data-widget-type={widgetTypes.HELLO_WORLD} />,
    );

    await createHelloWorldWidget();

    getByText('Hello World');
  });

  it('does not mount the widget when the container is not present', async () => {
    const { queryByText } = render(
      <div data-widget-type="unknown-widget-type" />
    );

    await createHelloWorldWidget();

    const widget = queryByText('Hello World');
    expect(widget).to.be.null;
  });
});
```

Run the test:

```sh
yarn test:unit src/applications/static-pages/hello-world/tests/createHelloWorldWidget.unit.spec.js
```

It should pass. These tests should be enough to cover your "create" function behavior.


##  Mount to an Existing Page

Running `vets-website` to interact with your widget is a great way to develop your widget in your development environment. However, for production, your widget should be mounted to an existing page.

1.  Find the Liquid template that is responsible for rendering the existing page.
1.  If there is no specific template for the page, you can assume there is a generic template rendering the page that already is setup to render widgets. In this case, you can add a widget to the existing page in Drupal or `vagov-content` with your widget's unique `widgetType` value.
1.  If there is a specific template for the page, add a `<div>` to the template with a `data-widget-type` attribute whose value is equal to your widget's unique `widgetType`.

##  Next Up: Final Steps

You're ready to mount your widget into a static content page.

[Continue to Testing](./FINISH.md)
