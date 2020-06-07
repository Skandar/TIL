# Композиция

Композиция - это механизм который позволяет не используя наследования переиспользовать код. Мы можем поместить внутри JSX тега, всё что хотим передать внутрь тега и оно будет доступно в `props.children`.

```js
function Wrapper(props) {
  return (
    <div className={'border-' + props.color}>
      {props.children}
    </div>
  );
}

function Component() {
  return (
    <Wrapper color="blue">
      <h1 className="text">
        Этот заголовок будет в props.children
      </h1>
    </Wrapper>
  );
}
```

Если необходимо иметь несколько мест для вставки, то можно использовать свои пропсы, а не `props.children`. Например:

```js
function Wrapper(props) {
  return (
    <div>
      <div className={'border-' + props.color}>
        {props.title}
      </div>
      <div className={'border-' + props.color}>
        {props.description}
      </div>
    </div>
  );
}

function Component() {
  return (
    <Wrapper color="blue"
      title={<h1>Заголовок</h1>}
      description={<p>Описание</p>}
    >
    </Wrapper>
  );
}
```

## Ссылки

- [React Documentation](https://ru.reactjs.org/docs/composition-vs-inheritance.html)
