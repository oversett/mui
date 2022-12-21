---
product: material-ui
title: Image List React component
components: ImageList, ImageListItem, ImageListItemBar
materialDesign: https://m2.material.io/components/image-lists
githubLabel: 'component: image list'
---

# Список изображений <meta data-oversett="" data-original-text="Image List">

<p class="description">Список изображений отображает коллекцию изображений в виде упорядоченной сетки.</p>

Списки изображений представляют собой набор элементов в повторяющемся виде. Они помогают улучшить визуальное восприятие содержимого, которое в них содержится.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Стандартный список изображений <meta data-oversett="" data-original-text="Standard image list">

Стандартные списки изображений лучше всего подходят для элементов одинаковой важности. Они имеют единый размер контейнера, соотношение и расстояние между ними.

{{"demo": "StandardImageList.js"}}

## Ватные списки изображений <meta data-oversett="" data-original-text="Quilted image list">

Ватные списки изображений подчеркивают преимущество одних элементов над другими в коллекции. Они создают иерархию, используя различные размеры контейнеров и соотношение между ними.

{{"demo": "QuiltedImageList.js"}}

## Плетеный список изображений <meta data-oversett="" data-original-text="Woven image list">

Плетеные списки изображений используют чередование соотношений контейнеров для создания ритмичной компоновки. Плетеный список изображений лучше всего подходит для просмотра однорангового контента.

{{"demo": "WovenImageList.js"}}

## Список изображений с каменной кладкой <meta data-oversett="" data-original-text="Masonry image list">

В списках изображений Masonry используются динамически изменяемые размеры высоты контейнеров, которые отражают соотношение сторон каждого изображения. Этот список изображений лучше всего подходит для просмотра необрезанного содержимого сверстников.

{{"demo": "MasonryImageList.js"}}

## Список изображений с полосами заголовков <meta data-oversett="" data-original-text="Image list with title bars">

Этот пример демонстрирует использование `ImageListItemBar` для добавления накладки к каждому элементу. Накладка может содержать `title`, `subtitle` и вторичное действие - в данном примере `IconButton`.

{{"demo": "TitlebarImageList.js"}}

### Строка заголовка под изображением (стандарт) <meta data-oversett="" data-original-text="Title bar below image (standard)">

Строка заголовка может быть размещена под изображением.

{{"demo": "TitlebarBelowImageList.js"}}

### Строка заголовка под изображением (кирпичная кладка) <meta data-oversett="" data-original-text="Title bar below image (masonry)">

{{"demo": "TitlebarBelowMasonryImageList.js"}}

## Пользовательский список изображений <meta data-oversett="" data-original-text="Custom image list">

В этом примере элементы имеют настроенную панель заголовка, расположенную сверху и с настроенным градиентом `titleBackground`. Вторичное действие `IconButton` расположено слева. Реквизит `gap` используется для настройки промежутка между элементами.

{{"demo": "CustomImageList.js", "defaultCodeOpen": false}}
