---
product: material-ui
title: Bottom Navigation React component
components: BottomNavigation, BottomNavigationAction
githubLabel: 'component: bottom navigation'
materialDesign: https://m2.material.io/components/bottom-navigation
---

# Нижняя навигация <meta data-oversett="" data-original-text="Bottom Navigation">

<p class="description">Нижняя навигационная панель позволяет перемещаться между основными пунктами назначения в приложении.</p>

Нижние навигационные панели отображают от трех до пяти пунктов назначения в нижней части экрана. Каждый пункт назначения представлен значком и дополнительной текстовой надписью. При нажатии на значок нижней навигационной панели пользователь переходит к пункту назначения верхнего уровня, связанному с этим значком.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Нижняя навигация <meta data-oversett="" data-original-text="Bottom navigation">

Когда есть только **три** действия, всегда отображайте и значки, и текстовые метки.

{{"demo": "SimpleBottomNavigation.js", "bg": true}}

## Нижняя навигация без ярлыка <meta data-oversett="" data-original-text="Bottom navigation with no label">

При наличии **четырех** или **пяти** действий отображайте неактивные представления только в виде значков.

{{"demo": "LabelBottomNavigation.js", "bg": true}}

## Фиксированное позиционирование <meta data-oversett="" data-original-text="Fixed positioning">

В этом демо нижняя навигация фиксируется внизу, независимо от количества контента на экране.

{{"demo": "FixedBottomNavigation.js", "bg": true, "iframe": true, "maxWidth": 600}}

## Библиотека маршрутизации сторонних производителей <meta data-oversett="" data-original-text="Third-party routing library">

Одним из частых случаев использования является выполнение навигации только на клиенте, без HTTP-трипа на сервер. Компонент `BottomNavigationAction` предоставляет реквизит `component` для обработки этого случая использования. Здесь представлено [более подробное руководство](/material-ui/guides/routing/).
