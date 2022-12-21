

# Композиция <meta data-oversett="" data-original-text="Composition">

<p class="description">MUI старается сделать композицию как можно более простой.</p>

## Обертывание компонентов <meta data-oversett="" data-original-text="Wrapping components">

Чтобы обеспечить максимальную гибкость и производительность, MUI необходим способ узнать природу дочерних элементов, которые получает компонент. Чтобы решить эту проблему, мы помечаем некоторые компоненты статическим свойством `muiName`, когда это необходимо.

Однако вам может понадобиться обернуть компонент, чтобы улучшить его, что может противоречить решению `muiName`. Если вы оборачиваете компонент, проверьте, установлено ли у него это статическое свойство.

Если вы столкнулись с этой проблемой, вам необходимо использовать для вашего обернутого компонента тот же тег, что и для обернутого компонента. Кроме того, вам следует переслать реквизиты, поскольку родительскому компоненту может понадобиться управлять реквизитами обернутого компонента.

Рассмотрим пример:

```jsx
const WrappedIcon = (props) => <Icon {...props} />;
WrappedIcon.muiName = Icon.muiName;
```

{{"demo": "Composition.js"}}

## Реквизит компонента <meta data-oversett="" data-original-text="Component prop">

MUI позволяет вам изменить корневой элемент, который будет отображаться, с помощью реквизита `component`.

### Как это работает? <meta data-oversett="" data-original-text="How does it work?">

Пользовательский компонент будет отображаться MUI следующим образом:

```js
return React.createElement(props.component, props);
```

Например, по умолчанию компонент `List` будет отображать элемент `<ul>`. Это можно изменить, передав [компонент React](https://reactjs.org/docs/components-and-props.html#function-and-class-components) в свойство `component`. В следующем примере компонент `List` будет отображаться с элементом `<nav>` в качестве корневого элемента:

```jsx
<List component="nav">
  <ListItem button>
    <ListItemText primary="Trash" />
  </ListItem>
  <ListItem button>
    <ListItemText primary="Spam" />
  </ListItem>
</List>
```

Этот паттерн очень мощный и позволяет добиться большой гибкости, а также взаимодействовать с другими библиотеками, такими как ваша любимая библиотека маршрутизации или форм. Но он также **поставляется с небольшим предостережением!**

### Инлайнинг и предостережение <meta data-oversett="" data-original-text="Inlining &amp; caveat">

Использование инлайн-функции в качестве аргумента для реквизита `component` может привести к **неожиданному размонтированию**, поскольку при каждом рендеринге React передается новый компонент. Например, если вы хотите создать пользовательскую `ListItem`, которая действует как ссылка, вы можете сделать следующее:

```jsx
import { Link } from 'react-router-dom';

function ListItemLink(props) {
  const { icon, primary, to } = props;

  const CustomLink = (props) => <Link to={to} {...props} />;

  return (
    <li>
      <ListItem button component={CustomLink}>
        <ListItemIcon>{icon}</ListItemIcon>
        <ListItemText primary={primary} />
      </ListItem>
    </li>
  );
}
```

:::warning
⚠️ Однако, поскольку мы используем встроенную функцию для изменения рендеринга компонента, React будет перемонтировать ссылку каждый раз при рендеринге `ListItemLink`. React не только излишне обновит DOM, но и потеряет состояние, например, эффект пульсации `ListItem` также не будет работать корректно.
:::

Решение простое: **избегайте инлайн-функций и передавайте статический компонент в проп `component`** . Давайте изменим компонент `ListItemLink` так, чтобы `CustomLink` всегда ссылался на один и тот же компонент:

```tsx
import { Link, LinkProps } from 'react-router-dom';

function ListItemLink(props) {
  const { icon, primary, to } = props;

  const CustomLink = React.useMemo(
    () =>
      React.forwardRef<HTMLAnchorElement, Omit<RouterLinkProps, 'to'>>(function Link(
        linkProps,
        ref,
      ) {
        return <Link ref={ref} to={to} {...linkProps} />;
      }),
    [to],
  );

  return (
    <li>
      <ListItem button component={CustomLink}>
        <ListItemIcon>{icon}</ListItemIcon>
        <ListItemText primary={primary} />
      </ListItem>
    </li>
  );
}
```

### Переадресация реквизита и предостережение <meta data-oversett="" data-original-text="Prop forwarding &amp; caveat">

Вы можете воспользоваться преимуществами переадресации реквизита для упрощения кода. В этом примере мы не создаем никакого промежуточного компонента:

```jsx
import { Link } from 'react-router-dom';

<ListItem button component={Link} to="/">
```

:::warning
⚠️ Однако эта стратегия страдает от ограничения: коллизии имен реквизитов. Компонент, получающий реквизит `component` (например, ListItem), может перехватить реквизит (например, to), предназначенный для покидающего элемента (например, Link).
:::

### С TypeScript <meta data-oversett="" data-original-text="With TypeScript">

Чтобы иметь возможность использовать реквизит `component`, тип реквизита должен использоваться с аргументами типа. В противном случае реквизит `component` не будет присутствовать.

В примерах ниже используется `TypographyProps`, но то же самое будет работать для любого компонента, у которого реквизит определен с помощью `OverrideProps`.

```ts
import { TypographyProps } from '@mui/material/Typography';

function CustomComponent(props: TypographyProps<'a', { component: 'a' }>) {
  /* ... */
}
// ...
<CustomComponent component="a" />;
```

Теперь `CustomComponent` можно использовать с реквизитом `component`, который должен быть установлен в `'a'`. Кроме того, `CustomComponent` будет иметь все реквизиты HTML-элемента `<a>`. Остальные реквизиты компонента `Typography` также будут присутствовать в реквизитах `CustomComponent`.

Пример кода с Button и react-router-dom вы можете найти в [этих демонстрациях](/material-ui/guides/routing/#component-prop).

#### Generic <meta data-oversett="" data-original-text="Generic">

Также можно иметь общий `CustomComponent`, который будет принимать любой компонент React и элементы HTML.

```ts
function GenericCustomComponent<C extends React.ElementType>(
  props: TypographyProps<C, { component?: C }>,
) {
  /* ... */
}
```

Если `GenericCustomComponent` используется с предоставленным реквизитом `component`, он также должен иметь все реквизиты, требуемые предоставленным компонентом.

```ts
function ThirdPartyComponent({ prop1 }: { prop1: string }) {
  /* ... */
}
// ...
<GenericCustomComponent component={ThirdPartyComponent} prop1="some value" />;
```

Реквизит `prop1` стал необходимым для `GenericCustomComponent`, так как `ThirdPartyComponent` имеет его в качестве требования.

Не каждый компонент полностью поддерживает любой тип компонента, который вы передаете. Если вы столкнулись с компонентом, который отвергает свой реквизит `component` в TypeScript, пожалуйста, откройте проблему. В настоящее время ведется работа по исправлению этого, делая реквизиты компонентов общими.

## Предостережения при использовании ссылок <meta data-oversett="" data-original-text="Caveat with refs">

В этом разделе рассматриваются предостережения при использовании пользовательского компонента в качестве `children` или для реквизита`component`.

Некоторым компонентам необходим доступ к узлу DOM. Ранее это было возможно с помощью `ReactDOM.findDOMNode`. Эта функция устарела в пользу `ref` и переадресации ссылок. Тем не менее, только следующие типы компонентов могут получить `ref`:

-   любой компонент MUI
-   компоненты класса, т.е. `React.Component` или `React.PureComponent`
-   компоненты DOM (или хоста), например, `div` или `button`
-   [Компоненты React.forwardRef](https://reactjs.org/docs/react-api.html#reactforwardref)
-   [компоненты React.lazy](https://reactjs.org/docs/react-api.html#reactlazy)
-   [компоненты React.memo](https://reactjs.org/docs/react-api.html#reactmemo)

Если вы не используете один из вышеперечисленных типов при использовании ваших компонентов в сочетании с MUI, вы можете увидеть предупреждение от React в вашей консоли, похожее на:

:::warning
Компонентам функций нельзя давать ссылки. Попытки получить доступ к этой ссылке будут безуспешными. Вы хотели использовать React.forwardRef()?
:::

Обратите внимание, что вы все равно получите это предупреждение для компонентов `lazy` и `memo`, если их обернутый компонент не может содержать ссылку. В некоторых случаях для помощи в отладке выдается дополнительное предупреждение, подобное следующему:

:::warning
Invalid prop `component` supplied to `ComponentName`. Expected an element type that can hold a ref.
:::

Здесь рассматриваются только два наиболее распространенных случая использования. Для получения дополнительной информации смотрите [этот раздел в официальной документации React](https://reactjs.org/docs/forwarding-refs.html).

```diff
-const MyButton = () => <div role="button" />;
+const MyButton = React.forwardRef((props, ref) =>
+  <div role="button" {...props} ref={ref} />);

 <Button component={MyButton} />;
```

```diff
-const SomeContent = props => <div {...props}>Hello, World!</div>;
+const SomeContent = React.forwardRef((props, ref) =>
+  <div {...props} ref={ref}>Hello, World!</div>);

 <Tooltip title="Hello again."><SomeContent /></Tooltip>;
```

Чтобы узнать, имеет ли используемый вами компонент MUI такое требование, ознакомьтесь с документацией props API для этого компонента. Если вам нужно переслать ссылки, описание будет ссылаться на этот раздел.

### Предостережение при использовании StrictMode <meta data-oversett="" data-original-text="Caveat with StrictMode">

Если вы используете компоненты классов для случаев, описанных выше, вы все еще будете видеть предупреждения в `React.StrictMode`.`ReactDOM.findDOMNode` используется внутри для обратной совместимости. Вы можете использовать `React.forwardRef` и указанный prop в компоненте класса для пересылки `ref` в DOM-компонент. Это не должно больше вызывать предупреждений, связанных с устареванием `ReactDOM.findDOMNode`.

```diff
 class Component extends React.Component {
   render() {
-    const { props } = this;
+    const { forwardedRef, ...props } = this.props;
     return <div {...props} ref={forwardedRef} />;
   }
 }

-export default Component;
+export default React.forwardRef((props, ref) => <Component {...props} forwardedRef={ref} />);
```
