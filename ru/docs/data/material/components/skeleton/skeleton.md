---
product: material-ui
title: React Skeleton component
components: Skeleton
githubLabel: 'component: skeleton'
---

# Скелет <meta data-oversett="" data-original-text="Skeleton">

<p class="description">Отображение предварительного просмотра содержимого перед загрузкой данных для уменьшения раздражения при загрузке.</p>

Данные для ваших компонентов могут быть доступны не сразу. Вы можете улучшить воспринимаемую отзывчивость страницы, используя скелеты. Создается впечатление, что все происходит немедленно, а затем информация постепенно отображается на экране (ср. " [Избегайте спиннера](https://www.lukew.com/ff/entry.asp?1797)").

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Использование <meta data-oversett="" data-original-text="Usage">

Компонент предназначен для использования **непосредственно в ваших компонентах**. Например:

```jsx
{
  item ? (
    <img
      style={{
        width: 210,
        height: 118,
      }}
      alt={item.title}
      src={item.src}
    />
  ) : (
    <Skeleton variant="rectangular" width={210} height={118} />
  );
}
```

## Варианты <meta data-oversett="" data-original-text="Variants">

Компонент поддерживает 4 варианта формы:

-   `text` (по умолчанию): представляет собой одну строку текста (вы можете настроить высоту через размер шрифта).
-   `circular`, `rectangular`, и `rounded`: имеют разный радиус границы, что позволяет вам контролировать размер.

{{"demo": "Variants.js"}}

## Анимации <meta data-oversett="" data-original-text="Animations">

По умолчанию скелет пульсирует, но вы можете изменить анимацию на волну или полностью отключить ее.

{{"demo": "Animations.js"}}

### Пример пульсации <meta data-oversett="" data-original-text="Pulsate example">

{{"demo": "YouTube.js", "defaultCodeOpen": false}}

### Пример волны <meta data-oversett="" data-original-text="Wave example">

{{"demo": "Facebook.js", "defaultCodeOpen": false, "bg": true}}

## Определение размеров <meta data-oversett="" data-original-text="Inferring dimensions">

Помимо приема реквизитов `width` и `height`, компонент также может определять размеры.

Это хорошо работает, когда речь идет о типографике, поскольку ее высота задается с помощью единиц `em`.

```jsx
<Typography variant="h1">{loading ? <Skeleton /> : 'h1'}</Typography>
```

{{"demo": "SkeletonTypography.js", "defaultCodeOpen": false}}

Но когда речь идет о других компонентах, вы можете не захотеть повторять ширину и высоту. В таких случаях можно передать `children`, и компонент сам определит ширину и высоту.

```jsx
loading ? (
  <Skeleton variant="circular">
    <Avatar />
  </Skeleton>
) : (
  <Avatar src={data.avatar} />
);
```

{{"demo": "SkeletonChildren.js", "defaultCodeOpen": false}}

## Цвет <meta data-oversett="" data-original-text="Color">

Цвет компонента можно настроить, изменив его CSS-свойство `background-color`. Это особенно полезно на черном фоне (иначе скелет будет невидим).

{{"demo": "SkeletonColor.js", "bg": "inline"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Скелетные экраны представляют собой альтернативу традиционному методу спиннера. Вместо того чтобы показывать абстрактный виджет, скелетные экраны создают предвкушение того, что будет дальше, и снижают когнитивную нагрузку.

Цвет фона скелета использует наименьшее количество яркости, чтобы быть видимым в хороших условиях (хорошее окружающее освещение, хороший экран, отсутствие нарушений зрения).

### ARIA <meta data-oversett="" data-original-text="ARIA">

Нет.

### Клавиатура <meta data-oversett="" data-original-text="Keyboard">

Скелет не фокусируется.
