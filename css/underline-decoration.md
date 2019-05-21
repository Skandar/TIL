# Underline decoration

Простое и красивое подчёркивание текста. [Demo](https://codepen.io/skandar_sl/pen/qGPXBm)

```css
a {
  text-decoration: none;

  background-image: linear-gradient(#fed800, #fed800);
  background-size: 100% 8px;
  background-repeat: no-repeat;
  background-position: left 0 bottom 4px;
  transition: background-size 250ms ease-in-out;

  /* For multiline text */
  box-decoration-break: clone;
  -webkit-box-decoration-break: clone;
  outline: none;
}
```
