# Root

Every [Stylable stylesheet]() has a reserved class called `root` that is matches the root node of the component. 

You can apply default styling and behavior to the component on the root class itself.

## Examples

The `root` class is added automatically to root in [react integration](react-integration.md). No need to write `className="root"`.

**CSS API**
```css
@namespace "Comp";
.root { background: red; } /* set component background to red */
```

**CSS OUTPUT**
```css
.Comp__root { background: red; }
```

> **Note**:  
> Root can also define [states](./pseudo-classes) and [extend another component](./extend-stylesheet.md).
