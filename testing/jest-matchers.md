# Jest matchers

Для проверки значений в Jest есть специальные методы.

## Сравнение эквивалентности

- `toBe` - применяется для сравнения эквивалентности примитивов. `toBe` для сравнения использует `Object.is`.
- `toEqual` - применяется для сравнения эквивалентности объектов. `toEqual` рекурсивно сравнивает поля объектов.

  ```js
  test('2 + 2 = 4', () => {
    expect(2 + 2).toBe(4);
  });

  test('добавление нового поля в объект', () => {
    const data = {one: 1};
    data['two'] = 2;
    expect(data).toEqual({one: 1, two: 2});
  });
  ```

## Проверка на истинность

Методы для проверки истинности:

- `toBeNull` - проверяет на `null`.
- `toBeUndefined` - проверяет на `undefined`.
- `toBeDefined` - противоположно `toBeUndefined`.
- `toBeTruthy` - проверяет является ли значение `true`.
- `toBeFalsy` - проверяет является ли значение `false`.

Так же если необходимо противоположное значение, можно вызвать функцию у поля `not`.

```js
test('null', () => {
  const n = null;
  expect(n).toBeNull();
  expect(n).toBeDefined();
  expect(n).not.toBeUndefined();
  expect(n).not.toBeTruthy();
  expect(n).toBeFalsy();
});
```

```js
test('ноль', () => {
  const z = 0;
  expect(z).not.toBeNull();
  expect(z).toBeDefined();
  expect(z).not.toBeUndefined();
  expect(z).not.toBeTruthy();
  expect(z).toBeFalsy();
});
```

## Проверка чисел

Методы для проверки чисел:

- `toBeGreaterThan` - эквивалентно `>`.
- `toBeGreaterThanOrEqual` - эквивалентно `>=`.
- `toBeLessThan` - эквивалентно `<`.
- `toBeLessThanOrEqual` - эквивалентно `<=`.

```js
test('2 + 2', () => {
  const value = 2 + 2;
  expect(value).toBeGreaterThan(3);
  expect(value).toBeGreaterThanOrEqual(3.5);
  expect(value).toBeLessThan(5);
  expect(value).toBeLessThanOrEqual(4.5);

  // toBe и toEqual работают одинаково для чисел
  expect(value).toBe(4);
  expect(value).toEqual(4);
});
```

Для проверки чисел с плавающей запятой  вместо `toEqual`/`toBe` нужно использовать `toBeCloseTo`.

```js
test('сложение чисел с плавающей запятой', () => {
  const value = 0.1 + 0.2;
  //expect(value).toBe(0.3);         Это не работает из-за погрешности округления
  expect(value).toBeCloseTo(0.3); // Это работает.
});
```

## Проверка строк

Строки можно проверить по регулярному выражению используя метод `toMatch`.

```js
test('there is no I in team', () => {
  expect('team').not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
  expect('Christoph').toMatch(/stop/);
});
```

## Проверка массивов и итерируемых значений

Массивы и итерируемые значения можно проверить по регулярному выражению используя метод `toContain`.

```js
const shoppingList = [
  'diapers',
  'kleenex',
  'trash bags',
  'paper towels',
  'beer',
];

test('beer есть в shoppingList', () => {
  expect(shoppingList).toContain('beer');
  expect(new Set(shoppingList)).toContain('beer');
});
```

## Проверка исключения

Функции можно проверить на исключения используя метод `toThrow`.

```js
function compileAndroidCode() {
  throw new Error('you are using the wrong JDK');
}

test('При компиляции андроида генерируется ошибка', () => {
  expect(compileAndroidCode).toThrow();
  expect(compileAndroidCode).toThrow(Error);

  // You can also use the exact error message or a regexp
  expect(compileAndroidCode).toThrow('you are using the wrong JDK');
  expect(compileAndroidCode).toThrow(/JDK/);
});
```

## Ссылки

- [Jest Docs. Using Matchers](https://jestjs.io/docs/en/using-matchers)
