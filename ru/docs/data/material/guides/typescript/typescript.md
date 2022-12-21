

# TypeScript <meta data-oversett="" data-original-text="TypeScript">

<p class="description">Благодаря TypeScript вы можете добавить статическую типизацию в JavaScript для повышения производительности разработчиков и качества кода.</p>

## Минимальная конфигурация <meta data-oversett="" data-original-text="Minimum configuration">

Для работы MUI требуется минимальная версия TypeScript 3.5. Посмотрите пример " [Создание приложения React с TypeScript](https://github.com/mui/material-ui/tree/master/examples/create-react-app-with-typescript) ".

Для работы типов рекомендуется, чтобы в вашем `tsconfig.json` были включены как минимум следующие опции:

```json
{
  "compilerOptions": {
    "lib": ["es6", "dom"],
    "noImplicitAny": true,
    "noImplicitThis": true,
    "strictNullChecks": true
  }
}
```

Опции строгого режима - это те же опции, которые требуются для каждого пакета types, опубликованного в пространстве имен `@types/`. Использование менее строгого `tsconfig.json` или пропуск некоторых библиотек может привести к ошибкам. Для получения наилучшего опыта работы с типами мы рекомендуем установить `"strict": true`.

## Работа с `value` и обработчиками событий <meta data-oversett="" data-original-text="Handling value and event handlers">

Многие компоненты, работающие с пользовательским вводом, предлагают реквизит `value` или обработчики событий, включающие текущий `value`. В большинстве ситуаций этот `value` обрабатывается только в React, который позволяет ему быть любого типа, например, объекты или массивы.

Однако этот тип не может быть проверен во время компиляции в ситуациях, когда он зависит от дочерних компонентов, например, для `Select` или `RadioGroup`. Это означает, что самым разумным вариантом будет ввести его как `unknown` и предоставить разработчику решать, как он хочет сузить этот тип. Мы не предлагаем возможность использовать общий тип в этих случаях по тем [же причинам, по которым `event.target` не является общим в React](https://github.com/DefinitelyTyped/DefinitelyTyped/issues/11508#issuecomment-256045682).

Демонстрационные примеры включают типизированные варианты, использующие приведение типов. Это приемлемый компромисс, поскольку все типы находятся в одном файле и являются очень базовыми. Вы должны решить для себя, приемлем ли для вас такой же компромисс. Типы библиотеки строгие по умолчанию и свободные по желанию.

## Настройка `Theme` <meta data-oversett="" data-original-text="Customization of Theme">

Перемещено в [/customization/theming/#custom-variables](/material-ui/customization/theming/#custom-variables).

## Сложности с реквизитом `component` <meta data-oversett="" data-original-text="Complications with the component prop">

Из-за некоторых ограничений TypeScript использование реквизита `component` может быть проблематичным, если вы создаете свой собственный компонент на основе компонентов Material UI. Для композиции компонентов вам, скорее всего, придется использовать один из этих двух вариантов:

1.  Обернуть компонент Material UI, чтобы усилить его.
2.  Использовать утилиту `styled()` для настройки стилей компонента.

Если вы используете первый вариант, ознакомьтесь с [руководством по композиции](/material-ui/guides/composition/#with-typescript) для получения более подробной информации.

Если вы используете утилиту `styled()` (независимо от того, откуда она взята - из `@mui/material` или `@emotion/styled`), вам нужно будет оформить полученный компонент, как показано ниже:

```tsx
import Button from '@mui/material/Button';
import { styled } from '@mui/material/styles';

const CustomButton = styled(Button)({
  // your custom styles go here
}) as typeof Button;
```
