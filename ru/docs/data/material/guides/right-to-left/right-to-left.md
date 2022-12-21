

# Право-лево <meta data-oversett="" data-original-text="Right-to-left">

<p class="description">Поддерживаются языки с правым направлением, такие как арабский, персидский или иврит. Чтобы изменить направление компонентов MUI, необходимо выполнить следующие шаги.</p>

## Шаги <meta data-oversett="" data-original-text="Steps">

### 1\. HTML <meta data-oversett="" data-original-text="1. HTML">

Убедитесь, что атрибут `dir` установлен на теге `html`, иначе родные компоненты будут сломаны:

```html
<html dir="rtl"></html>
```

Если вам нужно изменить направление текста во время выполнения, но React не управляет корневым элементом HTML, вы можете использовать JS API:

```js
document.dir = 'rtl';
```

В качестве альтернативы вышеописанному, вы также можете обернуть ваше приложение (или его часть) в элемент с атрибутом `dir`. Однако это не будет корректно работать с портированными элементами, такими как Dialogs, так как они будут отображаться вне элемента с атрибутом `dir`.

Чтобы исправить портированные компоненты, добавьте к ним явный атрибут `dir`:

```jsx
<Dialog dir="rtl">
  <MyComponent />
</Dialog>
```

### 2\. Тема <meta data-oversett="" data-original-text="2. Theme">

Установите направление в вашей пользовательской теме:

```js
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  direction: 'rtl',
});
```

### 3\. Установите плагин rtl <meta data-oversett="" data-original-text="3. Install the rtl plugin">

При использовании `emotion` или `styled-components` необходимо [`stylis-plugin-rtl`](https://github.com/styled-components/stylis-plugin-rtl) перевернуть стили.

```sh
npm install stylis stylis-plugin-rtl
```

:::warning
Только Emotion совместим с версией 2 плагина. `styled-components` требует версии 1. Если вы используете `styled-components` в качестве [стилизованного движка](/material-ui/guides/styled-engine/), убедитесь, что установили правильную версию.
:::

Если вы используете `jss` (до версии 4) или старый пакет `@mui/styles`, вам необходимо [`jss-rtl`](https://github.com/alitaheri/jss-rtl) перевернуть стили.

```sh
npm install jss-rtl
```

После установки плагина в ваш проект, компоненты MUI все еще требуют, чтобы он был загружен экземпляром движка стилей, который вы используете. Найдите ниже руководства о том, как его загрузить.

### 4\. Загрузка плагина rtl <meta data-oversett="" data-original-text="4. Load the rtl plugin">

#### 4.1 Emotion <meta data-oversett="" data-original-text="4.1 Emotion">

Если вы используете Emotion в качестве движка стилей, вам следует создать новый экземпляр кэша, использующий `stylis-plugin-rtl` (плагин по умолчанию `prefixer` также должен быть включен, чтобы сохранить префиксацию поставщиков) и разместить его в верхней части дерева вашего приложения. Компонент [CacheProvider](https://emotion.sh/docs/cache-provider) позволяет это сделать:

```jsx
import rtlPlugin from 'stylis-plugin-rtl';
import { CacheProvider } from '@emotion/react';
import createCache from '@emotion/cache';
import { prefixer } from 'stylis';

// Create rtl cache
const cacheRtl = createCache({
  key: 'muirtl',
  stylisPlugins: [prefixer, rtlPlugin],
});

function RTL(props) {
  return <CacheProvider value={cacheRtl}>{props.children}</CacheProvider>;
}
```

#### 4.2 стилизованные компоненты <meta data-oversett="" data-original-text="4.2 styled-components">

Если вы используете `styled-components` в качестве механизма стилей, вы можете использовать [StyleSheetManager](https://styled-components.com/docs/api#stylesheetmanager) и предоставить stylis-plugin-rtl в качестве элемента в свойстве `stylisPlugins`:

```jsx
import { StyleSheetManager } from 'styled-components';
import rtlPlugin from 'stylis-plugin-rtl';

function RTL(props) {
  return (
    <StyleSheetManager stylisPlugins={[rtlPlugin]}>
      {props.children}
    </StyleSheetManager>
  );
}
```

#### 4.3 JSS <meta data-oversett="" data-original-text="4.3 JSS">

После установки плагина в проект необходимо настроить экземпляр JSS для его загрузки. Следующим шагом будет сделать новый экземпляр JSS доступным для всех компонентов в дереве компонентов. [`StylesProvider`](/system/styles/api/#stylesprovider) компонент позволяет это сделать:

```jsx
import { create } from 'jss';
import rtl from 'jss-rtl';
import { StylesProvider, jssPreset } from '@mui/styles';

// Configure JSS
const jss = create({
  plugins: [...jssPreset().plugins, rtl()],
});

function RTL(props) {
  return <StylesProvider jss={jss}>{props.children}</StylesProvider>;
}
```

Для получения дополнительной информации о плагине, перейдите в [README плагина](https://github.com/alitaheri/jss-rtl).**Примечание**: Внутренне, withStyles использует этот JSS плагин, когда `direction: 'rtl'` установлен в теме.

## Демонстрация <meta data-oversett="" data-original-text="Demo">

_Используйте кнопку переключения направления в правом верхнем углу, чтобы перевернуть всю документацию_

{{"demo": "Direction.js"}}

## Отказ от трансформации rtl <meta data-oversett="" data-original-text="Opting out of rtl transformation">

### Эмоции и стилизованные компоненты <meta data-oversett="" data-original-text="Emotion &amp; styled-components">

Вы должны использовать синтаксис шаблонного литерала и добавить директиву `/* @noflip */` перед правилом или свойством, для которого вы хотите отключить право-левые стили.

```jsx
const AffectedText = styled('div')`
  text-align: left;
`;

const UnaffectedText = styled('div')`
  /* @noflip */
  text-align: left;
`;
```

{{"demo": "RtlOptOutStylis.js", "hideToolbar": true}}

### JSS <meta data-oversett="" data-original-text="JSS">

Если вы хотите предотвратить воздействие трансформации `rtl` на определенный набор правил, вы можете добавить `flip: false` в начале.

```jsx
const useStyles = makeStyles(
  (theme) => ({
    affected: {
      textAlign: 'right',
    },
    unaffected: {
      flip: false,
      textAlign: 'right',
    },
  }),
  { defaultTheme },
);
```
