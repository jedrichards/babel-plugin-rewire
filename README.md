# babel-plugin-rewire

A Babel plugin that adds the ability to rewire modul dependency.

[![Build Status](https://travis-ci.org/speedskater/babel-plugin-rewire.svg)](https://travis-ci.org/speedskater/babel-plugin-rewire)
 
It is inspired by [rewire.js](https://github.com/jhnns/rewire) and transfers its concepts to es6 using babel.

It is for writing tests, specifically to mock the dependencies of the module under test.

Therfore for each module it adds and exports the methods __GetDependency__, __Rewire__, and __ResetDependency__.
These methods allow to rewire the module under test. Furthermore in case of a default Export these methods are assigned to the existing default export.

e.g. Testing a React Component

## Module to test (e.g. a React Component) 

```javascript
import ChildComponent from 'child-component-module';
 
export default class MyFancyWrapperComponent extends React.Component {

	render() {
		return (<div className="wrapper-style">
			<ChildComponent {...this.props} />
		</div>);
	}
}
```

## TestCode

```javascript
import ComponentToTest from 'my-fancy-wrapper-component-module';

ComponentToTest.__Rewire__('ChildComponent', React.createClass({
    render: function() { return <div {...this.props}></div>; }
}));
....

ComponentToTest.__ResetDependency__('ChildComponent');
```

# Install

```
$ npm install babel babel-plugin-rewire
```

# Use

```
$ babel --plugins rewire
```

or:

```javascript
require("babel").transform("code", { plugins: ["rewire"] });
```

with `webpack` use the following loader:

```javascript
{test: /src\/js\/.+\.js$/, loader: 'babel-loader?plugins=rewire' }
```

## Release History

* 0.1.0 Initial release
* 0.1.1 Bugfix: moved to peer dependencies

# License

The ISC License (ISC)

Copyright (c) 2015, Robert Binna <r.binna@synedra.com>

Permission to use, copy, modify, and/or distribute this software for any
	purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

	THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
