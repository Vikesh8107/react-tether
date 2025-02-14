# React Tether

![CI Status](https://github.com/danreeves/react-tether/actions/workflows/main.yml/badge.svg)
[![Sauce Test Status](https://app.saucelabs.com/buildstatus/react-tether)](https://app.saucelabs.com/u/react-tether)

> Cross-browser Testing Platform and Open Source <3 Provided by [Sauce Labs](https://saucelabs.com/).

---

React wrapper around [Tether](https://github.com/shipshapecode/tether), a positioning engine to make overlays, tooltips and dropdowns better

![React Tether](images/tether-header.png)

## Install

`npm install react-tether`

**As of version 2, a minimum of React 16.3 is required. If you need support for React < 16.3 please use the [1.x branch](https://github.com/danreeves/react-tether/tree/1.x).**

## Example Usage

```javascript
import TetherComponent from "react-tether";

class SimpleDemo extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isOpen: false,
    };
  }

  render() {
    const { isOpen } = this.state;

    return (
      <TetherComponent
        attachment="top center"
        constraints={[
          {
            to: "scrollParent",
            attachment: "together",
          },
        ]}
        /* renderTarget: This is what the item will be tethered to, make sure to attach the ref */
        renderTarget={(ref) => (
          <button
            ref={ref}
            onClick={() => {
              this.setState({ isOpen: !isOpen });
            }}
          >
            Toggle Tethered Content
          </button>
        )}
        /* renderElement: If present, this item will be tethered to the component returned by renderTarget */
        renderElement={(ref) =>
          isOpen && (
            <div ref={ref}>
              <h2>Tethered Content</h2>
              <p>A paragraph to accompany the title.</p>
            </div>
          )
        }
      />
    );
  }
}

```

## Props

#### `renderTarget`: PropTypes.func

This is a [render prop](https://reactjs.org/docs/render-props.html), the component returned from this function will be Tether's `target`. One argument, ref, is passed into this function. This is a ref that must be attached to the highest possible DOM node in the tree. If this is not done the element will not render.

#### `renderElement`: PropTypes.func

This is a [render prop](https://reactjs.org/docs/render-props.html), the component returned from this function will be Tether's `element`, that will be moved. If no component is returned, the target will still render, but with no element tethered. One argument, ref, is passed into this function. This is a ref that must be attached to the highest possible DOM node in the tree. If this is not done the element will not render.

#### `renderElementTag`: PropTypes.string

The tag that is used to render the Tether element, defaults to `div`.

#### `renderElementTo`: PropTypes.string

Where in the DOM the Tether element is appended. Passes in any valid selector to `document.querySelector`. Defaults to `document.body`.

Tether requires this element to be `position: static;`, otherwise it will default to `document.body`. See [this example](https://danreeves.github.io/react-tether/tests/renderelementto/) for more information.

#### `Tether Options`:

Any valid [Tether options](https://tetherjs.dev/#usage).

#### `children`:

Previous versions of react-tether used children to render the target and component, using children will now throw an error. Please use renderTarget and renderElement instead

## Imperative API

The following methods are exposed on the component instance:

- `getTetherInstance(): Tether`
- `disable(): void`
- `enable(): void`
- `on(event: string, handler: function, ctx: any): void`
- `once(event: string, handler: function, ctx: any): void`
- `off(event: string, handler: function): void`
- `position(): void`

#### Example usage:

```javascript
<TetherComponent
	ref={(tether) => (this.tether = tether)}
	renderTarget={(ref) => <Target ref={ref} />}
	renderElement={(ref) => (
		<Element ref={ref} onResize={() => this.tether && this.tether.position()} />
	)}
/>
```

## Run Example

clone repo

`git clone git@github.com:danreeves/react-tether.git`

move into folder

`cd ~/react-tether`

install dependencies

`npm install`

run dev mode

`npm run demo`

open your browser and visit: `http://localhost:1234/`
