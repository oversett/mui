---
product: material-ui
title: React Avatar component
components: Avatar, AvatarGroup, Badge
githubLabel: 'component: avatar'
---

# Аватар <meta data-oversett="" data-original-text="Avatar">

<p class="description">Аватары встречаются во всем материальном дизайне, их используют во всем, от таблиц до диалоговых меню.</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Аватары изображений <meta data-oversett="" data-original-text="Image avatars">

Аватары изображений можно создать, передав компоненту стандартные реквизиты `img` `src` или `srcSet`.

{{"demo": "ImageAvatars.js"}}

## Буквенные аватары <meta data-oversett="" data-original-text="Letter avatars">

Аватары, содержащие простые символы, могут быть созданы путем передачи строки `children`.

{{"demo": "LetterAvatars.js"}}

Вы можете использовать различные цвета фона для аватара. Следующий демонстрационный пример генерирует цвет на основе имени человека.

{{"demo": "BackgroundLetterAvatars.js"}}

## Размеры <meta data-oversett="" data-original-text="Sizes">

Вы можете изменить размер аватара с помощью свойств `height` и `width` CSS.

{{"demo": "SizeAvatars.js"}}

## Аватары-иконки <meta data-oversett="" data-original-text="Icon avatars">

Аватары в виде иконок создаются путем передачи иконки в качестве `children`.

{{"demo": "IconAvatars.js"}}

## Варианты <meta data-oversett="" data-original-text="Variants">

Если вам нужны квадратные или округлые аватары, используйте свойство `variant`.

{{"demo": "VariantAvatars.js"}}

## Обратные действия <meta data-oversett="" data-original-text="Fallbacks">

Если при загрузке изображения аватара произошла ошибка, компонент переходит к альтернативному варианту в следующем порядке:

-   предоставленные дочерние элементы
-   первая буква текста `alt`
-   общий значок аватара

{{"demo": "FallbackAvatars.js"}}

## Сгруппированный <meta data-oversett="" data-original-text="Grouped">

`AvatarGroup` отображает дочерние элементы в виде стопки. Используйте параметр `max`, чтобы ограничить количество аватаров.

{{"demo": "GroupAvatars.js"}}

### Общее количество аватаров <meta data-oversett="" data-original-text="Total avatars">

Если вам нужно контролировать общее количество не показанных аватаров, вы можете использовать реквизит `total`.

{{"demo": "TotalAvatars.js"}}

## Со значком <meta data-oversett="" data-original-text="With badge">

{{"demo": "BadgeAvatars.js"}}
