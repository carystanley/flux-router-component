# flux-router-component [![Build Status](https://travis-ci.org/yahoo/flux-router-component.svg?branch=master)](https://travis-ci.org/yahoo/flux-router-component) [![Dependency Status](https://david-dm.org/yahoo/flux-router-component.svg)](https://david-dm.org/yahoo/flux-router-component)
This package provides navigational React components and router React mixin for applications built with [Flux](http://facebook.github.io/react/docs/flux-overview.html) architecture.  Please check out [examples](https://github.com/yahoo/flux-router-component/tree/master/examples) of how to use these components.

## NavLink
`NavLink` is the a React component for navigational links.  When the link is clicked, NavLink will dispatch `NAVIGATE` action to flux dispatcher.  The dispatcher can then dispatch the action to the stores that can handle it.

### Example Usage
```js
var NavLink = require('flux-router-component').NavLink;

var Nav = React.createClass({
    render: function () {
        var pages,
            links,
            dispatcher = this.props.dispatcher;  // this is the Flux dispatcher object
        pages = [
            {
                name: 'home',
                url: '/home',
                text: 'Home'
            },
            {
                name: 'about',
                url: '/about',
                text: 'About Us'
            }
        ];
        links = pages.map(function (page) {
            return (
                <li className="navItem">
                    <NavLink href={page.url} dispatcher={dispatcher}>
                        {page.text}
                    </NavLink>
                </li>
            );
        });
        return (
            <ul className="nav">
                {links}
            </ul>
        );

    }
});
```

## RouterMixin
`RouterMixin` is a React mixin to be used by appication's top level React component to:

* manage browser history when route changes, and
* dispatch `NAVIGATE` action via flux dispatcher on window `popstate` events


### Example Usage
```js
var RouterMixin = require('flux-router-component').RouterMixin;

var Application = React.createClass({
    mixins: [RouterMixin],
    ...
});
```

## Browser Support
This library supports browsers without native pushState, such as IE8 and IE9.  For these old browsers, hash will be updated with the new route path.  Here is an example:

User clicks on a link to navigate from the current route `http://mydomain.com/home`, to a new route `http://mydomain.com/path/to/new/route`:

* HTML5 browsers with pushState support will have the url updated to the new route;
* IE8 and IE9 will have a hash fragment added to the current route: `http://mydomain.com/home#/path/to/new/route`.

## Polyfills
`addEventListener` and `removeEventListener` polyfills are provided by:

* Compatibility code example on [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget.addEventListener)
* A few DOM polyfill libaries listed on [Modernizer Polyfill wiki page](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills#dom).

## License
This software is free to use under the Yahoo! Inc. BSD license.
See the [LICENSE file][] for license text and copyright information.

[LICENSE file]: https://github.com/yahoo/flux-router-component/blob/master/LICENSE.md

Third-pary open source code used are listed in our [package.json file]( https://github.com/yahoo/flux-router-component/blob/master/package.json).
