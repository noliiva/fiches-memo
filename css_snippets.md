# CSS snippets

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
