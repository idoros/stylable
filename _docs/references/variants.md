
# Variants

A variant is a mixin described as part of a Stylable stylesheet that can be later applied on a CSS ruleset.

A single component might offer multiple style variants for different themes or semantics.

## Define a variant

> *Note*: Variants can be defined only for a [class selector](./class-selectors.md).

CSS API :
```css
/* theme.css */
:import {
    -st-from: "./button.css";
    -st-default: Button;
}
.SaleBtn {
    -st-extends: Button;
    -st-variant: true;
    color: red;
}
.SaleBtn:hover {
    color: pink;
}
```

`-st-variant: true;` tells the Stylable pre-processor that if the variant SaleBtn isn't used anywhere in the project it can ignore it during the build stage, resulting in a smaller end-CSS without redundant rules.


## Define inline variants

It's handy when authoring a component to keep all its styles, and any variants you offer to consumers of your component, in one file.

For example, consider the following button, and its variant, BigButton

```css
.root {
    color:red;
    background-color:blue;
    height:2em;
}

.BigButton {
    -st-variant: true;
    height:5em;
}
```

> *Notice:* variants without an [extends directive rule](./extend-stylesheet.md) are automatically variants of the owner stylesheet.


## Use variants

CSS API:
```css
/* page.css */
:import {
    -st-from: "./theme.css";
    -st-names: SaleBtn;
}

.sale-button {
    -st-mixin: SaleBtn;
}
```

CSS OUTPUT:
```css
/* namespaced to page */
.root .sale-button {
    color: red;
}
.root .sale-button:hover {
    color: pink;
}
```

## Use variants with extends 

When using variant with `-st-extends` the class also inherits the variant type.

CSS API:
```css
/* page.css */
:import {
    -st-from: "./theme.css";
    -st-names: SaleBtn;
}

.sale-button {
    -st-extends: SaleBtn;
}

.sale-button::icon {
    border: 2px solid green;
}
```

CSS OUTPUT:
```css
/* namespaced to page */
.root .sale-button {
    color: red;
}
.root .sale-button:hover {
    color: pink;
}
.root .sale-button .button-icon {
    border: 2px solid green;
}
```