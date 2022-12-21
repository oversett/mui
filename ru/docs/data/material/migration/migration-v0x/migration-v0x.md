

# Переход с v0.x на v1 <meta data-oversett="" data-original-text="Migration from v0.x to v1">

<p class="description">Да, v1 была выпущена! Воспользуйтесь преимуществами двухлетних усилий.</p>

## FAQ <meta data-oversett="" data-original-text="FAQ">

### Ух ты - API сильно изменился! Значит ли это, что 1.0 полностью изменился, мне придется изучать основы заново, а миграция будет практически невозможна? <meta data-oversett="" data-original-text="Woah - the API is way different! Does that mean 1.0 is completely different, I'll have to learn the basics all over again, and migrating will be practically impossible?">

Я рад, что вы спросили! Ответ - нет. Основные концепции не изменились. Вы заметите, что API обеспечивает большую гибкость, но это имеет свою цену - компоненты более низкого уровня, которые абстрагируют меньшую сложность.

### Что послужило причиной столь масштабных изменений? <meta data-oversett="" data-original-text="What motivated such a large change?">

Material UI был запущен [4 года назад](https://github.com/mui/material-ui/commit/28b768913b75752ecf9b6bb32766e27c241dbc46). С тех пор экосистема сильно развилась, мы тоже многому научились.[@nathanmarks](https://github.com/nathanmarks/) приступил к амбициозной задаче, перестроив Material UI с **нуля**, используя эти знания для решения давних проблем. Вот некоторые из основных изменений:

-   Новое решение для стилизации с использованием CSS-in-JS (больше возможностей для [настройки](/material-ui/customization/how-to-customize/), лучшая производительность).
-   Новая работа с темами (вложенность, самоподдерживающиеся и т.д.)
-   Молниеносная документация благодаря [Next.js](https://github.com/vercel/next.js)
-   Гораздо лучшее [покрытие тестами](/material-ui/guides/testing/) (99%+, запуск на всех основных браузерах, [визуальные регрессионные тесты](https://app.argos-ci.com/mui/material-ui/builds))
-   Полная поддержка [рендеринга на стороне сервера](/material-ui/guides/server-rendering/)
-   Широкий спектр [поддерживаемых браузеров](/material-ui/getting-started/supported-platforms/)

### С чего начать миграцию? <meta data-oversett="" data-original-text="Where should I start in a migration?">

1.  Начните с установки версии Material UI v1.x вместе с версией v0.x.

С помощью yarn:

```sh
yarn add material-ui
yarn add @material-ui/core
```

или с помощью npm:

```sh
npm install material-ui
npm install @material-ui/core
```

, затем .

```js
import FlatButton from 'material-ui/FlatButton'; // v0.x
import Button from '@material-ui/core/Button'; // v1.x
```

2.  Запустите [помощник миграции](https://github.com/mui/material-ui/tree/master/packages/mui-codemod) на вашем проекте.
3.  `MuiThemeProvider` для версии v1.x необязателен, но если у вас есть пользовательская тема, вы можете использовать версии компонента v0.x и v1.x одновременно, например, так:

```jsx
import * as React from 'react';
import { MuiThemeProvider, createMuiTheme } from '@material-ui/core/styles'; // v1.x
import { MuiThemeProvider as V0MuiThemeProvider } from 'material-ui';
import getMuiTheme from 'material-ui/styles/getMuiTheme';

const theme = createMuiTheme({
  /* theme for v1.x */
});
const themeV0 = getMuiTheme({
  /* theme for v0.x */
});

function App() {
  return (
    <MuiThemeProvider theme={theme}>
      <V0MuiThemeProvider muiTheme={themeV0}>{/*Components*/}</V0MuiThemeProvider>
    </MuiThemeProvider>
  );
}

export default App;
```

4.  После этого вы можете свободно мигрировать по одному экземпляру компонента за раз.

## Компоненты <meta data-oversett="" data-original-text="Components">

### Автозаполнение <meta data-oversett="" data-original-text="Autocomplete">

Material UI не предоставляет высокоуровневого API для решения этой проблемы. Мы рекомендуем вам изучить [решения, созданные сообществом React](/material-ui/react-autocomplete/).

В будущем мы рассмотрим возможность предоставления простого компонента для решения простых случаев использования: [#9997](https://github.com/mui/material-ui/issues/9997).

### Иконка Svg <meta data-oversett="" data-original-text="Svg Icon">

Запустите [помощник миграции](https://github.com/mui/material-ui/tree/master/packages/mui-codemod) в вашем проекте.

Это позволит применить изменения, подобные следующим:

```diff
-import AddIcon from 'material-ui/svg-icons/Add';
+import AddIcon from '@mui/icons-material/Add';

 <AddIcon />
```

### Плоская кнопка <meta data-oversett="" data-original-text="Flat Button">

```diff
-import FlatButton from 'material-ui/FlatButton';
+import Button from '@material-ui/core/Button';

-<FlatButton />
+<Button />
```

### Приподнятая кнопка <meta data-oversett="" data-original-text="Raised Button">

Путь обновления RaisedButton:

```diff
-import RaisedButton from 'material-ui/RaisedButton';
+import Button from '@material-ui/core/Button';

-<RaisedButton />
+<Button variant="contained" />
```

### Subheader <meta data-oversett="" data-original-text="Subheader">

```diff
-import Subheader from 'material-ui/Subheader';
+import ListSubheader from '@material-ui/core/ListSubheader';

-<Subheader>Sub Heading</Subheader>
+<ListSubheader>Sub Heading</ListSubheader>
```

### Переключение <meta data-oversett="" data-original-text="Toggle">

```diff
-import Toggle from 'material-ui/Toggle';
+import Switch from '@material-ui/core/Switch';

-<Toggle
-  toggled={this.state.checkedA}
-  onToggle={this.handleToggle}
-/>
+<Switch
+  checked={this.state.checkedA}
+  onChange={this.handleSwitch}
+/>
```

### Пункт меню <meta data-oversett="" data-original-text="Menu Item">

```diff
-import MenuItem from 'material-ui/MenuItem';
+import MenuItem from '@material-ui/core/MenuItem';

-<MenuItem primaryText="Profile" />
+<MenuItem>Profile</MenuItem>
```

### Иконка шрифта <meta data-oversett="" data-original-text="Font Icon">

```diff
-import FontIcon from 'material-ui/FontIcon';
+import Icon from '@material-ui/core/Icon';

-<FontIcon>home</FontIcon>
+<Icon>home</Icon>
```

### Круговой прогресс <meta data-oversett="" data-original-text="Circular Progress">

```diff
-import CircularProgress from 'material-ui/CircularProgress';
+import CircularProgress from '@material-ui/core/CircularProgress';

-<CircularProgress mode="indeterminate" />
+<CircularProgress variant="indeterminate" />
```

### Выпадающее меню <meta data-oversett="" data-original-text="Drop Down Menu">

```diff
-import DropDownMenu from 'material-ui/DropDownMenu';
+import Select from '@material-ui/core/Select';

-<DropDownMenu></DropDownMenu>
+<Select value={this.state.value}></Select>
```

### Продолжение следует... <meta data-oversett="" data-original-text="To be continued…">

Вы успешно мигрировали свое приложение и хотите помочь сообществу? Существует открытый вопрос для завершения этого руководства по миграции [#7195](https://github.com/mui/material-ui/issues/7195). Любой запрос на исправление приветствуется 😊.
