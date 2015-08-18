# `<FontAwesome/>`
A pure Javascript, CSS-free implementation of [Font Awesome](http://fontawesome.io) using [React](http://facebook.github.io/react/) and [Radium](https://github.com/FormidableLabs/radium).

## Usage
```sh
npm install @grove/react-font-awesome --save 
```
The published package contains Babel-transpiled code in `lib/` and has peer dependencies of `react`, `radium`, and `babel-runtime`. You'll need to depend on those yourself and `npm install` them.

```js
// Button.jsx
import React, { PropTypes } from 'react';
import radium from 'radium';
import Icon from 'react-font-awesome';

// Some styling for the button
const button = {
  backgroundColor: 'green',
  color: 'white',
  padding: '5px 10px',
  fontSize: 20,
};

// Optional styling to the icon
const icon = {
  transition: 'transform 200ms',
  transform: 'rotateY(180deg)',
  // radium provides hover states and vendor prefixes
  ':hover': {
    transform: 'rotateY(180deg) scale(1.5)'
  },
};

const Button = React.createClass({
  propTypes: {
    style: PropTypes.object,
    iconStyle: PropTypes.object,
  },
  
  render() {
    const { style, iconStyle } = this.props;
    return (
      <button style={[button, style]}>
        Click me!
        <Icon name='pied-piper' style={[icon, iconStyle]} />
      </button>
    );
  }
});

export default radium(Button);
```

## Prior Art
* [react-fontawesome](https://github.com/builtbybig/react-fontawesome)
* [react-fa](https://github.com/andreypopp/react-fa)
* [react-font-awesome](https://github.com/Laiff/react-font-awesome)

Each of the previous libraries implements the icon set using CSS classes and pseudo `:before` elements with the Font Awesome stylesheet. Some of them also require you to setup a bundler like Webpack in order to bring in the CSS. This package was created to avoid both of those hassles.

On the first mount of a `FontAwesome` component, the `@font-face` rule is appended to the `<head>` as a `<style>` element. The font files are loaded from the Bootstrap CDN. No `:before` elements are needed — the icon is a span with the actual unicode character as the content and inline styling to set the font family.

The rest of the Font Awesome API (larger sizes, stack, flip, 2x, etc.) was specifically not implemented. This is because those are shorthands for styling, which you can set yourself with the `style` prop.

## Contributions
Pull requests welcome! Especially tests :smile: