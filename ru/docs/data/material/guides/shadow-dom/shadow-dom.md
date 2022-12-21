

# Теневой DOM <meta data-oversett="" data-original-text="Shadow DOM">

<p class="description">Теневой DOM позволяет инкапсулировать части приложения, чтобы отделить их от глобальных стилей, нацеленных на обычное дерево DOM.</p>

## Как использовать теневой DOM с Material UI <meta data-oversett="" data-original-text="How to use the shadow DOM with Material UI">

### 1\. Стили <meta data-oversett="" data-original-text="1. Styles">

Теневой DOM - это API, который предоставляет способ прикрепить скрытый разделенный DOM к элементу. Это полезно, когда вам нужно сохранить структуру, стиль и поведение различных компонентов отдельно от остального кода на странице, чтобы предотвратить конфликты. Более подробную информацию смотрите в [документации MDN по теневому DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM). Следующий фрагмент кода показывает, как применять стили внутри теневого DOM:

```tsx
const container = document.querySelector('#root');
const shadowContainer = container.attachShadow({ mode: 'open' });
const emotionRoot = document.createElement('style');
const shadowRootElement = document.createElement('div');
shadowContainer.appendChild(emotionRoot);
shadowContainer.appendChild(shadowRootElement);

const cache = createCache({
  key: 'css',
  prepend: true,
  container: emotionRoot,
});

ReactDOM.createRoot(shadowRootElement).render(
  <CacheProvider value={cache}>
    <App />
  </CacheProvider>,
);
```

### 2\. Тема <meta data-oversett="" data-original-text="2. Theme">

MUI компоненты, такие как `Menu`, `Dialog`, `Popover` и другие, используют [`Portal`](/material-ui/react-portal/) для рендеринга нового "поддерева" в контейнере вне текущей иерархии DOM. По умолчанию таким контейнером является `document.body`. Но поскольку стили применяются только внутри теневого DOM, нам необходимо рендерить порталы и внутри контейнера теневого DOM:

```tsx
const theme = createTheme({
  components: {
    MuiPopover: {
      defaultProps: {
        container: shadowRootElement,
      },
    },
    MuiPopper: {
      defaultProps: {
        container: shadowRootElement,
      },
    },
    MuiModal: {
      defaultProps: {
        container: shadowRootElement,
      },
    },
  },
});

// ...

<ThemeProvider theme={theme}>
  <App />
</ThemeProvider>;
```

## Демо <meta data-oversett="" data-original-text="Demo">

В приведенном ниже примере видно, что на компонент вне теневого DOM влияют глобальные стили, а на компонент внутри теневого DOM - нет:

{{"demo": "ShadowDOMDemo.js", "hideToolbar": true, "bg": true}}
