

# Генератор имен классов <meta data-oversett="" data-original-text="ClassName generator">

<p class="description">Настройка генерации имен классов во время сборки.</p>

Этот API представлен в `@mui/material` (v5.0.5) как замена устаревшего [`createGenerateClassName`](/system/styles/api/#creategenerateclassname-options-class-name-generator).

:::warning
Этот API находится на нестабильной стадии и может быть изменен в будущем.
:::

## Настройка <meta data-oversett="" data-original-text="Setup">

По умолчанию Material UI генерирует глобальное имя класса для каждого слота компонента. Например, `<Button>Text</Button>` генерирует html как:

```html
<button
  class="MuiButton-root MuiButton-text MuiButton-textPrimary MuiButton-sizeMedium MuiButton-textSizeMedium MuiButtonBase-root css-1ujsas3"
>
  Text
</button>
```

Чтобы настроить все имена классов, генерируемые компонентами Material UI, создайте отдельный файл javascript для использования API `ClassNameGenerator`.

```js
// create a new file called `MuiClassNameSetup.js` at the root or src folder.
import { unstable_ClassNameGenerator as ClassNameGenerator } from '@mui/material/className';

ClassNameGenerator.configure(
  // Do something with the componentName
  (componentName) => componentName,
);
```

и затем импортируйте этот файл в корень индекса перед любым импортом `@mui/*`.

```js
import './MuiClassNameSetup';
import Button from '@mui/material/Button';
// ...other component imports

function App() {
  return <Button>Text</Button>;
}
```

Вот несколько примеров настройки:

### Изменить префикс имени класса <meta data-oversett="" data-original-text="Change class name prefix">

```js
// MuiClassNameSetup.js
import { unstable_ClassNameGenerator as ClassNameGenerator } from '@mui/material/className';

ClassNameGenerator.configure((componentName) => `foo-bar-${componentName}`);
```

В результате HTML-результат изменится на следующий:

```html
<button
  class="foo-bar-MuiButton-root foo-bar-MuiButton-text foo-bar-MuiButton-textPrimary foo-bar-MuiButton-sizeMedium foo-bar-MuiButton-textSizeMedium foo-bar-MuiButtonBase-root css-1ujsas3"
>
  Button
</button>
```

### Переименовать имя класса компонента <meta data-oversett="" data-original-text="Rename component class name">

Каждый компонент Material UI имеет формат имени класса `${componentName}-${slot}`. Например, имя компонента [`Chip`](/material-ui/react-chip/) `MuiChip` , которое используется в качестве глобального имени класса для каждого элемента `<Chip />`. Вы можете удалить/изменить префикс `Mui` следующим образом:

```js
// MuiClassNameSetup.js
import { unstable_ClassNameGenerator as ClassNameGenerator } from '@mui/material/className';

ClassNameGenerator.configure((componentName) => componentName.replace('Mui', ''));
```

Теперь класс `Mui` исчез.

```html
<div
  class="Chip-root Chip-filled Chip-sizeMedium Chip-colorDefault Chip-filledDefault css-mttbc0"
>
  Chip
</div>
```

:::warning
[Классы состояний](/material-ui/customization/how-to-customize/#state-classes) не являются именами компонентов и поэтому не могут быть изменены или удалены.
:::

## Предупреждение <meta data-oversett="" data-original-text="Caveat">

-   `ClassNameGenerator.configure` должен быть вызван перед импортом компонентов Material UI.
    
-   Вы всегда должны использовать `[component]Classes` для тематизации/кастомизации, чтобы получить правильное сгенерированное имя класса.
    
    ```diff
    +import { outlinedInputClasses } from '@mui/material/OutlinedInput';
    
     const theme = createTheme({
       components: {
         MuiOutlinedInput: {
           styleOverrides: {
             root: {
    -          '& .MuiOutlinedInput-notchedOutline': {
    +          // the result will contain the prefix.
    +          [`& .${outlinedInputClasses.notchedOutline}`]: {
                 borderWidth: 1,
               }
             }
           }
         }
       }
     });
    ```
    
-   Этот API следует использовать только во время сборки.
    
-   Конфигурация применяется ко всем компонентам во всем приложении. Вы не можете нацелиться на определенную часть приложения.
    

## Примеры фреймворка <meta data-oversett="" data-original-text="Framework examples">

Всегда создавайте файл инциализатора, чтобы поднять вызов `ClassNameGenerator` на самый верх.

```js
// create a new file called `MuiClassNameSetup.js` at the root or src folder.
import { unstable_ClassNameGenerator as ClassNameGenerator } from '@mui/material/className';

ClassNameGenerator.configure(
  // Do something with the componentName
  (componentName) => componentName,
);
```

Затем импортируйте этот файл в основной источник javascript на основе фреймворка.

### Next.js <meta data-oversett="" data-original-text="Next.js">

Импортируйте инициализатор в `/pages/_app.js`.

```diff
+import './MuiClassNameSetup';
 import * as React from 'react';
 import PropTypes from 'prop-types';
 import Head from 'next/head';

 export default function MyApp(props) {
   const { Component, pageProps } = props;

   return (
     <Component {...pageProps} />
   );
 }
```

### Создание приложения React <meta data-oversett="" data-original-text="Create React App">

Импортируйте инициализатор в `/src/index.js`.

```diff
+import './MuiClassNameSetup';
 import * as React from 'react';
 import ReactDOM from 'react-dom';
 import App from './App';

 ReactDOM.render(<App />);
```

### Gatsby <meta data-oversett="" data-original-text="Gatsby">

Импортируйте инициализатор в `gatsby-ssr.js` в корневую папку.

```diff
+import './MuiClassNameSetup';

 export const wrapPageElement = ({ element }) => {
   return element;
 };
```
