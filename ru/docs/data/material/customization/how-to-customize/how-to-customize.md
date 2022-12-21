---
product: material-ui
components: GlobalStyles
---

# Как настроить <meta data-oversett="" data-original-text="How to customize">

<p class="description">Узнайте, как настраивать компоненты Material UI, используя различные стратегии для конкретных случаев использования.</p>

Material UI предоставляет несколько различных способов настройки стилей компонентов. Ваш конкретный контекст определит, какой из них будет идеальным. Ниже перечислены варианты от самого узкого до самого широкого случая использования:

1.  [Разовая настройка](#1-one-off-customization)
2.  [Многоразовый компонент](#2-reusable-component)
3.  [Глобальные переопределения темы](#3-global-theme-overrides)
4.  [Глобальное переопределение CSS](#4-global-css-override)

## 1\. Одноразовая настройка <meta data-oversett="" data-original-text="1. One-off customization">

Чтобы изменить стили _одного единственного экземпляра_ компонента, вы можете использовать одну из следующих опций:

### Реквизит `sx` <meta data-oversett="" data-original-text="The sx prop">

[Реквизит`sx`](/system/getting-started/the-sx-prop/) в большинстве случаев является лучшим вариантом для добавления переопределения стилей к одному экземпляру компонента. Его можно использовать со всеми компонентами Material UI.

{{"demo": "SxProp.js" }}

#### Переопределение стилей вложенных компонентов <meta data-oversett="" data-original-text="Overriding nested component styles">

Чтобы настроить определенную часть компонента, вы можете использовать имя класса, предоставленное Material UI, внутри реквизита `sx`. В качестве примера, допустим, вы хотите изменить большой палец компонента `Slider` с круга на квадрат.

Сначала используйте инструменты dev вашего браузера, чтобы определить класс для слота компонента, который вы хотите переопределить.

Стили, внедряемые в DOM с помощью Material UI, опираются на имена классов, которые все [следуют стандартному шаблону](/system/styles/advanced/#class-names):`[hash]-Mui[Component name]-[name of the slot]`.

В данном случае стили применяются с помощью `.css-ae2u5c-MuiSlider-thumb`, но на самом деле вам нужно указать только класс `.MuiSlider-thumb`, где `Slider` - компонент, а `thumb` - слот. Используйте это имя класса, чтобы написать CSS-селектор внутри реквизита `sx` (`& .MuiSlider-thumb`), и добавьте свои переопределения.

<img src="/static/images/customization/dev-tools.png" alt="dev-tools" width="796" style="margin-bottom: 16px;">

{{"demo": "DevTools.js"}}

:::warning
Эти имена классов нельзя использовать в качестве селекторов CSS, поскольку они нестабильны.
:::

### Переопределение стилей с помощью имен классов <meta data-oversett="" data-original-text="Overriding styles with class names">

Если вы хотите переопределить стили компонента с помощью пользовательских классов, вы можете использовать реквизит `className`, доступный для каждого компонента. Чтобы переопределить стили определенной части компонента, используйте глобальные классы, предоставляемые Material UI, как описано в предыдущем разделе **"Переопределение стилей вложенных компонентов"** в [разделе реквизит`sx`](#the-sx-prop) .

Посетите руководство по [совместимости библиотек стилей](/material-ui/guides/interoperability/), чтобы найти примеры такого подхода с использованием различных библиотек стилей.

### Классы состояний <meta data-oversett="" data-original-text="State classes">

Такие состояния, как _hover_, _focus_, _disabled_ и _selected_, стилизуются с большей специфичностью CSS. Чтобы настроить их, необходимо **увеличить специфичность**.

Вот пример с _отключенным_ состоянием и компонентом `Button` с использованием псевдокласса (`:disabled`):

```css
.Button {
  color: black;
}

/* Increase the specificity */
.Button:disabled {
  color: white;
}
```

```jsx
<Button disabled className="Button">
```

Вы не всегда можете использовать псевдоклассы CSS, поскольку состояние не существует в веб-спецификации. Возьмем в качестве примера компонент `MenuItem` и его _выбранное_ состояние. В этой ситуации вы можете использовать **классы состояний** Material UI, которые действуют так же, как псевдоклассы CSS. Используйте имя глобального класса `.Mui-selected` для настройки специального состояния компонента `MenuItem`:

```css
.MenuItem {
  color: black;
}

/* Increase the specificity */
.MenuItem.Mui-selected {
  color: blue;
}
```

```jsx
<MenuItem selected className="MenuItem">
```

Если вы хотите узнать больше об этой теме, рекомендуем ознакомиться с [MDN Web Docs on CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity).

#### Почему мне нужно увеличить специфичность, чтобы переопределить состояние одного компонента? <meta data-oversett="" data-original-text="Why do I need to increase specificity to override one component state?">

Псевдоклассы CSS имеют высокий уровень специфичности. Для согласованности с родными элементами классы состояний Material UI имеют тот же уровень специфичности, что и псевдоклассы CSS, что позволяет нацеливаться на состояние отдельного компонента.

#### Какие пользовательские классы состояний доступны в Material UI? <meta data-oversett="" data-original-text="What custom state classes are available in Material UI?">

Вы можете полагаться на следующие [имена глобальных классов](/system/styles/advanced/#class-names), генерируемые Material UI:

| Состояние | Имя глобального класса |
| --- | --- |
| активный | `.Mui-active` |
| проверено | `.Mui-checked` |
| завершено | `.Mui-completed` |
| отключен | `.Mui-disabled` |
| ошибка | `.Mui-error` |
| расширенный | `.Mui-expanded` |
| фокус видимый | `.Mui-focusVisible` |
| сфокусированный | `.Mui-focused` |
| необходимый | `.Mui-required` |
| выбран | `.Mui-selected` |

:::error
Никогда не применяйте стили непосредственно к именам классов состояний. Это повлияет на все компоненты с непонятными побочными эффектами. Всегда нацеливайте класс состояния вместе с компонентом.
:::

```css
/* ❌ NOT OK */
.Mui-error {
  color: red;
}

/* ✅ OK */
.MuiOutlinedInput-root.Mui-error {
  color: red;
}
```

## 2\. Многоразовый компонент <meta data-oversett="" data-original-text="2. Reusable component">

Чтобы повторно использовать одни и те же переопределения в разных местах вашего приложения, создайте компонент многократного использования с помощью [`styled()`](/system/styled/) утилиту:

{{"demo": "StyledCustomization.js", "defaultCodeOpen": true}}

### Динамические переопределения <meta data-oversett="" data-original-text="Dynamic overrides">

Утилита `styled()` позволяет добавлять динамические стили на основе реквизитов компонента. Это можно сделать с помощью **динамического CSS** или **переменных CSS**.

#### Динамический CSS <meta data-oversett="" data-original-text="Dynamic CSS">

:::warning
Если вы используете TypeScript, вам нужно будет обновить типы реквизитов нового компонента.
:::

{{"demo": "DynamicCSS.js", "defaultCodeOpen": false}}

```tsx
import * as React from 'react';
import { styled } from '@mui/material/styles';
import Slider, { SliderProps } from '@mui/material/Slider';

interface StyledSliderProps extends SliderProps {
  success?: boolean;
}

const StyledSlider = styled(Slider, {
  shouldForwardProp: (prop) => prop !== 'success',
})<StyledSliderProps>(({ success, theme }) => ({
  ...(success &&
    {
      // the overrides added when the new prop is used
    }),
}));
```

#### CSS-переменные <meta data-oversett="" data-original-text="CSS variables">

{{"demo": "DynamicCSSVariables.js"}}

## 3\. Глобальные переопределения темы <meta data-oversett="" data-original-text="3. Global theme overrides">

Material UI предоставляет инструменты темы для управления согласованностью стиля всех компонентов пользовательского интерфейса. Для получения дополнительной информации посетите страницу [настройки темы компонента](/material-ui/customization/theme-components/).

## 4\. Глобальное переопределение CSS <meta data-oversett="" data-original-text="4. Global CSS override">

Чтобы добавить глобальные базовые стили для некоторых элементов HTML, используйте компонент `GlobalStyles`. Вот пример того, как можно переопределить стили для элементов `h1`:

{{"demo": "GlobalCssOverride.js", "iframe": true, "height": 100}}

Если вы уже используете компонент [CssBaseline](/material-ui/react-css-baseline/) для установки базовых стилей, вы также можете добавить эти глобальные стили в качестве переопределений для этого компонента. Вот как вы можете добиться того же самого, используя этот подход.

{{"demo": "OverrideCssBaseline.js", "iframe": true, "height": 100}}

Ключ `styleOverrides` в слоте компонента `MuiCssBaseline` также поддерживает обратный вызов, с помощью которого вы можете получить доступ к теме. Вот как вы можете добиться того же, используя этот подход.

{{"demo": "OverrideCallbackCssBaseline.js", "iframe": true, "height": 100}}

:::success
Хорошей практикой является привязка `<GlobalStyles />` к статической константе, чтобы избежать повторного рендеринга. Это гарантирует, что генерируемый тег `<style>` не будет пересчитываться при каждом рендеринге.
:::

```diff
 import * as React from 'react';
 import GlobalStyles from '@mui/material/GlobalStyles';

+const inputGlobalStyles = <GlobalStyles styles={...} />;

 function Input(props) {
   return (
     <React.Fragment>
-      <GlobalStyles styles={...} />
+      {inputGlobalStyles}
       <input {...props} />
     </React.Fragment>
   )
 }
```
