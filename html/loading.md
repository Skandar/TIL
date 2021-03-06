# Нативная “ленивая” загрузка `img` и `iframe`



В Chrome 75 (за флагом) появился HTML атрибут `loading`, который позволяет лениво загружать картинки и iframe. [Demo](https://mathiasbynens.be/demo/img-loading-lazy)



```js
if ('loading' in HTMLImageElement.prototype) { 
    // Браузер поддерживает атрибут "loading"
} else {
   // Использовать JS библиотеки для ленивой загрузки
}
```



## Возможные значения

- **`lazy`** - загружать “лениво“ (асинхронно).

- **`eager`** - загружает сразу (синхронно).

- **`auto`** - браузер сам решает как загрузить.

  

## Применение

- Любые фотографии и iframe’ы которые находятся за областью первого экрана.

- Слайдеры.

- Галереи

- Бесконечная прокрутка

  

## Ссылки

- [Native image lazy-loading for the web!](https://addyosmani.com/blog/lazy-loading/)