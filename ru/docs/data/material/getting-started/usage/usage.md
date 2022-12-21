

# Использование <meta data-oversett="" data-original-text="Usage">

<p class="description">Изучите основы работы с компонентами Material UI.</p>

## Быстрый старт <meta data-oversett="" data-original-text="Quickstart">

Следующий фрагмент кода демонстрирует простое приложение, в котором используется компонент Material UI [Button](/material-ui/react-button/):

```jsx
import * as React from 'react';
import Button from '@mui/material/Button';

export default function MyApp() {
  return (
    <div>
      <Button variant="contained">Hello World</Button>
    </div>
  );
}
```

Вы можете поиграть с этим кодом в интерактивной демонстрации Code Sandbox ниже. Попробуйте изменить `variant` на кнопке на `outlined`, чтобы увидеть, как изменится стиль:

{{"demo": "Usage.js", "hideToolbar": true, "bg": true}}

## Globals <meta data-oversett="" data-original-text="Globals">

Поскольку компоненты Material UI созданы для изолированного функционирования, они не требуют глобальных стилей. Для улучшения пользовательского опыта и удобства разработчиков мы рекомендуем добавить следующие глобальные стили в ваше приложение.

### Отзывчивый метатег <meta data-oversett="" data-original-text="Responsive meta tag">

Material UI - это библиотека компонентов, ориентированная _на мобильные устройства_: сначала мы пишем код для мобильных устройств, а затем масштабируем компоненты по мере необходимости с помощью медиазапросов CSS.

Чтобы обеспечить правильное отображение и сенсорное масштабирование для всех устройств, добавьте метатег responsive viewport к элементу `<head>`:

```html
<meta name="viewport" content="initial-scale=1, width=device-width" />
```

### CssBaseline <meta data-oversett="" data-original-text="CssBaseline">

Material UI предоставляет дополнительный компонент [CssBaseline](/material-ui/react-css-baseline/). Он устраняет некоторые несоответствия в браузерах и устройствах, обеспечивая сброс настроек, которые лучше подходят для Material UI, чем альтернативные глобальные таблицы стилей, такие как [normalize.css](https://github.com/necolas/normalize.css/).

### Шрифт по умолчанию <meta data-oversett="" data-original-text="Default font">

В Material UI по умолчанию используется шрифт Roboto. Подробную информацию см. в разделе [Установка - Шрифт Roboto](/material-ui/getting-started/installation/#roboto-font).
