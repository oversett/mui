---
product: material-ui
title: React Typography component
components: Typography
githubLabel: 'component: Typography'
materialDesign: https://m2.material.io/design/typography/the-type-system.html
---

# Типографика <meta data-oversett="" data-original-text="Typography">

<p class="description">Используйте типографику, чтобы представить дизайн и контент как можно более четко и эффективно.</p>

Слишком большое количество размеров и стилей шрифта одновременно может испортить любой макет. [Шрифтовая шкала](https://m2.material.io/design/typography/#type-scale) имеет ограниченный набор размеров шрифта, которые хорошо работают вместе с сеткой макета.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Общие сведения <meta data-oversett="" data-original-text="General">

Шрифт _Roboto_ **не** будет автоматически загружаться MUI. Вы сами отвечаете за загрузку любых шрифтов, используемых в вашем приложении. Шрифт Roboto имеет несколько простых способов начать работу. Для более продвинутой настройки ознакомьтесь с[разделом настройки темы](/material-ui/customization/typography/).

## CDN Roboto Font <meta data-oversett="" data-original-text="Roboto Font CDN">

Ниже показан пример разметки ссылки, используемой для загрузки шрифта Roboto из CDN:

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
/>
```

## Установить с помощью npm <meta data-oversett="" data-original-text="Install with npm">

Вы можете [установить его](https://www.npmjs.com/package/@fontsource/roboto), выполнив одну из следующих команд в терминале:

С помощью **npm**:

`npm install @fontsource/roboto`

Или **yarn**:

`yarn add @fontsource/roboto`

Затем вы можете импортировать его в свою точку входа.

```js
import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
```

Для получения дополнительной информации ознакомьтесь с [Fontsource](https://github.com/fontsource/fontsource).

Fontsource можно настроить на загрузку определенных подмножеств, весов и стилей. В конфигурации типографики MUI по умолчанию используются только шрифты весом 300, 400, 500 и 700.

## Компонент <meta data-oversett="" data-original-text="Component">

Компонент Typography позволяет легко применить набор весов и размеров шрифтов по умолчанию в вашем приложении.

{{"demo": "Types.js"}}

## Тема <meta data-oversett="" data-original-text="Theme">

В некоторых ситуациях вы можете не использовать компонент `Typography`. Надеемся, что вы сможете воспользоваться преимуществами [`typography`](/material-ui/customization/default-theme/?expand-path=$.typography) ключами темы.

{{"demo": "TypographyTheme.js"}}

## Изменение семантического элемента <meta data-oversett="" data-original-text="Changing the semantic element">

Компонент Typography использует свойство `variantMapping`, чтобы связать вариант пользовательского интерфейса с семантическим элементом. Важно понимать, что стиль компонента типографики не зависит от семантического базового элемента.

-   Вы можете изменить базовый элемент для разовой ситуации с помощью реквизита `component`:

```jsx
{
  /* There is already an h1 in the page, let's not duplicate it. */
}
<Typography variant="h1" component="h2">
  h1. Heading
</Typography>;
```

-   Вы можете изменить отображение [глобально с помощью темы](/material-ui/customization/theme-components/#default-props):

```js
const theme = createTheme({
  components: {
    MuiTypography: {
      defaultProps: {
        variantMapping: {
          h1: 'h2',
          h2: 'h2',
          h3: 'h2',
          h4: 'h2',
          h5: 'h2',
          h6: 'h2',
          subtitle1: 'h2',
          subtitle2: 'h2',
          body1: 'span',
          body2: 'span',
        },
      },
    },
  },
});
```

## Добавление и отключение вариантов <meta data-oversett="" data-original-text="Adding &amp; disabling variants">

Помимо использования вариантов типографики по умолчанию, вы можете добавлять собственные варианты или отключать те, которые вам не нужны. Смотрите пример [добавления и отключения вариантов](/material-ui/customization/typography/#adding-amp-disabling-variants) для получения дополнительной информации.

## Системные реквизиты <meta data-oversett="" data-original-text="System props">

Являясь полезным компонентом CSS, `Typography` поддерживает все [`system`](/system/properties/) свойства. Вы можете использовать их как prop непосредственно в компоненте. Например, margin-top:

```jsx
<Typography mt={2}>
```

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Несколько ключевых факторов, которые необходимо соблюдать для создания доступной типографики:

-   **Цвет**. Обеспечьте достаточный контраст между текстом и его фоном, ознакомьтесь с минимальным рекомендуемым [коэффициентом цветового контраста WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) (4,5:1).
-   **Размер шрифта**. Используйте [относительные единицы (rem)](/material-ui/customization/typography/#font-size), чтобы приспособиться к настройкам пользователя.
-   **Иерархия заголовков**. [Не пропускайте](https://www.w3.org/WAI/tutorials/page-structure/headings/) уровни заголовков. Чтобы решить эту проблему, необходимо отделить [семантику от стиля](#changing-the-semantic-element).
