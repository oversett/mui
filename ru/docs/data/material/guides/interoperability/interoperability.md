

# Совместимость библиотек стилей <meta data-oversett="" data-original-text="Style library interoperability">

<p class="description">Хотя вы можете использовать для стилизации вашего приложения решение для стилей на основе Emotion, предоставляемое MUI, вы также можете использовать то, что вы уже знаете и любите (от простого CSS до styled-components).</p>

Целью данного руководства является документирование наиболее популярных альтернатив, но вы должны обнаружить, что принципы, применяемые здесь, могут быть адаптированы к другим библиотекам. Здесь приведены примеры для следующих решений стилизации:

-   [Обычный CSS](#plain-css)
-   [Глобальный CSS](#global-css)
-   [Стилизованные компоненты](#styled-components)
-   [Модули CSS](#css-modules)
-   [Emotion](#emotion)
-   [Tailwind CSS](#tailwind-css)
-   [~~JSS~~ TSS](#jss-tss)

## Простой CSS <meta data-oversett="" data-original-text="Plain CSS">

Ничего вычурного, просто обычный CSS.

{{"demo": "StyledComponents.js", "hideToolbar": true}}

[![Edit Button](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/plain-css-fdue7)

**PlainCssSlider.css**

```css
.slider {
  color: #20b2aa;
}

.slider:hover {
  color: #2e8b57;
}
```

**PlainCssSlider.js**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
import './PlainCssSlider.css';

export default function PlainCssSlider() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider defaultValue={30} className="slider" />
    </div>
  );
}
```

### Порядок внедрения CSS ⚠️ <meta data-oversett="" data-original-text="CSS injection order ⚠️">

**Примечание:** Большинство CSS-in-JS решений вставляют свои стили внизу HTML `<head>`, что дает MUI приоритет над вашими пользовательскими стилями. Чтобы устранить необходимость в **!important**, вам нужно изменить порядок введения CSS. Вот демонстрация того, как это можно сделать в MUI:

```jsx
import * as React from 'react';
import { StyledEngineProvider } from '@mui/material/styles';

export default function GlobalCssPriority() {
  return (
    <StyledEngineProvider injectFirst>
      {/* Your component tree. Now you can override MUI's styles. */}
    </StyledEngineProvider>
  );
}
```

**Примечание:** Если вы используете Emotion и в вашем приложении есть пользовательский кэш, то он будет иметь приоритет над кэшем, поступающим из MUI. Для того чтобы порядок инъекций был правильным, необходимо добавить опцию prepend. Вот пример:

```jsx
import * as React from 'react';
import { CacheProvider } from '@emotion/react';
import createCache from '@emotion/cache';

const cache = createCache({
  key: 'css',
  prepend: true,
});

export default function PlainCssPriority() {
  return (
    <CacheProvider value={cache}>
      {/* Your component tree. Now you can override MUI's styles. */}
    </CacheProvider>
  );
}
```

**Примечание:** Если вы используете styled-components и у вас есть `StyleSheetManager` с пользовательским `target`, убедитесь, что цель является первым элементом в HTML `<head>`. Если вам интересно посмотреть, как это можно сделать, вы можете взглянуть на [`StyledEngineProvider`](https://github.com/mui/material-ui/blob/master/packages/mui-styled-engine-sc/src/StyledEngineProvider/StyledEngineProvider.js) реализацию в пакете `@mui/styled-engine-sc`.

### Более глубокие элементы <meta data-oversett="" data-original-text="Deeper elements">

Если вы попытаетесь стилизовать слайдер, вам, скорее всего, придется затронуть некоторые дочерние элементы слайдера, например, большой палец. В MUI все дочерние элементы имеют повышенную специфичность 2: `.parent .child {}`. При написании переопределений необходимо делать то же самое.

В следующих примерах переопределяется стиль слайдера `thumb` в дополнение к пользовательским стилям самого слайдера.

{{"demo": "StyledComponentsDeep.js", "hideToolbar": true}}

**PlainCssSliderDeep1.css**

```css
.slider {
  color: #20b2aa;
}

.slider:hover {
  color: #2e8b57;
}

.slider .MuiSlider-thumb {
  border-radius: 1px;
}
```

**PlainCssSliderDeep1.js**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
import './PlainCssSliderDeep1.css';

export default function PlainCssSliderDeep1() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider defaultValue={30} className="slider" />
    </div>
  );
}
```

Приведенная выше демонстрация полагается на [значения по умолчанию `className`](/system/styles/advanced/) , но вы можете указать собственное имя класса с помощью API `slotProps`.

**PlainCssSliderDeep2.css**

```css
.slider {
  color: #20b2aa;
}

.slider:hover {
  color: #2e8b57;
}

.slider .thumb {
  border-radius: 1px;
}
```

**PlainCssSliderDeep2.js**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
import './PlainCssSliderDeep2.css';

export default function PlainCssSliderDeep2() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider
        defaultValue={30}
        className="slider"
        slotProps={{ thumb: { className: 'thumb' } }}
      />
    </div>
  );
}
```

## Глобальный CSS <meta data-oversett="" data-original-text="Global CSS">

Явное предоставление имен классов компоненту требует слишком много усилий?[Вы можете использовать имена классов, сгенерированные MUI](/system/styles/advanced/).

[![Edit Button](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/global-classnames-dho8k)

**GlobalCssSlider.css**

```css
.MuiSlider-root {
  color: #20b2aa;
}

.MuiSlider-root:hover {
  color: #2e8b57;
}
```

**GlobalCssSlider.js**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
import './GlobalCssSlider.css';

export default function GlobalCssSlider() {
  return <Slider defaultValue={30} />;
}
```

### Порядок внедрения CSS ⚠️ <meta data-oversett="" data-original-text="CSS injection order ⚠️">

**Примечание:** Большинство CSS-in-JS решений внедряют свои стили в нижней части HTML `<head>`, что дает MUI приоритет над вашими пользовательскими стилями. Чтобы устранить необходимость в **!important**, вам нужно изменить порядок введения CSS. Вот демонстрация того, как это можно сделать в MUI:

```jsx
import * as React from 'react';
import { StyledEngineProvider } from '@mui/material/styles';

export default function GlobalCssPriority() {
  return (
    <StyledEngineProvider injectFirst>
      {/* Your component tree. Now you can override MUI's styles. */}
    </StyledEngineProvider>
  );
}
```

**Примечание:** Если вы используете Emotion и в вашем приложении есть пользовательский кэш, то он будет иметь приоритет над кэшем, поступающим из MUI. Для того чтобы порядок инъекций был правильным, необходимо добавить опцию prepend. Вот пример:

```jsx
import * as React from 'react';
import { CacheProvider } from '@emotion/react';
import createCache from '@emotion/cache';

const cache = createCache({
  key: 'css',
  prepend: true,
});

export default function GlobalCssPriority() {
  return (
    <CacheProvider value={cache}>
      {/* Your component tree. Now you can override MUI's styles. */}
    </CacheProvider>
  );
}
```

**Примечание:** Если вы используете styled-components и у вас есть `StyleSheetManager` с пользовательским `target`, убедитесь, что target является первым элементом в HTML `<head>`. Если вам интересно посмотреть, как это можно сделать, вы можете взглянуть на [`StyledEngineProvider`](https://github.com/mui/material-ui/blob/master/packages/mui-styled-engine-sc/src/StyledEngineProvider/StyledEngineProvider.js) реализацию в пакете `@mui/styled-engine-sc`.

### Более глубокие элементы <meta data-oversett="" data-original-text="Deeper elements">

Если вы попытаетесь стилизовать слайдер, вам, скорее всего, придется затронуть некоторые дочерние элементы слайдера, например, большой палец. В MUI все дочерние элементы имеют повышенную специфичность 2: `.parent .child {}`. При написании переопределений необходимо делать то же самое.

В следующем примере переопределяется стиль слайдера `thumb` в дополнение к пользовательским стилям самого слайдера.

{{"demo": "StyledComponentsDeep.js", "hideToolbar": true}}

**GlobalCssSliderDeep.css**

```css
.MuiSlider-root {
  color: #20b2aa;
}

.MuiSlider-root:hover {
  color: #2e8b57;
}

.MuiSlider-root .MuiSlider-thumb {
  border-radius: 1px;
}
```

**GlobalCssSliderDeep.js**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
import './GlobalCssSliderDeep.css';

export default function GlobalCssSliderDeep() {
  return <Slider defaultValue={30} />;
}
```

## Стилизованные компоненты <meta data-oversett="" data-original-text="Styled Components">

![stars](https://img.shields.io/github/stars/styled-components/styled-components.svg?style=social&label=Star) ![npm](https://img.shields.io/npm/dm/styled-components.svg)

### Изменение стилизованного механизма по умолчанию <meta data-oversett="" data-original-text="Change the default styled engine">

По умолчанию компоненты MUI поставляются с Emotion в качестве движка стилей. Однако, если вы хотите использовать `styled-components`, вы можете настроить свое приложение, следуя [руководству по стилизованным движкам](/material-ui/guides/styled-engine/#how-to-switch-to-styled-components) или начав с одного из примеров проектов:

-   [Создание React App со стилизованными компонентами](https://github.com/mui/material-ui/tree/master/examples/create-react-app-with-styled-components)
-   [Создание React App со стилизованными компонентами и typescript](https://github.com/mui/material-ui/tree/master/examples/create-react-app-with-styled-components-typescript)

Следуя этому подходу, вы уменьшите размер пакета и избавитесь от необходимости настраивать порядок внедрения CSS.

После того, как механизм стилей настроен должным образом, вы можете воспользоваться утилитой [`styled()`](/system/styled/) утилиту из `@mui/material/styles` и получить прямой доступ к теме.

{{"demo": "StyledComponents.js", "hideToolbar": true}}

[![Edit Button](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/styled-components-interoperability-w9z9d)

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
import { styled } from '@mui/material/styles';

const CustomizedSlider = styled(Slider)`
  color: #20b2aa;

  :hover {
    color: #2e8b57;
  }
`;

export default function StyledComponents() {
  return <CustomizedSlider defaultValue={30} />;
}
```

### Более глубокие элементы <meta data-oversett="" data-original-text="Deeper elements">

Если вы попытаетесь стилизовать слайдер, вам, скорее всего, придется затронуть некоторые дочерние элементы слайдера, например, большой палец. В MUI все дочерние элементы имеют повышенную специфичность 2: `.parent .child {}`. При написании переопределений необходимо делать то же самое.

В следующих примерах переопределяется стиль слайдера `thumb` в дополнение к пользовательским стилям самого слайдера.

{{"demo": "StyledComponentsDeep.js", "defaultCodeOpen": true}}

В приведенном выше примере используются [значения по умолчанию `className`](/system/styles/advanced/) , но вы можете задать собственное имя класса с помощью API `slotProps`.

```jsx
import * as React from 'react';
import { styled } from '@mui/material/styles';
import Slider from '@mui/material/Slider';

const CustomizedSlider = styled((props) => (
  <Slider slotProps={{ thumb: { className: 'thumb' } }} {...props} />
))`
  color: #20b2aa;

  :hover {
    color: #2e8b57;
  }

  & .thumb {
    border-radius: 1px;
  }
`;

export default function StyledComponentsDeep2() {
  return (
    <div>
      <Slider defaultValue={30} />
      <CustomizedSlider defaultValue={30} />
    </div>
  );
}
```

### Тема <meta data-oversett="" data-original-text="Theme">

При использовании поставщика тем MUI тема будет доступна и в контексте темы стилизованного движка (Emotion или styled-components, в зависимости от вашей конфигурации).

:::warning
Если вы уже используете пользовательскую тему в styled-components или Emotion, она может быть несовместима со спецификацией темы MUI. Если она несовместима, вам нужно сначала визуализировать ThemeProvider MUI. Это обеспечит изолированность структур тем. Это идеально подходит для постепенного внедрения компонентов MUI в кодовую базу.
:::

Вам рекомендуется использовать один и тот же объект темы между MUI и остальными компонентами вашего проекта.

```jsx
const CustomizedSlider = styled(Slider)(
  ({ theme }) => `
  color: ${theme.palette.primary.main};

  :hover {
    color: ${darken(theme.palette.primary.main, 0.2)};
  }
`,
);
```

{{"demo": "StyledComponentsTheme.js"}}

### Порталы <meta data-oversett="" data-original-text="Portals">

[Портал](/material-ui/react-portal/) предоставляет первоклассный способ отображения дочерних элементов в узел DOM, который существует вне иерархии DOM родительского компонента. Из-за того, как styled-components определяет область применения CSS, вы можете столкнуться с проблемами, когда стилизация не применяется.

Например, если вы попытаетесь стилизовать `tooltip`, созданный компонентом [Tooltip](/material-ui/react-tooltip/), вам нужно будет передать свойство `className` элементу, отображаемому вне иерархии DOM. Следующий пример показывает обходной путь:

```jsx
import * as React from 'react';
import { styled } from '@mui/material/styles';
import Button from '@mui/material/Button';
import Tooltip from '@mui/material/Tooltip';

const StyledTooltip = styled(({ className, ...props }) => (
  <Tooltip {...props} classes={{ popper: className }} />
))`
  & .MuiTooltip-tooltip {
    background: navy;
  }
`;
```

{{"demo": "StyledComponentsPortal.js"}}

## Модули CSS <meta data-oversett="" data-original-text="CSS Modules">

![stars](https://img.shields.io/github/stars/css-modules/css-modules.svg?style=social&label=Star)

Трудно сказать, какова доля рынка [этого решения для стилизации](https://github.com/css-modules/css-modules), так как она зависит от того, какое решение для пакетирования используют люди.

{{"demo": "StyledComponents.js", "hideToolbar": true}}

[![Edit Button](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/css-modules-nuyg8)

**CssModulesSlider.module.css**

```css
.slider {
  color: #20b2aa;
}

.slider:hover {
  color: #2e8b57;
}
```

**CssModulesSlider.js**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';
// webpack, parcel or else will inject the CSS into the page
import styles from './CssModulesSlider.module.css';

export default function CssModulesSlider() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider defaultValue={30} className={styles.slider} />
    </div>
  );
}
```

### Порядок внедрения CSS ⚠️ <meta data-oversett="" data-original-text="CSS injection order ⚠️">

**Примечание:** Большинство CSS-in-JS решений внедряют свои стили в нижней части HTML `<head>`, что дает MUI приоритет над вашими пользовательскими стилями. Чтобы устранить необходимость в **!important**, вам нужно изменить порядок введения CSS. Вот демонстрация того, как это можно сделать в MUI:

```jsx
import * as React from 'react';
import { StyledEngineProvider } from '@mui/material/styles';

export default function GlobalCssPriority() {
  return (
    <StyledEngineProvider injectFirst>
      {/* Your component tree. Now you can override MUI's styles. */}
    </StyledEngineProvider>
  );
}
```

**Примечание:** Если вы используете Emotion и в вашем приложении есть пользовательский кэш, то он будет иметь приоритет над кэшем, поступающим из MUI. Для того чтобы порядок инъекций был правильным, необходимо добавить опцию prepend. Вот пример:

```jsx
import * as React from 'react';
import { CacheProvider } from '@emotion/react';
import createCache from '@emotion/cache';

const cache = createCache({
  key: 'css',
  prepend: true,
});

export default function CssModulesPriority() {
  return (
    <CacheProvider value={cache}>
      {/* Your component tree. Now you can override MUI's styles. */}
    </CacheProvider>
  );
}
```

**Примечание:** Если вы используете styled-components и у вас есть `StyleSheetManager` с пользовательским `target`, убедитесь, что целью является первый элемент в HTML `<head>`. Если вам интересно посмотреть, как это можно сделать, вы можете взглянуть на [`StyledEngineProvider`](https://github.com/mui/material-ui/blob/master/packages/mui-styled-engine-sc/src/StyledEngineProvider/StyledEngineProvider.js) реализацию в пакете `@mui/styled-engine-sc`.

### Более глубокие элементы <meta data-oversett="" data-original-text="Deeper elements">

Если вы попытаетесь стилизовать слайдер, вам, скорее всего, придется затронуть некоторые дочерние элементы слайдера, например, большой палец. В MUI все дочерние элементы имеют повышенную специфичность 2: `.parent .child {}`. При написании переопределений необходимо сделать то же самое. Важно помнить, что CSS Modules добавляет уникальный id к каждому классу, и этот id не будет присутствовать в дочерних классах MUI. Чтобы избежать этого, CSS Modules предоставляет функциональность - селектор `:global`.

В следующих примерах переопределяется стиль слайдера `thumb` в дополнение к пользовательским стилям самого слайдера.

{{"demo": "StyledComponentsDeep.js", "hideToolbar": true}}

**CssModulesSliderDeep1.module.css**

```css
.slider {
  color: #20b2aa;
}

.slider:hover {
  color: #2e8b57;
}

.slider :global .MuiSlider-thumb {
  border-radius: 1px;
}
```

**CssModulesSliderDeep1.js**

```jsx
import * as React from 'react';
// webpack, parcel or else will inject the CSS into the page
import styles from './CssModulesSliderDeep1.module.css';
import Slider from '@mui/material/Slider';

export default function CssModulesSliderDeep1() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider defaultValue={30} className={styles.slider} />
    </div>
  );
}
```

Приведенная выше демонстрация полагается на [значения по умолчанию `className`](/system/styles/advanced/) , но вы можете указать собственное имя класса с помощью API `slotProps`.

**CssModulesSliderDeep2.module.css**

```css
.slider {
  color: #20b2aa;
}

.slider:hover {
  color: #2e8b57;
}

.slider .thumb {
  border-radius: 1px;
}
```

**CssModulesSliderDeep2.js**

```jsx
import * as React from 'react';
// webpack, parcel or else will inject the CSS into the page
import styles from './CssModulesSliderDeep2.module.css';
import Slider from '@mui/material/Slider';

export default function CssModulesSliderDeep2() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider
        defaultValue={30}
        className={styles.slider}
        slotProps={{ thumb: { className: styles.thumb } }}
      />
    </div>
  );
}
```

## Эмоция <meta data-oversett="" data-original-text="Emotion">

![stars](https://img.shields.io/github/stars/emotion-js/emotion.svg?style=social&label=Star) ![npm](https://img.shields.io/npm/dm/@emotion/react.svg)

### Реквизит `css` <meta data-oversett="" data-original-text="The css prop">

Метод **css()** модуля Emotion работает без проблем с MUI.

{{"demo": "EmotionCSS.js", "defaultCodeOpen": true}}

### Тема <meta data-oversett="" data-original-text="Theme">

Она работает точно так же, как и стилизованные компоненты. Вы можете [использовать то же руководство](/material-ui/guides/interoperability/#styled-components).

### API `styled()` <meta data-oversett="" data-original-text="The styled() API">

Работает точно так же, как и стилизованные компоненты. Вы можете [воспользоваться тем же руководством](/material-ui/guides/interoperability/#styled-components).

## Tailwind CSS <meta data-oversett="" data-original-text="Tailwind CSS">

![stars](https://img.shields.io/github/stars/tailwindlabs/tailwindcss.svg?style=social&label=Star) ![npm](https://img.shields.io/npm/dm/tailwindcss)

### Настройка <meta data-oversett="" data-original-text="Setup">

Если вы привыкли к Tailwind CSS и хотите использовать его вместе с компонентами MUI, вы можете начать с клонирования проекта примера [Tailwind CSS](https://github.com/mui/material-ui/tree/master/examples/tailwind-css). Если вы используете другой фреймворк или уже настроили свой проект, выполните следующие шаги:

1.  Добавьте Tailwind CSS в свой проект, следуя инструкциям на сайте [https://tailwindcss.com/docs/installation.](https://tailwindcss.com/docs/installation)
2.  Удалите стиль [префлайта Tailwind CSS](https://tailwindcss.com/docs/preflight), чтобы вместо него использовать префлайт MUI[(CssBaseline](/material-ui/react-css-baseline/)).

**tailwind.config.js**

```diff
 module.exports = {
+  corePlugins: {
+    preflight: false,
+  },
 };
```

3.  Добавьте параметр `important`, используя идентификатор обертки вашего приложения. Например, `#__next` для Next.js и `"#root"` для CRA:

**tailwind.config.js**

```diff
 module.exports = {
   content: [
     "./src/**/*.{js,jsx,ts,tsx}",
   ],
+  important: '#root',
   theme: {
     extend: {},
   },
   plugins: [],
 }
```

Большинство CSS, используемых в Material UI, имеют специфичность 1, поэтому это свойство `important` не нужно. Однако в некоторых крайних случаях MUI использует вложенные селекторы CSS, которые выигрывают у Tailwind CSS. Используйте этот шаг, чтобы убедиться, что [более глубокие элементы](#deeper-elements-5) всегда можно настроить с помощью вспомогательных классов Tailwind. Подробнее об этой опции можно прочитать здесь [https://tailwindcss.com/docs/configuration#selector-strategy](https://tailwindcss.com/docs/configuration#selector-strategy).

4.  Исправьте порядок инъекции CSS. Большинство решений CSS-in-JS внедряют свои стили внизу HTML `<head>`, что дает MUI преимущество перед Tailwind CSS. Чтобы уменьшить потребность в свойстве `important`, необходимо изменить порядок внедрения CSS. Вот демонстрация того, как это можно сделать в MUI:

```jsx
import * as React from 'react';
import { StyledEngineProvider } from '@mui/material/styles';

export default function GlobalCssPriority() {
  return (
    <StyledEngineProvider injectFirst>
      {/* Your component tree. Now you can override MUI's styles. */}
    </StyledEngineProvider>
  );
}
```

**Примечание:** Если вы используете Emotion и в вашем приложении есть пользовательский кэш, он будет переопределять кэш, поступающий из MUI. Для того чтобы порядок инъекций был правильным, необходимо добавить опцию prepend. Вот пример:

```jsx
import * as React from 'react';
import { CacheProvider } from '@emotion/react';
import createCache from '@emotion/cache';

const cache = createCache({
  key: 'css',
  prepend: true,
});

export default function PlainCssPriority() {
  return (
    <CacheProvider value={cache}>
      {/* Your component tree. Now you can override MUI's styles. */}
    </CacheProvider>
  );
}
```

**Примечание:** Если вы используете styled-components и у вас есть `StyleSheetManager` с пользовательским `target`, убедитесь, что target является первым элементом в HTML `<head>`. Если вам интересно посмотреть, как это можно сделать, вы можете взглянуть на [`StyledEngineProvider`](https://github.com/mui/material-ui/blob/master/packages/mui-styled-engine-sc/src/StyledEngineProvider/StyledEngineProvider.js) реализацию в пакете `@mui/styled-engine-sc`.

5.  Измените целевой контейнер для `Portal`\-связанных элементов так, чтобы они внедрялись под оберткой основного приложения, которая использовалась в шаге 3 для установки опции `important` в конфигурации Tailwind.

```jsx
const rootElement = document.getElementById("root");
const root = createRoot(rootElement);

const theme = createTheme({
  components: {
    MuiPopover: {
      defaultProps: {
        container: rootElement,
      },
    },
    MuiPopper: {
      defaultProps: {
        container: rootElement,
      },
    },
  },
});

root.render(
  <StyledEngineProvider injectFirst>
    <ThemeProvider theme={theme}>
      <App />
    </ThemeProvider>
  </StyledEngineProvider>;
);
```

### Использование <meta data-oversett="" data-original-text="Usage">

Теперь все готово, и вы можете начать использовать Tailwind CSS в компонентах MUI!

{{"demo": "StyledComponents.js", "hideToolbar": true}}

[![Edit on StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/edit/github-ndkshy?file=pages%2Findex.tsx)

**index.tsx**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';

export default function App() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider defaultValue={30} className="text-teal-600" />
    </div>
  );
}
```

### Более глубокие элементы <meta data-oversett="" data-original-text="Deeper elements">

Если вы попытаетесь изменить стиль, например, слайдера, вы, скорее всего, захотите настроить его дочерние элементы.

В этом примере показано, как переопределить стиль слайдера `thumb`.

{{"demo": "StyledComponentsDeep.js", "hideToolbar": true}}

**SliderThumbOverrides.tsx**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';

export default function SliderThumbOverrides() {
  return (
    <div>
      <Slider defaultValue={30} />
      <Slider
        defaultValue={30}
        className="text-teal-600"
        slotProps={{ thumb: { className: 'rounded-sm' } }}
      />
    </div>
  );
}
```

### Стилизация псевдосостояний <meta data-oversett="" data-original-text="Styling pseudo states">

Если вы хотите стилизовать псевдосостояние компонента, вы можете использовать соответствующий ключ в реквизите `classes`. Вот пример того, как вы можете стилизовать активное состояние слайдера:

**SliderPseudoStateOverrides.tsx**

```jsx
import * as React from 'react';
import Slider from '@mui/material/Slider';

export default function SliderThumbOverrides() {
  return <Slider defaultValue={30} classes={{ active: 'shadow-none' }} />;
}
```

## ~~JSS~~ TSS <meta data-oversett="" data-original-text="JSS TSS">

Сам [JSS](https://cssinjs.org/) больше не поддерживается в MUI, однако, если вам нравится API на основе хуков (`makeStyles` → `useStyles`), который [`react-jss`](https://codesandbox.io/s/j3l06yyqpw) который был предложен, вы можете выбрать [`tss-react`](https://github.com/garronej/tss-react).

[TSS](https://docs.tss-react.dev) хорошо интегрируется с MUI и обеспечивает лучшую поддержку TypeScript, чем JSS.

:::info
Если вы переходите с `@material-ui/core` (v4) на `@mui/material` (v5), ознакомьтесь с [разделом tss-react](/material-ui/migration/migrating-from-jss/#2-use-tss-react) руководства по миграции.
:::

```tsx
import { render } from 'react-dom';
import { CacheProvider } from '@emotion/react';
import createCache from '@emotion/cache';
import { ThemeProvider } from '@mui/material/styles';

export const muiCache = createCache({
  key: 'mui',
  prepend: true,
});

//NOTE: Don't use <StyledEngineProvider injectFirst/>
render(
  <CacheProvider value={muiCache}>
    <ThemeProvider theme={myTheme}>
      <Root />
    </ThemeProvider>
  </CacheProvider>,
  document.getElementById('root'),
);
```

Теперь вы можете просто`import { makeStyles, withStyles } from 'tss-react/mui'`. Объект темы, который будет передан вашим функциям обратного вызова, будет тем же, который вы получили с помощью`import { useTheme } from '@mui/material/styles'`.

Если вы хотите контролировать, каким должен быть объект `theme`, вы можете реэкспортировать `makeStyles` и `withStyles` из файла с именем, например, `makesStyles.ts`:

```ts
import { useTheme } from '@mui/material/styles';
//WARNING: tss-react require TypeScript v4.4 or newer. If you can't update use:
//import { createMakeAndWithStyles } from "tss-react/compat";
import { createMakeAndWithStyles } from 'tss-react';

export const { makeStyles, withStyles } = createMakeAndWithStyles({
  useTheme,
  /*
    OR, if you have extended the default mui theme adding your own custom properties:
    Let's assume the myTheme object that you provide to the <ThemeProvider /> is of
    type MyTheme then you'll write:
    */
  //"useTheme": useTheme as (()=> MyTheme)
});
```

Затем библиотека используется следующим образом:

```tsx
import { makeStyles } from 'tss-react/mui';

export function MyComponent(props: Props) {
  const { className } = props;

  const [color, setColor] = useState<'red' | 'blue'>('red');

  const { classes, cx } = useStyles({ color });

  //Thanks to cx, className will take priority over classes.root
  return <span className={cx(classes.root, className)}>hello world</span>;
}

const useStyles = makeStyles<{ color: 'red' | 'blue' }>()((theme, { color }) => ({
  root: {
    color,
    '&:hover': {
      backgroundColor: theme.palette.primary.main,
    },
  },
}));
```

Для получения информации о том, как настроить SSR или что-либо еще, пожалуйста, обратитесь к [документации TSS](https://github.com/garronej/tss-react).

:::info
Существует [плагин ESLint](https://docs.tss-react.dev/detecting-unused-classes) для обнаружения неиспользуемых классов.
:::

:::warning
Сохраните **`@emotion/styled` как зависимость вашего проекта**. Даже если вы никогда не используете его в явном виде, он является зависимостью от аналога `@mui/material`.
:::
