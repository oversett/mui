

# Установка <meta data-oversett="" data-original-text="Installation">

<p class="description">Установите Material UI, самый популярный в мире фреймворк React UI.</p>

## Установка по умолчанию <meta data-oversett="" data-original-text="Default installation">

Выполните одну из следующих команд, чтобы добавить Material UI в свой проект:

### npm <meta data-oversett="" data-original-text="npm">

```sh
npm install @mui/material @emotion/react @emotion/styled
```

### yarn <meta data-oversett="" data-original-text="yarn">

```sh
yarn add @mui/material @emotion/react @emotion/styled
```

## Со стилизованными компонентами <meta data-oversett="" data-original-text="With styled-components">

Material UI использует [Emotion](https://emotion.sh/) в качестве движка стилизации по умолчанию. Если вы хотите использовать вместо него [styled-components](https://styled-components.com/), выполните одну из следующих команд:

### npm <meta data-oversett="" data-original-text="npm">

```sh
npm install @mui/material @mui/styled-engine-sc styled-components
```

### yarn <meta data-oversett="" data-original-text="yarn">

```sh
yarn add @mui/material @mui/styled-engine-sc styled-components
```

:::warning
Посетите [руководство по движку Styled](/material-ui/guides/styled-engine/) для получения дополнительной информации о том, как настроить styled-components.
:::

## Зависимости Peer <meta data-oversett="" data-original-text="Peer dependencies">

[`react`](https://www.npmjs.com/package/react) >= 17.0.0 и [`react-dom`](https://www.npmjs.com/package/react-dom) >= 17.0.0 являются одноранговыми зависимостями.

## Шрифт Roboto <meta data-oversett="" data-original-text="Roboto font">

В Material UI по умолчанию используется шрифт [Roboto](https://fonts.google.com/specimen/Roboto). Вы можете добавить его в свой проект с помощью npm или yarn через [Fontsource](https://fontsource.org/), или с помощью Google Fonts CDN.

### npm <meta data-oversett="" data-original-text="npm">

```sh
npm install @fontsource/roboto
```

### yarn <meta data-oversett="" data-original-text="yarn">

```sh
yarn add @fontsource/roboto
```

Затем вы можете импортировать его в точку входа следующим образом:

```tsx
import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
```

:::info
Fontsource можно настроить на загрузку определенных подмножеств, весов и стилей. Конфигурация типографики Material UI по умолчанию использует только шрифты весом 300, 400, 500 и 700.
:::

### Веб-шрифты Google <meta data-oversett="" data-original-text="Google Web Fonts">

Чтобы установить шрифт Roboto в свой проект с помощью Google Web Fonts CDN, добавьте следующий фрагмент кода в тег `<head />` вашего проекта:

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
/>
```

## Icons <meta data-oversett="" data-original-text="Icons">

Чтобы использовать [компонент шрифта Icon](/material-ui/icons/#icon-font-icons) или готовые SVG-иконки Material Icons (например, те, что представлены в [демонстрационных версиях иконок](/material-ui/icons/)), необходимо сначала установить шрифт [Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons). Это можно сделать с помощью npm или yarn, а также с помощью Google Web Fonts CDN.

### npm <meta data-oversett="" data-original-text="npm">

```sh
npm install @mui/icons-material
```

### yarn <meta data-oversett="" data-original-text="yarn">

```sh
yarn add @mui/icons-material
```

### Google Web Fonts <meta data-oversett="" data-original-text="Google Web Fonts">

Чтобы установить шрифт Material Icons в свой проект с помощью Google Web Fonts CDN, добавьте следующий фрагмент кода в тег `<head />` вашего проекта:

Чтобы использовать компонент font `Icon`, необходимо сначала добавить шрифт [Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons). Вот [некоторые инструкции](/material-ui/icons/#icon-font-icons)о том, как это сделать. Например, через Google Web Fonts:

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/icon?family=Material+Icons"
/>
```

## CDN . <meta data-oversett="" data-original-text="CDN">

Вы можете сразу же начать использовать Material UI с минимальной инфраструктурой front-end, установив его через CDN, что является отличным вариантом для быстрого создания прототипов. Чтобы начать работу, следуйте [этому примеру с CDN](https://github.com/mui/material-ui/tree/master/examples/cdn).

:::error
Мы _не_ рекомендуем использовать этот подход в производстве. Он требует от клиента загрузки всей библиотеки - независимо от того, какие компоненты фактически используются - что негативно сказывается на производительности и использовании полосы пропускания.
:::

Предоставляются два файла Universal Module Definition (UMD):

-   один для разработки: [https://unpkg.com/@mui/material@latest/umd/material-ui.development.js](https://unpkg.com/@mui/material@latest/umd/material-ui.development.js)
-   один для производства: [https://unpkg.com/@mui/material@latest/umd/material-ui.production.min.js](https://unpkg.com/@mui/material@latest/umd/material-ui.production.min.js)

:::warning
Ссылки UMD используют тег `latest` для указания на последнюю версию библиотеки. Этот указатель _нестабилен_ и может изменяться по мере выпуска новых версий. Вам следует рассмотреть возможность указания на конкретную версию, например, [v5.0.0](https://unpkg.com/@mui/material@5.0.0/umd/material-ui.development.js).
:::
