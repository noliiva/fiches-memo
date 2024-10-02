# CSS snippets

## Create new stacking context
```
isolation: isolate;
```

## Hide something while keeping it accessible

(source: https://www.scottohara.me/blog/2017/04/14/inclusively-hidden.html)
```
.hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  overflow: hidden;
  clip: rect( 0 0 0 0 );
  white-space: nowrap;
  clip-path: inset( 50% );
}
```

## Display full links in print stylesheets:

(source: https://css-tricks.com/css-content/)
```
@media print {
     a[href]:after { " (" attr(href) ") "; }
}
```

## Reverse text color based on background color:

(sources: https://css-tricks.com/reverse-text-color-mix-blend-mode/, https://css-tricks.com/methods-contrasting-text-backgrounds/)
```
<div><span>TEXT</span></div>
```
```
div {
  background: red;
}
span {
  mix-blend-mode: difference;
}
```
```
div {
  background: red;
  color: red;
}
span {
  filter: invert(1) grayscale(1) contrast(9);
}
```

## Align icon perfectly with text:

(sources: https://css-tricks.com/reverse-text-color-mix-blend-mode/, https://css-tricks.com/methods-contrasting-text-backgrounds/)
```
<p><span class="icon">@</span> Don't be square!</p>
```
```
.icon {
  display: inline-block;
  height: 1em;
  width: 1em;
  vertical-align: middle;
  margin-top: calc(1ex - 1cap);
  background: currentColor;
  color: white;
}
```
