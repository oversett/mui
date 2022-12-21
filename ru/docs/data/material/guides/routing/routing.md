

# Библиотеки маршрутизации <meta data-oversett="" data-original-text="Routing libraries">

<p class="description">По умолчанию навигация осуществляется с помощью собственного элемента <code>&lt;a&gt;</code>. Вы можете настроить его так, чтобы использовать свой собственный маршрутизатор. Например, используя Link от Next.js или react-router.</p>

## Компоненты навигации <meta data-oversett="" data-original-text="Navigation components">

Есть два основных компонента для выполнения навигации. Наиболее распространенным является компонент [`Link`](/material-ui/react-link/) Он отображает родной элемент `<a>` и применяет `href` в качестве атрибута.

{{"demo": "LinkDemo.js"}}

Вы также можете сделать кнопку выполняющей навигационные действия. Если ваш компонент расширяемый [`ButtonBase`](/material-ui/api/button-base/)то предоставление реквизита `href` включает режим ссылки. Например, с компонентом `Button`:

{{"demo": "ButtonDemo.js"}}

## Глобальная тема Link <meta data-oversett="" data-original-text="Global theme Link">

В реальных приложениях использования родного элемента `<a>` редко бывает достаточно. Вы можете улучшить пользовательский опыт, систематически используя улучшенный компонент Link. Тема MUI позволяет настроить этот компонент один раз. Например, с помощью react-router:

```tsx
import { Link as RouterLink, LinkProps as RouterLinkProps } from 'react-router-dom';
import { LinkProps } from '@mui/material/Link';

const LinkBehavior = React.forwardRef<
  HTMLAnchorElement,
  Omit<RouterLinkProps, 'to'> & { href: RouterLinkProps['to'] }
>((props, ref) => {
  const { href, ...other } = props;
  // Map href (MUI) -> to (react-router)
  return <RouterLink ref={ref} to={href} {...other} />;
});

const theme = createTheme({
  components: {
    MuiLink: {
      defaultProps: {
        component: LinkBehavior,
      } as LinkProps,
    },
    MuiButtonBase: {
      defaultProps: {
        LinkComponent: LinkBehavior,
      },
    },
  },
});
```

{{"demo": "LinkRouterWithTheme.js", "defaultCodeOpen": false}}

:::warning
Этот подход имеет ограничения при использовании TypeScript. Реквизит `href` принимает только строку. Если вам нужно предоставить более богатую структуру, см. следующий раздел.
:::

## `component` prop <meta data-oversett="" data-original-text="component prop">

Интеграцию со сторонними библиотеками маршрутизации можно обеспечить с помощью реквизита `component`. Подробнее об этом реквизите можно узнать в [**руководстве по композиции**](/material-ui/guides/composition/#component-prop).

### Ссылка <meta data-oversett="" data-original-text="Link">

Вот несколько демонстраций с [react-router](https://github.com/remix-run/react-router). Вы можете применять одну и ту же стратегию со всеми компонентами: BottomNavigation, Card и т.д.

{{"demo": "LinkRouter.js"}}

### Кнопка <meta data-oversett="" data-original-text="Button">

{{"demo": "ButtonRouter.js"}}

**Примечание**: базовый компонент кнопки добавляет атрибут `role="button"`, когда определяет намерение отобразить кнопку без собственного элемента `<button>`. Это может создать проблемы при отображении ссылки. Если вы не используете один из реквизитов `href`, `to` или `component="a"`, вам нужно переопределить атрибут `role`. В приведенном выше примере это достигается установкой `role={undefined}` **после** реквизита spread.

```jsx
const LinkBehavior = React.forwardRef((props, ref) => (
  <RouterLink ref={ref} to="/" {...props} role={undefined} />
));
```

### Вкладки <meta data-oversett="" data-original-text="Tabs">

{{"demo": "TabsRouter.js", "defaultCodeOpen": false}}

### Список <meta data-oversett="" data-original-text="List">

{{"demo": "ListRouter.js"}}

## Другие примеры <meta data-oversett="" data-original-text="More examples">

### Next.js <meta data-oversett="" data-original-text="Next.js">

В [папке с примерами](https://github.com/mui/material-ui/tree/HEAD/examples/nextjs-with-typescript) представлен адаптер для использования [компонента Link из Next.js](https://nextjs.org/docs/api-reference/next/link) с MUI.

-   Первой версией адаптера является [`NextLinkComposed`](https://github.com/mui/material-ui/blob/HEAD/examples/nextjs-with-typescript/src/Link.tsx) компонент. Этот компонент не имеет стиля и отвечает только за обработку навигации. Реквизит `href` был переименован в `to`, чтобы избежать конфликта названий. Это похоже на компонент Link в react-router.
    
    ```tsx
    import Button from '@mui/material/Button';
    import { NextLinkComposed } from '../src/Link';
    
    export default function Index() {
      return (
        <Button
          component={NextLinkComposed}
          to={{
            pathname: '/about',
            query: { name: 'test' },
          }}
        >
          Button link
        </Button>
      );
    }
    ```
    
-   Вторая версия адаптера - компонент `Link`. Этот компонент стилизован. Он использует [компонент Link из MUI](/material-ui/react-link/) с помощью `NextLinkComposed`.
    
    ```tsx
    import Link from '../src/Link';
    
    export default function Index() {
      return (
        <Link
          href={{
            pathname: '/about',
            query: { name: 'test' },
          }}
        >
          Link
        </Link>
      );
    }
    ```
    

### Gatsby <meta data-oversett="" data-original-text="Gatsby">

Компонент [Link](https://www.gatsbyjs.com/docs/linking-between-pages/) в Gatsby построен на `@reach/router`. Вы можете использовать ту же предыдущую документацию для react-router. В отличие от Next.js, он не требует создания адаптера.
