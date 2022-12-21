---
product: material-ui
title: React Rating component
components: Rating
githubLabel: 'component: rating'
waiAria: https://www.w3.org/WAI/tutorials/forms/custom-controls/#a-star-rating
---

# Рейтинг <meta data-oversett="" data-original-text="Rating">

<p class="description">Рейтинги дают представление о мнениях и опыте других людей, а также позволяют пользователю выставить собственную оценку.</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовый рейтинг <meta data-oversett="" data-original-text="Basic rating">

{{"demo": "BasicRating.js"}}

## Точность рейтинга <meta data-oversett="" data-original-text="Rating precision">

Рейтинг может отображать любое плавающее число с помощью реквизита `value`. Используйте реквизит `precision`, чтобы определить минимально допустимое изменение значения инкремента.

{{"demo": "HalfRating.js"}}

## Обратная связь при наведении <meta data-oversett="" data-original-text="Hover feedback">

Вы можете отображать метку при наведении, чтобы помочь пользователю выбрать правильное значение рейтинга. В демонстрационном примере используется реквизит `onChangeActive`.

{{"demo": "HoverRating.js"}}

## Размеры <meta data-oversett="" data-original-text="Sizes">

Для увеличения или уменьшения размера рейтинга используйте реквизит `size`.

{{"demo": "RatingSize.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Более подробно об этом можно узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedRating.js"}}

## Радиогруппа <meta data-oversett="" data-original-text="Radio group">

Рейтинг реализован с помощью радиогруппы, установите `highlightSelectedOnly`, чтобы восстановить естественное поведение.

{{"demo": "RadioGroupRating.js"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

[(Учебник WAI](https://www.w3.org/WAI/tutorials/forms/custom-controls/#a-star-rating))

Доступность этого компонента зависит от:

-   Радиогруппа, поля которой визуально скрыты. Она содержит шесть радиокнопок, по одной для каждой звезды, и еще одну для 0 звезд, которая отмечена по умолчанию. Обязательно укажите значение для параметра `name`, уникальное для родительской формы.
-   Ярлыки для радиокнопок содержат фактический текст ("1 звезда", "2 звезды", ...). Обязательно предоставьте подходящую функцию для реквизита `getLabelText`, если страница не на английском языке. Вы можете использовать [включенные локали](https://mui.com/material-ui/guides/localization/) или создать свои собственные.
-   Визуально отличимый внешний вид для иконок рейтинга. По умолчанию компонент рейтинга использует различие цвета и формы (заполненные и пустые иконки) для обозначения значения. В том случае, если вы используете цвет как единственное средство для указания значения, информация должна также отображаться в виде текста, как в этом демо-ролике. Это важно для соответствия [Критерию успеха 1.4.1](https://www.w3.org/TR/WCAG21/#use-of-color) стандарта WCAG2.1.

{{"demo": "TextRating.js"}}

### ARIA <meta data-oversett="" data-original-text="ARIA">

Рейтинг, доступный только для чтения, имеет роль "img" и метку aria, которая описывает отображаемый рейтинг.

### Клавиатура <meta data-oversett="" data-original-text="Keyboard">

Поскольку в компоненте рейтинга используются радиокнопки, взаимодействие с клавиатурой соответствует поведению родного браузера. Клавиша Tab фокусирует текущий рейтинг, а клавиши курсора управляют выбранным рейтингом.

Рейтинг, доступный только для чтения, не фокусируется.
