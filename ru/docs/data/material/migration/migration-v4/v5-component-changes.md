

# Ломающие изменения в v5, часть вторая: основные компоненты <meta data-oversett="" data-original-text="Breaking changes in v5, part two: core components">

<p class="description">Это справочное руководство по всем изменениям, внесенным в Material v5, и по тому, как с ними обращаться при переходе с v4. В этой части рассматриваются изменения в компонентах.</p>

## Миграция Material UI v5 <meta data-oversett="" data-original-text="Material UI v5 migration">

1.  [Начало работы](/material-ui/migration/migration-v4/)
2.  [Ломающие изменения, часть первая: стиль и тема](/material-ui/migration/v5-style-changes/)
3.  Ломающие изменения, часть вторая: компоненты 👈 _Вы здесь_
4.  [Миграция с JSS](/material-ui/migration/migrating-from-jss/)
5.  [Устранение неполадок](/material-ui/migration/troubleshooting/)

## Разрывные изменения, часть вторая <meta data-oversett="" data-original-text="Breaking changes, part two">

В Material UI v5 внесен ряд изменений по сравнению с v4. Многие из этих изменений можно устранить автоматически с помощью [кодмодов](/material-ui/migration/migration-v4/#run-codemods), описанных в [главном руководстве по миграции](/material-ui/migration/migration-v4/).

В следующем документе перечислены все изменения, связанные с компонентами в v5, и способы их устранения.

Если вы еще не сделали этого, пожалуйста, обязательно ознакомьтесь с [первой частью "Ломающие изменения в v5: стили и темы](/material-ui/migration/v5-style-changes/) ", чтобы продолжить процесс миграции.

:::warning
Изменения, которые обрабатываются кодмодами, обозначаются символом ✅ в оглавлении в правой части экрана.

Если вы уже следовали инструкциям основного руководства по миграции и запустили кодовые модули, то вам не нужно предпринимать никаких дополнительных действий по этим пунктам.

Все остальные изменения должны быть выполнены вручную.
:::

Поскольку основные компоненты используют Emotion в качестве движка стилей, реквизиты, используемые Emotion, не перехватываются. Реквизит `as` в следующем фрагменте кода не будет передан на `SomeOtherComponent`.

```jsx
<MuiComponent component={SomeOtherComponent} as="button" />
```

## AppBar <meta data-oversett="" data-original-text="AppBar">

### Исправление проблем с z-индексом <meta data-oversett="" data-original-text="Fix z-index issues">

Удалите z-индекс при статическом и относительном положении. Это позволяет избежать создания контекста суммирования и проблем с рендерингом.

### Замена реквизита цвета для темного режима <meta data-oversett="" data-original-text="Replace color prop for dark mode">

Реквизит `color` больше не имеет эффекта в темном режиме. Панель приложения использует фоновый цвет, требуемый повышением, чтобы следовать [рекомендациям Material Design](https://m2.material.io/design/color/dark-theme.html). Используйте `enableColorOnDark`, чтобы восстановить поведение v4.

```jsx
<AppBar enableColorOnDark />
```

## Предупреждение <meta data-oversett="" data-original-text="Alert">

### ✅ Обновить импорт <meta data-oversett="" data-original-text="✅ Update import">

Переместите компонент из лаборатории в ядро. Компонент теперь стабилен.

```diff
-import Alert from '@mui/lab/Alert';
-import AlertTitle from '@mui/lab/AlertTitle';
+import Alert from '@mui/material/Alert';
+import AlertTitle from '@mui/material/AlertTitle';
```

## Автозаполнение <meta data-oversett="" data-original-text="Autocomplete">

### ✅ Обновить импорт <meta data-oversett="" data-original-text="✅ Update import">

Переместите компонент из лаборатории в ядро. Компонент теперь стабилен.

```diff
-import Autocomplete from '@mui/lab/Autocomplete';
-import useAutocomplete  from '@mui/lab/useAutocomplete';
+import Autocomplete from '@mui/material/Autocomplete';
+import useAutoComplete from '@mui/material/useAutocomplete';
```

### Удалить реквизит отладки <meta data-oversett="" data-original-text="Remove debug prop">

Удалите `debug` prop. Есть несколько более простых альтернатив: `open={true}`, Chrome devtools ["Emulate focused"](https://twitter.com/sulco/status/1305841873945272321), или React devtools prop setter.

### Обновить `renderOption` <meta data-oversett="" data-original-text="Update renderOption">

`renderOption` теперь должно возвращать полную DOM-структуру опции. Это упрощает настройку. Вы можете восстановить изменение с помощью:

```diff
 <Autocomplete
-  renderOption={(option, { selected }) => (
-    <React.Fragment>
+  renderOption={(props, option, { selected }) => (
+    <li {...props}>
       <Checkbox
         icon={icon}
         checkedIcon={checkedIcon}
         style={{ marginRight: 8 }}
         checked={selected}
       />
       {option.title}
-    </React.Fragment>
+    </li>
   )}
 />
```

### ✅ Переименуйте `closeIcon` в `clearIcon`. <meta data-oversett="" data-original-text="✅ Rename closeIcon to clearIcon">

Переименуйте `closeIcon` prop в `clearIcon`, чтобы избежать путаницы.

```diff
-<Autocomplete closeIcon={defaultClearIcon} />
+<Autocomplete clearIcon={defaultClearIcon} />
```

### Переименование аргументов причины <meta data-oversett="" data-original-text="Rename reason arguments">

Следующие значения аргумента reason в `onChange` и `onClose` были переименованы для согласованности:

1.  `create-option` на `createOption`
2.  `select-option` на `selectOption`
3.  `remove-option` к `removeOption`

Измените правила CSS, использующие `[data-focus="true"]`, на `.Mui-focused`. Атрибут `data-focus` больше не устанавливается на сфокусированной опции; вместо этого используются глобальные имена классов.

```diff
-'.MuiAutocomplete-option[data-focus="true"]': {
+'.MuiAutocomplete-option.Mui-focused': {
```

### ✅ Переименовать getOptionSelected <meta data-oversett="" data-original-text="✅ Rename getOptionSelected">

Переименуйте `getOptionSelected` в `isOptionEqualToValue`, чтобы лучше описать его назначение.

```diff
 <Autocomplete
-  getOptionSelected={(option, value) => option.title === value.title}
+  isOptionEqualToValue={(option, value) => option.title === value.title}
```

## Аватар <meta data-oversett="" data-original-text="Avatar">

### ✅ Переименовать круг <meta data-oversett="" data-original-text="✅ Rename circle">

Переименуйте `circle` в `circular` для согласованности:

```diff
-<Avatar variant="circle">
-<Avatar classes={{ circle: 'className' }}>
+<Avatar variant="circular">
+<Avatar classes={{ circular: 'className' }}>
```

Поскольку `circular` является значением по умолчанию, реквизит варианта может быть удален:

```diff
-<Avatar variant="circle">
+<Avatar>
```

### ✅ Обновить импорт AvatarGroup <meta data-oversett="" data-original-text="✅ Update AvatarGroup import">

Переместите AvatarGroup из лаборатории в ядро.

```diff
-import AvatarGroup from '@mui/lab/AvatarGroup';
+import AvatarGroup from '@mui/material/AvatarGroup';
```

## Значок <meta data-oversett="" data-original-text="Badge">

### ✅ Переименовать круг и прямоугольник <meta data-oversett="" data-original-text="✅ Rename circle and rectangle">

Переименуйте `circle` в `circular` и `rectangle` в `rectangular` для согласованности.

```diff
-<Badge overlap="circle">
-<Badge overlap="rectangle">
+<Badge overlap="circular">
+<Badge overlap="rectangular">
```

```diff
 <Badge classes={{
-  anchorOriginTopRightRectangle: 'className',
-  anchorOriginBottomRightRectangle: 'className',
-  anchorOriginTopLeftRectangle: 'className',
-  anchorOriginBottomLeftRectangle: 'className',
-  anchorOriginTopRightCircle: 'className',
-  anchorOriginBottomRightCircle: 'className',
-  anchorOriginTopLeftCircle: 'className',
+  anchorOriginTopRightRectangular: 'className',
+  anchorOriginBottomRightRectangular: 'className',
+  anchorOriginTopLeftRectangular: 'className',
+  anchorOriginBottomLeftRectangular: 'className',
+  anchorOriginTopRightCircular: 'className',
+  anchorOriginBottomRightCircular: 'className',
+  anchorOriginTopLeftCircular: 'className',
 }}>
```

## BottomNavigation <meta data-oversett="" data-original-text="BottomNavigation">

### Обновление типа события (TypeScript) <meta data-oversett="" data-original-text="Update event type (TypeScript)">

Событие `event` в `onChange` теперь набирается как `React.SyntheticEvent`, а не как `React.ChangeEvent`.

```diff
-<BottomNavigation onChange={(event: React.ChangeEvent<{}>) => {}} />
+<BottomNavigation onChange={(event: React.SyntheticEvent) => {}} />
```

## BottomNavigationAction <meta data-oversett="" data-original-text="BottomNavigationAction">

### Удалить разворот и обертку <meta data-oversett="" data-original-text="Remove span and wrapper">

Удалите элемент `span`, который обертывает дочерние элементы. Удалите также `wrapper` classKey.

Более подробную информацию об этом изменении вы можете найти в [этом запросе на GitHub](https://github.com/mui/material-ui/pull/26923).

```diff
 <button class="MuiBottomNavigationAction-root">
-  <span class="MuiBottomNavigationAction-wrapper">
     {icon}
     <span class="MuiBottomNavigationAction-label">
       {label}
     </span>
-  </span>
 </button>
```

## Вставка <meta data-oversett="" data-original-text="Box">

### ✅ Обновление значения параметра borderRadius <meta data-oversett="" data-original-text="✅ Update borderRadius prop value">

Преобразование значения реквизита системы `borderRadius` было изменено.

Если оно получает число, оно умножает это значение на значение `theme.shape.borderRadius`.

Используйте строку, чтобы указать явное значение px.

```diff
-<Box borderRadius="borderRadius">
+<Box borderRadius={1}>
```

```diff
-<Box borderRadius={16}>
+<Box borderRadius="16px">
```

### ✅ Применение API sx <meta data-oversett="" data-original-text="✅ Apply sx API">

Системные реквизиты Box имеют альтернативный API в v5, использующий реквизит `sx`.

Обратитесь к документации по системе, чтобы узнать больше о [преимуществах этого API](/system/getting-started/usage/#api-tradeoff).

```jsx
<Box border="1px dashed grey" p={[2, 3, 4]} m={2}>
<Box sx={{ border: "1px dashed grey", p: [2, 3, 4], m: 2 }}>
```

### ✅ Переименование свойств CSS <meta data-oversett="" data-original-text="✅ Rename CSS properties">

Следующие свойства были переименованы, поскольку спецификация CSS считает их устаревшими свойствами CSS:

1.  `gridGap` на `gap`
2.  `gridColumnGap` to `columnGap`
3.  `gridRowGap` к `rowGap`

```diff
-<Box gridGap={1}>
-<Box gridColumnGap={2}>
-<Box gridRowGap={3}>
+<Box gap={1}>
+<Box columnGap={2}>
+<Box rowGap={3}>
```

:::info
Функция системной сетки не была документирована в v4.
:::

### Удалить свойство clone <meta data-oversett="" data-original-text="Remove clone prop">

Реквизит `clone` был удален, поскольку его поведение может быть получено путем применения реквизита `sx` непосредственно к дочернему компоненту, если это компонент Material UI.

```diff
-<Box sx={{ border: '1px dashed grey' }} clone>
-  <Button>Save</Button>
-</Box>
+<Button sx={{ border: '1px dashed grey' }}>Save</Button>
```

### Замените реквизит render на `sx`. <meta data-oversett="" data-original-text="Replace render prop with sx">

Возможность передавать render prop была удалена, поскольку ее поведение можно получить, применив `sx` prop непосредственно к дочернему компоненту, если это компонент Material UI.

```diff
-<Box sx={{ border: '1px dashed grey' }}>
-  {(props) => <Button {...props}>Save</Button>}
-</Box>
+<Button sx={{ border: '1px dashed grey' }}>Save</Button>
```

Для нематериальных компонентов пользовательского интерфейса используйте реквизит `component`.

```diff
-<Box sx={{ border: '1px dashed grey' }}>
-  {(props) => <button {...props}>Save</button>}
-</Box>
+<Box component="button" sx={{ border: '1px dashed grey' }}>Save</Box>
```

## Кнопка <meta data-oversett="" data-original-text="Button">

### ✅ Удаление реквизита цвета по умолчанию <meta data-oversett="" data-original-text="✅ Remove default color prop">

Реквизит кнопки `color` теперь "primary" по умолчанию, а "default" был удален. Это приближает кнопку к рекомендациям Material Design и упрощает API.

```diff
-<Button color="default">
+<Button>
```

:::info
Если вы предпочитаете использовать цвет `default` в v4, посмотрите [демо CodeSandbox](https://codesandbox.io/s/mimic-v4-button-default-color-bklx8?file=/src/Demo.tsx), чтобы увидеть, как это работает в v5.
:::

### Удалите span и label <meta data-oversett="" data-original-text="Remove span and label">

Элемент `span`, обертывающий дочерние элементы, был удален. `label` classKey также удален.

Подробнее об этом изменении вы можете узнать в [этом запросе на GitHub](https://github.com/mui/material-ui/pull/26666), оно было необходимо для iOS.

```diff
 <button class="MuiButton-root">
-  <span class="MuiButton-label">
     children
-  </span>
 </button>
```

## Фишка <meta data-oversett="" data-original-text="Chip">

### ✅ Переименовать default в filled <meta data-oversett="" data-original-text="✅ Rename default to filled">

Переименуйте вариант `default` в `filled` для согласованности.

Поскольку `filled` является значением по умолчанию, параметр variant можно удалить:

```diff
-<Chip variant="default">
+<Chip>
```

## Флажок <meta data-oversett="" data-original-text="Checkbox">

### По умолчанию установлен на "primary" <meta data-oversett="" data-original-text="Set to &quot;primary&quot; by default">

Цвет флажка теперь по умолчанию "первичный". Чтобы продолжать использовать "вторичный" цвет, необходимо явно указать `secondary`. Это приближает флажок к рекомендациям Material Design.

```diff
-<Checkbox />
+<Checkbox color="secondary" />
```

### Обновление имен классов CSS <meta data-oversett="" data-original-text="Update CSS class names">

Компонент больше не имеет имен классов `.MuiIconButton-root` и `.MuiIconButton-label`.

Вместо них используйте `.MuiButtonBase-root`.

```diff
-<span class="MuiIconButton-root MuiButtonBase-root MuiCheckbox-root PrivateSwitchBase-root">
-  <span class="MuiIconButton-label">
-    <input class="PrivateSwitchBase-input">
+<span class="MuiButtonBase-root MuiCheckbox-root PrivateSwitchBase-root">
+  <span class="PrivateSwitchBase-input">
```

## CircularProgress <meta data-oversett="" data-original-text="CircularProgress">

### ✅ Переименовать static в determinate <meta data-oversett="" data-original-text="✅ Rename static to determinate">

Вариант `static` был переименован в `determinate`, а предыдущий вид `determinate` был заменен на `static`.

Это было исключением из Material Design и было удалено из спецификации.

```diff
-<CircularProgress variant="static" classes={{ static: 'className' }} />
+<CircularProgress variant="determinate" classes={{ determinate: 'className' }} />
```

:::error
Если вы ранее настраивали `determinate`, то ваши настройки, скорее всего, больше не действительны. Пожалуйста, удалите их.
:::

## Свернуть <meta data-oversett="" data-original-text="Collapse">

### ✅ Переименование реквизита collapsedHeight <meta data-oversett="" data-original-text="✅ Rename collapsedHeight prop">

Реквизит `collapsedHeight` был переименован в `collapsedSize` для поддержки горизонтального направления.

```diff
-<Collapse collapsedHeight={40}>
+<Collapse collapsedSize={40}>
```

Ключ `classes.container` был изменен, чтобы соответствовать соглашению других компонентов.

```diff
-<Collapse classes={{ container: 'collapse' }}>
+<Collapse classes={{ root: 'collapse' }}>
```

## CssBaseline <meta data-oversett="" data-original-text="CssBaseline">

### Обновление styled-engine <meta data-oversett="" data-original-text="Update styled-engine">

Компонент был переведен на использование `@mui/styled-engine` (`emotion` или `styled-components`) вместо `jss`.

Вы должны удалить ключ `@global` при определении переопределений стиля для него. Вы также можете начать использовать синтаксис шаблонов CSS вместо синтаксиса объектов JavaScript.

```diff
 const theme = createTheme({
   components: {
     MuiCssBaseline: {
-      styleOverrides: {
-        '@global': {
-          html: {
-            WebkitFontSmoothing: 'auto',
-          },
-        },
-      },
+      styleOverrides: `
+        html {
+          -webkit-font-smoothing: auto;
+        }
+      `
     },
   },
 });
```

### Обновление размера шрифта тела <meta data-oversett="" data-original-text="Update body font size">

Размер шрифта `body` изменился с `theme.typography.body2` (`0.875rem`) на `theme.typography.body1` (`1rem`). Чтобы вернуться к предыдущему размеру, вы можете переопределить его в теме:

```js
const theme = createMuiTheme({
  components: {
    MuiCssBaseline: {
      styleOverrides: {
        body: {
          fontSize: '0.875rem',
          lineHeight: 1.43,
          letterSpacing: '0.01071em',
        },
      },
    },
  },
});
```

## Dialog <meta data-oversett="" data-original-text="Dialog">

### ✅ Обновление реквизитов перехода <meta data-oversett="" data-original-text="✅ Update transition props">

Реквизит перехода `on*` был удален. Вместо него используйте `TransitionProps`.

```diff
  <Dialog
-  onEnter={onEnter}
-  onEntered={onEntered}
-  onEntering={onEntering}
-  onExit={onExit}
-  onExited={onExited}
-  onExiting={onExiting}
+  TransitionProps={{
+    onEnter,
+    onEntered,
+    onEntering,
+    onExit,
+    onExited,
+    onExiting,
+  }}
  >
```

### ✅ Удалить реквизит disableBackdropClick <meta data-oversett="" data-original-text="✅ Remove disableBackdropClick prop">

Удалите реквизит `disableBackdropClick`, поскольку он является избыточным.

Игнорируйте события закрытия из `onClose`, используя вместо этого `reason === 'backdropClick'`.

```diff
  <Dialog
-  disableBackdropClick
-  onClose={handleClose}
+  onClose={(event, reason) => {
+    if (reason !== 'backdropClick') {
+      handleClose(event, reason);
+    }
+  }}
  />
```

### Удалить компонент withMobileDialog <meta data-oversett="" data-original-text="Remove withMobileDialog component">

Удалите компонент высшего порядка `withMobileDialog`.

:::warning
Это обрабатывается в [preset-safe codemod](#preset-safe) путем применения жестко закодированной функции для предотвращения падения приложения, но требуются дополнительные исправления.
:::

API hook позволяет найти более простое и гибкое решение:

```diff
-import withMobileDialog from '@mui/material/withMobileDialog';
+import { useTheme, useMediaQuery } from '@mui/material';

 function ResponsiveDialog(props) {
-  const { fullScreen } = props;
+  const theme = useTheme();
+  const fullScreen = useMediaQuery(theme.breakpoints.down('sm'));
   const [open, setOpen] = React.useState(false);

 // ...

-export default withMobileDialog()(ResponsiveDialog);
+export default ResponsiveDialog;
```

### ✅ Удалите параметр disableTypography. <meta data-oversett="" data-original-text="✅ Remove disableTypography prop">

Сплющите DOM-структуру DialogTitle и удалите реквизит `disableTypography`.

```diff
-<DialogTitle disableTypography>
-  <Typography variant="h4" component="h2">
+<DialogTitle>
+  <Typography variant="h4" component="span">
      My header
   </Typography>
```

## Разделитель <meta data-oversett="" data-original-text="Divider">

### Замените background-color на border-color <meta data-oversett="" data-original-text="Replace background-color with border-color">

Используйте `border-color` вместо `background-color`. Это предотвратит непостоянство высоты на экранах с измененным масштабом.

Если вы настроили цвет границы, вам нужно будет обновить переопределение свойства CSS:

```diff
 .MuiDivider-root {
-  background-color: #f00;
+  border-color: #f00;
 }
```

## ExpansionPanel <meta data-oversett="" data-original-text="ExpansionPanel">

### ✅ Переименование компонентов <meta data-oversett="" data-original-text="✅ Rename components">

Переименуйте компоненты `ExpansionPanel` в `Accordion`, чтобы использовать более распространенное соглашение об именовании:

```diff
-import ExpansionPanel from '@mui/material/ExpansionPanel';
-import ExpansionPanelSummary from '@mui/material/ExpansionPanelSummary';
-import ExpansionPanelDetails from '@mui/material/ExpansionPanelDetails';
-import ExpansionPanelActions from '@mui/material/ExpansionPanelActions';
+import Accordion from '@mui/material/Accordion';
+import AccordionSummary from '@mui/material/AccordionSummary';
+import AccordionDetails from '@mui/material/AccordionDetails';
+import AccordionActions from '@mui/material/AccordionActions';

-<ExpansionPanel>
+<Accordion>
-  <ExpansionPanelSummary>
+  <AccordionSummary>
      <Typography>Location</Typography>
      <Typography>Select trip destination</Typography>
-  </ExpansionPanelSummary>
+  </AccordionSummary>
-  <ExpansionPanelDetails>
+  <AccordionDetails>
      <Chip label="Barbados" onDelete={() => {}} />
      <Typography variant="caption">Select your destination of choice</Typography>
-  </ExpansionPanelDetails>
+  </AccordionDetails>
    <Divider />
-  <ExpansionPanelActions>
+  <AccordionActions>
      <Button size="small">Cancel</Button>
      <Button size="small">Save</Button>
-  </ExpansionPanelActions>
+  </AccordionActions>
-</ExpansionPanel>
+</Accordion>
```

### Обновление типа события (TypeScript) <meta data-oversett="" data-original-text="Update event type (TypeScript)">

Компонент `event` в `onChange` теперь набирается как `React.SyntheticEvent`, а не `React.ChangeEvent`.

```diff
-<Accordion onChange={(event: React.ChangeEvent<{}>, expanded: boolean) => {}} />
+<Accordion onChange={(event: React.SyntheticEvent, expanded: boolean) => {}} />
```

## ExpansionPanelDetails <meta data-oversett="" data-original-text="ExpansionPanelDetails">

### Удалить отображение: flex <meta data-oversett="" data-original-text="Remove display: flex">

Удалите `display: flex` из `AccordionDetails` (ранее `ExpansionPanelDetails`), так как он был слишком многословен - большинство разработчиков ожидают `display: block`.

## ExpansionPanelSummary <meta data-oversett="" data-original-text="ExpansionPanelSummary">

### Переименовать focused в focusVisible <meta data-oversett="" data-original-text="Rename focused to focusVisible">

Переименовать `focused` в `focusVisible` для согласованности:

```diff
 <AccordionSummary
   classes={{
-    focused: 'custom-focus-visible-classname',
+    focusVisible: 'custom-focus-visible-classname',
   }}
 />
```

### Удалить реквизит IconButtonProps <meta data-oversett="" data-original-text="Remove IconButtonProps prop">

Удалить `IconButtonProps` prop из `AccordionSummary` (ранее `ExpansionPanelSummary`).

Компонент отображает элемент `<div>` вместо `IconButton`, поэтому в этом реквизите больше нет необходимости.

## Fab <meta data-oversett="" data-original-text="Fab">

### ✅ Переименовать круглое в круглое <meta data-oversett="" data-original-text="✅ Rename round to circular">

```diff
-<Fab variant="round">
+<Fab variant="circular">
```

### Удалить span и label <meta data-oversett="" data-original-text="Remove span and label">

Элемент `span`, который обволакивает дочерние элементы, был удален. `label` classKey также удален.

Более подробно об этом изменении можно узнать в [этом запросе на GitHub](https://github.com/mui/material-ui/pull/27112), раньше он был необходим для iOS.

```diff
 <button class="MuiFab-root">
-  <span class="MuiFab-label">
     {children}
-  </span>
 </button>
```

## FormControl <meta data-oversett="" data-original-text="FormControl">

### ✅ Обновление варианта по умолчанию <meta data-oversett="" data-original-text="✅ Update default variant">

Измените вариант по умолчанию с `standard` на `outlined`.

`standard` был удален из руководства по Material Design.

:::warning
✅ Это обрабатывается в [кодовом модуле variant-prop - прочитайте](#variant-prop)подробности перед запуском этого кодового модуля.
:::

```diff
-<FormControl value="Standard" />
-<FormControl value="Outlined" variant="outlined" />
+<FormControl value="Standard" variant="standard" />
+<FormControl value="Outlined" />
```

## FormControlLabel <meta data-oversett="" data-original-text="FormControlLabel">

### Добавьте обязательный реквизит label <meta data-oversett="" data-original-text="Add required label prop">

Реквизит `label` теперь является обязательным. Если вы использовали `FormControlLabel` без `label`, вы можете заменить его значением реквизита `control`.

```diff
-<FormControlLabel control={<Checkbox />} />
+<Checkbox />
```

## Сетка <meta data-oversett="" data-original-text="Grid">

### ✅ Переименовать реквизит justify <meta data-oversett="" data-original-text="✅ Rename justify prop">

Переименуйте реквизит `justify` в `justifyContent` для согласования с именем свойства CSS.

```diff
-<Grid justify="center">
+<Grid justifyContent="center">
```

### ✅ Удалить реквизиты и классы align и justify <meta data-oversett="" data-original-text="✅ Remove align and justify props and classes">

Реквизиты `alignItems`, `alignContent` и `justifyContent`\- вместе с их классами и ключами переопределения стилей - были удалены:

"align-items-xs-center", "align-items-xs-flex-start", "align-items-xs-flex-end", "align-items-xs-baseline", "align-content-xs-center", "align-content-xs-flex-start", "align-content-xs-flex-end", "align-content-xs-space-between", "align-content-xs-space-around", "justify-content-xs-center", "justify-content-xs-flex-end", "justify-content-xs-space-between", "justify-content-xs-space-around" и "justify-content-xs-space-evenly".

Эти реквизиты теперь считаются частью Системы, а не самого компонента `Grid`.

Если вы все еще хотите добавить для них переопределения, вы можете использовать [обратный вызов в качестве значения в `styleOverrides`.](/material-ui/customization/theme-components/#overrides-based-on-props)

```diff
 const theme = createTheme({
   components: {
     MuiGrid: {
-      styleOverrides: {
-        'align-items-xs-flex-end': {
-          marginTop: 20,
-        },
-      },
+      styleOverrides: ({ ownerState }) => ({
+        ...ownerState.alignItems === 'flex-end' && {
+          marginTop: 20,
+        },
+      }),
     },
   },
 });
```

### Изменение отрицательных полей <meta data-oversett="" data-original-text="Change negative margins">

Отрицательные поля применяются только к верхней и левой сторонам контейнера сетки. Если вам нужны отрицательные поля со всех сторон, мы рекомендуем использовать новый Grid v2:

```diff
- import Grid from '@mui/material/Grid';
+ import Grid from '@mui/material/Unstable_Grid2';
```

Чтобы узнать больше о Grid v2, ознакомьтесь с [демо-версиями](/material-ui/react-grid2/#whats-changed) и [руководством по переходу на Grid](/material-ui/migration/migration-grid-v2/).

:::info
Grid v2 был представлен в Material UI v5.9.1 и по умолчанию имеет отрицательные поля со всех сторон.
:::

## GridList <meta data-oversett="" data-original-text="GridList">

### ✅ Переименование компонента GridList <meta data-oversett="" data-original-text="✅ Rename GridList component">

Переименуйте компоненты `GridList` в `ImageList`, чтобы привести их в соответствие с текущим именованием Material Design.

### Переименование реквизитов GridList <meta data-oversett="" data-original-text="Rename GridList props">

-   Переименуйте реквизит GridList `spacing` в `gap`, чтобы привести его в соответствие с атрибутом CSS.
-   Переименуйте реквизит GridList `cellHeight` в `rowHeight`.
-   Добавьте реквизит `variant` в GridList.
-   Переименуйте реквизит GridListItemBar `actionPosition` в `position`. (Обратите внимание также на соответствующие изменения имен классов).

### Используйте CSS object-fit <meta data-oversett="" data-original-text="Use CSS object-fit">

Используйте CSS `object-fit`. Для поддержки IE11 либо используйте полифилл, например,[этот пакет npm](https://www.npmjs.com/package/object-fit-images), либо продолжайте использовать компонент v4.

```diff
-import GridList from '@mui/material/GridList';
-import GridListTile from '@mui/material/GridListTile';
-import GridListTileBar from '@mui/material/GridListTileBar';
+import ImageList from '@mui/material/ImageList';
+import ImageListItem from '@mui/material/ImageListItem';
+import ImageListItemBar from '@mui/material/ImageListItemBar';

-<GridList spacing={8} cellHeight={200}>
-  <GridListTile>
+<ImageList gap={8} rowHeight={200}>
+  <ImageListItem>
    <img src="file.jpg" alt="Image title" />
-    <GridListTileBar
+    <ImageListItemBar
      title="Title"
      subtitle="Subtitle"
    />
-  </GridListTile>
-</GridList>
+  </ImageListItem>
+</ImageList>
```

## Скрытый <meta data-oversett="" data-original-text="Hidden">

### Заменить устаревший компонент <meta data-oversett="" data-original-text="Replace deprecated component">

Этот компонент устарел, поскольку его функциональность может быть создана с помощью функции [`sx`](/system/getting-started/the-sx-prop/) реквизит или [`useMediaQuery`](/material-ui/react-use-media-query/) hook.

:::warning
Это решается в [preset-safe codemod](#preset-safe) путем применения поддельного компонента `Hidden` для предотвращения падения приложения, но требуются дополнительные исправления.
:::

Используйте `sx` prop для замены `implementation="css"`:

```diff
-<Hidden implementation="css" xlUp><Paper /></Hidden>
-<Hidden implementation="css" xlUp><button /></Hidden>
+<Paper sx={{ display: { xl: 'none', xs: 'block' } }} />
+<Box component="button" sx={{ display: { xl: 'none', xs: 'block' } }} />
```

```diff
-<Hidden implementation="css" mdDown><Paper /></Hidden>
-<Hidden implementation="css" mdDown><button /></Hidden>
+<Paper sx={{ display: { xs: 'none', md: 'block' } }} />
+<Box component="button" sx={{ display: { xs: 'none', md: 'block' } }} />
```

Используйте хук `useMediaQuery` для замены `implementation="js"`:

```diff
-<Hidden implementation="js" xlUp><Paper /></Hidden>
+const hidden = useMediaQuery(theme => theme.breakpoints.up('xl'));
+return hidden ? null : <Paper />;
```

## Иконка <meta data-oversett="" data-original-text="Icon">

### Удалить fontSize="default" <meta data-oversett="" data-original-text="Remove fontSize=&quot;default&quot;">

Значение по умолчанию `fontSize` было изменено с `default` на `medium` для согласованности. В маловероятном случае, если вы использовали значение `default`, реквизит можно удалить:

```diff
-<Icon fontSize="default">icon-name</Icon>
+<Icon>icon-name</Icon>
```

## IconButton <meta data-oversett="" data-original-text="IconButton">

### ✅ Обновление реквизита размера <meta data-oversett="" data-original-text="✅ Update size prop">

Отступы для размера по умолчанию были уменьшены до 8px, в результате чего размер уменьшился до 40px.

Для старого размера по умолчанию 48px используйте `size="large"`.

Это изменение было сделано, чтобы лучше соответствовать продуктам Google, когда Material Design перестал документировать шаблон кнопки-иконки.

```diff
- <IconButton>
+ <IconButton size="large">
```

### Удалите span и label <meta data-oversett="" data-original-text="Remove span and label">

Элемент `span`, обволакивающий дочерние элементы, был удален. Также удален элемент `label` classKey.

Подробнее об этом изменении можно узнать в [этом запросе на GitHub](https://github.com/mui/material-ui/pull/26666), оно было необходимо для iOS.

```diff
 <button class="MuiIconButton-root">
-  <span class="MuiIconButton-label">
     <svg />
-  </span>
 </button>
```

## Ссылка <meta data-oversett="" data-original-text="Link">

### ✅ Обновление реквизита подчеркивания по умолчанию <meta data-oversett="" data-original-text="✅ Update default underline prop">

Реквизит `underline` по умолчанию изменен с `"hover"` на `"always"`.

Чтобы воссоздать поведение из v4, примените `defaultProps` в теме.

:::warning
✅ Это обрабатывается в [кодемоде link-underline-hover - прочитайте](#link-underline-hover)подробности перед запуском этого кодемода.
:::

```js
createTheme({
  components: {
    MuiLink: {
      defaultProps: {
        underline: 'hover',
      },
    },
  },
});
```

## Меню <meta data-oversett="" data-original-text="Menu">

### ✅ Обновление реквизитов перехода <meta data-oversett="" data-original-text="✅ Update transition props">

Реквизит перехода `on*` был удален. Вместо него используйте `TransitionProps`.

```diff
 <Menu
-  onEnter={onEnter}
-  onEntered={onEntered}
-  onEntering={onEntering}
-  onExit={onExit}
-  onExited={onExited}
-  onExiting={onExiting}
+  TransitionProps={{
+    onEnter,
+    onEntered,
+    onEntering,
+    onExit,
+    onExited,
+    onExiting,
+  }}
 >
```

:::info
Вариант `selectedMenu` больше не будет вертикально выравнивать выбранный элемент по якорю.
:::

### Изменить значение по умолчанию anchorOrigin.vertical <meta data-oversett="" data-original-text="Change default anchorOrigin.vertical value">

Измените значение по умолчанию `anchorOrigin.vertical`, чтобы следовать рекомендациям Material Design.

Теперь меню отображается под якорем, а не поверх него.

Вы можете восстановить прежнее поведение с помощью:

```diff
 <Menu
+  anchorOrigin={{
+    vertical: 'top',
+    horizontal: 'left',
+  }}
```

## MenuItem . <meta data-oversett="" data-original-text="MenuItem">

### Обновление имен классов CSS <meta data-oversett="" data-original-text="Update CSS class names">

Компонент `MenuItem` наследует компонент `ButtonBase` вместо `ListItem`.

Имена классов, связанные с "MuiListItem-\*", были удалены, а тематизация `ListItem` больше не влияет на `MenuItem`.

```diff
-<li className="MuiButtonBase-root MuiMenuItem-root MuiListItem-root">
+<li className="MuiButtonBase-root MuiMenuItem-root">
```

### Замените реквизит listItemClasses <meta data-oversett="" data-original-text="Replace listItemClasses prop">

Реквизит `listItemClasses` удален, вместо него используйте `classes`.

```diff
-<MenuItem listItemClasses={{...}}>
+<MenuItem classes={{...}}>
```

Подробнее о [API CSS MenuItem](/material-ui/api/menu-item/#css).

## Модальный <meta data-oversett="" data-original-text="Modal">

### ✅ Удалить реквизит disableBackdropClick <meta data-oversett="" data-original-text="✅ Remove disableBackdropClick prop">

Удалите реквизит `disableBackdropClick`, так как он является избыточным.

Вместо него используйте `onClose` и `reason === 'backdropClick'`.

```diff
 <Modal
-  disableBackdropClick
-  onClose={handleClose}
+  onClose={(event, reason) => {
+    if (reason !== 'backdropClick') {
+      handleClose(event, reason);
+    }
+  }}
 />
```

### ✅ Удалить `onEscapeKeyDown` prop <meta data-oversett="" data-original-text="✅ Remove onEscapeKeyDown prop">

Удалите реквизит `onEscapeKeyDown`, потому что он избыточен.

Вместо него используйте `onClose` с `reason === "escapeKeyDown"`.

```diff
 <Modal
-  onEscapeKeyDown={handleEscapeKeyDown}
+  onClose={(event, reason) => {
+    if (reason === 'escapeKeyDown') {
+      handleEscapeKeyDown(event);
+    }
+  }}
 />
```

### Удалить `onRendered` реквизит <meta data-oversett="" data-original-text="Remove onRendered prop">

Удалите реквизит `onRendered`.

В зависимости от варианта использования, вы можете использовать либо [обратный вызов](https://reactjs.org/docs/refs-and-the-dom.html#callback-refs) на дочернем элементе, либо крючок эффекта в дочернем компоненте.

## NativeSelect <meta data-oversett="" data-original-text="NativeSelect">

### Удалить слот selectMenu <meta data-oversett="" data-original-text="Remove selectMenu slot">

Объедините слот `selectMenu` со слотом `select`. Слот `selectMenu` был лишним.

Слот `root` больше не применяется к select, а применяется к корню.

```diff
-<NativeSelect classes={{ root: 'class1', select: 'class2', selectMenu: 'class3' }} />
+<NativeSelect classes={{ select: 'class1 class2 class3' }} />
```

## OutlinedInput <meta data-oversett="" data-original-text="OutlinedInput">

### Заменить реквизит labelWidth <meta data-oversett="" data-original-text="Replace labelWidth prop">

Удалите реквизит `labelWidth`.

Реквизит `label` теперь выполняет ту же цель, используя CSS-макет вместо JavaScript-измерений для отображения разрыва в контуре.

```diff
-<OutlinedInput labelWidth={20} />
+<OutlinedInput label="First Name" />
```

## Бумага <meta data-oversett="" data-original-text="Paper">

### Изменение непрозрачности фона в темном режиме <meta data-oversett="" data-original-text="Change dark mode background opacity">

Изменение непрозрачности фона в зависимости от высоты в темном режиме.

Это изменение было сделано для лучшего соответствия рекомендациям Material Design.

Вы можете отменить его в теме:

```diff
 const theme = createTheme({
   components: {
     MuiPaper: {
+      styleOverrides: { root: { backgroundImage: 'unset' } },
     },
   },
 });
```

## Пагинация <meta data-oversett="" data-original-text="Pagination">

### ✅ Обновление импорта <meta data-oversett="" data-original-text="✅ Update import">

Переместите компонент из лаборатории в ядро.

Компонент теперь стабилен.

```diff
-import Pagination from '@mui/lab/Pagination';
-import PaginationItem from '@mui/lab/PaginationItem';
-import { usePagination } from '@mui/lab/Pagination';
+import Pagination from '@mui/material/Pagination';
+import PaginationItem from '@mui/material/PaginationItem';
+import usePagination from '@mui/material/usePagination';
```

### ✅ Переименуйте круглое в круглое <meta data-oversett="" data-original-text="✅ Rename round to circular">

```diff
-<Pagination shape="round">
-<PaginationItem shape="round">
+<Pagination shape="circular">
+<PaginationItem shape="circular">
```

## Popover <meta data-oversett="" data-original-text="Popover">

### ✅ Обновить реквизит перехода <meta data-oversett="" data-original-text="✅ Update transition props">

Реквизит перехода `on*` был удален.

Вместо него используйте `TransitionProps`.

```diff
  <Popover
-  onEnter={onEnter}
-  onEntered={onEntered}
-  onEntering={onEntering}
-  onExit={onExit}
-  onExited={onExited}
-  onExiting={onExiting}
+  TransitionProps={{
+    onEnter,
+    onEntered,
+    onEntering,
+    onExit,
+    onExited,
+    onExiting,
+  }}
  >
```

### Удалить реквизит getContentAnchorEl <meta data-oversett="" data-original-text="Remove getContentAnchorEl prop">

Реквизит `getContentAnchorEl` был удален для упрощения логики позиционирования.

## Popper <meta data-oversett="" data-original-text="Popper">

### Обновление с v1 до v2 <meta data-oversett="" data-original-text="Upgrade from v1 to v2">

Обновите [Popper.js](https://popper.js.org/) с версии 1 до версии 2.

Префиксы CSS изменились:

```diff
  popper: {
    zIndex: 1,
-  '&[x-placement*="bottom"] .arrow': {
+  '&[data-popper-placement*="bottom"] .arrow': {
```

Имена методов изменились:

```diff
-popperRef.current.scheduleUpdate()
+popperRef.current.update()
```

```diff
-popperRef.current.update()
+popperRef.current.forceUpdate()
```

API модификаторов был изменен слишком значительно, чтобы описать его здесь.

Читайте [руководство по миграции Popper.js](https://popper.js.org/docs/v2/migration-guide/) для получения полной информации.

## Портал <meta data-oversett="" data-original-text="Portal">

### Удалите реквизит onRendered <meta data-oversett="" data-original-text="Remove onRendered prop">

Удалите реквизит `onRendered`.

В зависимости от вашего сценария использования, вы можете использовать либо [обратный вызов](https://reactjs.org/docs/refs-and-the-dom.html#callback-refs) на дочернем элементе, либо хук эффекта в дочернем компоненте.

## Радио <meta data-oversett="" data-original-text="Radio">

### Обновление реквизита цвета по умолчанию <meta data-oversett="" data-original-text="Update default color prop">

Цветовой реквизит радио теперь по умолчанию "первичный".

Чтобы продолжать использовать "вторичный" цвет, необходимо явно указать `secondary`.

Это приближает радио к рекомендациям Material Design.

```diff
-<Radio />
+<Radio color="secondary" />
```

### Обновление классов CSS <meta data-oversett="" data-original-text="Update CSS classes">

Этот компонент больше не имеет имен классов `.MuiIconButton-root` или `.MuiIconButton-label`.

Вместо них используйте `.MuiButtonBase-root`.

```diff
- <span class="MuiIconButton-root MuiButtonBase-root MuiRadio-root PrivateSwitchBase-root">
-   <span class="MuiIconButton-label">
-     <input class="PrivateSwitchBase-input">
+ <span class="MuiButtonBase-root MuiRadio-root PrivateSwitchBase-root">
+   <span class="PrivateSwitchBase-input">
```

## Рейтинг <meta data-oversett="" data-original-text="Rating">

### ✅ Обновление импорта <meta data-oversett="" data-original-text="✅ Update imports">

Переместите компонент из лаборатории в ядро.

Компонент теперь стабилен.

```diff
-import Rating from '@mui/lab/Rating';
+import Rating from '@mui/material/Rating';
```

### Изменить пустую иконку по умолчанию <meta data-oversett="" data-original-text="Change default empty icon">

Измените пустой значок по умолчанию, чтобы улучшить доступность.

Если у вас есть пользовательский `icon` prop, но нет `emptyIcon` prop, вы можете восстановить прежнее поведение с помощью:

```diff
 <Rating
   icon={customIcon}
+  emptyIcon={null}
 />
```

### Переименовать visuallyhidden <meta data-oversett="" data-original-text="Rename visuallyhidden">

Переименуйте `visuallyhidden` в `visuallyHidden` для согласованности:

```diff
  <Rating
    classes={{
-    visuallyhidden: 'custom-visually-hidden-classname',
+    visuallyHidden: 'custom-visually-hidden-classname',
    }}
  />
```

## RootRef <meta data-oversett="" data-original-text="RootRef">

### Удалить компонент <meta data-oversett="" data-original-text="Remove component">

Этот компонент был удален.

Вы можете получить ссылку на базовый DOM-узел наших компонентов через `ref` prop.

Компонент полагается на [`ReactDOM.findDOMNode`](https://reactjs.org/docs/react-dom.html#finddomnode) который [устарел в `React.StrictMode`.](https://reactjs.org/docs/strict-mode.html#warning-about-deprecated-finddomnode-usage)

:::warning
Это обработано в [preset-safe codemod](#preset-safe) путем применения поддельного компонента `RootRef` для предотвращения падения приложения, но требуются дополнительные исправления.
:::

```diff
-<RootRef rootRef={ref}>
-  <Button />
-</RootRef>
+<Button ref={ref} />
```

## Выберите <meta data-oversett="" data-original-text="Select">

### ✅ Обновить вариант по умолчанию <meta data-oversett="" data-original-text="✅ Update default variant">

Измените вариант по умолчанию с `standard` на `outlined`.

`standard` был удален из руководства по Material Design.

Если вы составляете `Select` с компонентом управления формой, вам нужно обновить только `FormControl`\- селект наследует вариант от своего контекста.

:::success
✅ Это обрабатывается в [кодовом модуле variant-prop - прочитайте](#variant-prop)подробности перед запуском этого кодового модуля.
:::

```diff
-<Select value="Standard" />
-<Select value="Outlined" variant="outlined" />
+<Select value="Standard" variant="standard" />
+<Select value="Outlined" />
```

### Заменить реквизит labelWidth <meta data-oversett="" data-original-text="Replace labelWidth prop">

Удалите реквизит `labelWidth`.

Реквизит `label` теперь выполняет ту же цель, используя макет CSS вместо измерений JavaScript для отображения разрыва в варианте `outlined`.

`TextField` уже обрабатывает это по умолчанию.

```diff
-<Select variant="outlined" labelWidth={20} />
+<Select variant="outlined" label="Gender" />
```

### Удалить слот selectMenu <meta data-oversett="" data-original-text="Remove selectMenu slot">

Слот `selectMenu` объединен со слотом `select`. Слот `selectMenu` был лишним.

Слот `root` больше не применяется к select, а применяется к корню.

```diff
-<Select classes={{ root: 'class1', select: 'class2', selectMenu: 'class3' }} />
+<Select classes={{ select: 'class1 class2 class3' }} />
```

### Обновление типа события (TypeScript) <meta data-oversett="" data-original-text="Update event type (TypeScript)">

Событие `event` в `onChange` теперь набирается как `SelectChangeEvent<T>`, а не как `React.ChangeEvent`.

```diff
+ import Select, { SelectChangeEvent } from '@mui/material/Select';

-<Select onChange={(event: React.SyntheticEvent, value: unknown) => {}} />
+<Select onChange={(event: SelectChangeEvent<T>, child: React.ReactNode) => {}} />
```

Это было необходимо для предотвращения переопределения `event.target` событий, вызвавших изменение.

## Скелет <meta data-oversett="" data-original-text="Skeleton">

### ✅ Обновление импорта <meta data-oversett="" data-original-text="✅ Update import">

Переместите компонент из лаборатории в ядро.

Компонент теперь стабилен.

```diff
-import Skeleton from '@mui/lab/Skeleton';
+import Skeleton from '@mui/material/Skeleton';
```

### ✅ Переименовать круг и прямоугольник <meta data-oversett="" data-original-text="✅ Rename circle and rect">

Переименуйте `circle` в `circular` и `rect` в `rectangular` для согласованности:

```diff
-<Skeleton variant="circle" />
-<Skeleton variant="rect" />
-<Skeleton classes={{ circle: 'custom-circle-classname', rect: 'custom-rect-classname',  }} />
+<Skeleton variant="circular" />
+<Skeleton variant="rectangular" />
+<Skeleton classes={{ circular: 'custom-circle-classname', rectangular: 'custom-rect-classname',  }} />
```

## Слайдер <meta data-oversett="" data-original-text="Slider">

### Обновление типа события (TypeScript) <meta data-oversett="" data-original-text="Update event type (TypeScript)">

Событие `event` в `onChange` теперь набирается как `React.SyntheticEvent`, а не как `React.ChangeEvent`.

```diff
-<Slider onChange={(event: React.SyntheticEvent, value: unknown) => {}} />
+<Slider onChange={(event: Event, value: unknown) => {}} />
```

Это было необходимо для предотвращения переопределения `event.target` событий, вызвавших изменение.

### Замена реквизитов ValueLabelComponent и ThumbComponent <meta data-oversett="" data-original-text="Replace ValueLabelComponent and ThumbComponent props">

Реквизиты `ValueLabelComponent` и `ThumbComponent` теперь являются частью реквизита `components`.

```diff
  <Slider
-  ValueLabelComponent={CustomValueLabel}
-  ThumbComponent={CustomThumb}
+  components={{
+    ValueLabel: CustomValueLabel,
+    Thumb: CustomThumb,
+  }}
  />
```

### Рефакторинг CSS <meta data-oversett="" data-original-text="Refactor CSS">

Переработайте CSS в соответствии с последними [рекомендациями Material Design](https://m2.material.io/components/sliders) и сделайте пользовательские стили более интуитивно понятными.[См. документацию](/material-ui/react-slider/).

[<img width="247" alt="" src="https://user-images.githubusercontent.com/3165635/121884800-a8808600-cd13-11eb-8cdf-e25de8f1ba73.png" style="margin: auto">](/material-ui/react-slider/#continuous-sliders)

Вы можете уменьшить плотность слайдера, приблизив ее к v4 с помощью [реквизита`size="small"`](/material-ui/react-slider/#sizes) .

## Snackbar <meta data-oversett="" data-original-text="Snackbar">

### Обновление позиционирования по умолчанию <meta data-oversett="" data-original-text="Update default positioning">

Уведомление теперь отображается слева внизу на больших экранах.

Это лучше соответствует поведению Gmail, Google Keep, material.io и т.д.

Вы можете восстановить поведение v4 с помощью:

```diff
-<Snackbar />
+<Snackbar anchorOrigin={{ vertical: 'bottom', horizontal: 'center' }} />
```

### ✅ Обновить реквизиты перехода <meta data-oversett="" data-original-text="✅ Update transition props">

Реквизиты перехода `on*` были удалены.

Вместо него используйте `TransitionProps`.

```diff
 <Snackbar
-  onEnter={onEnter}
-  onEntered={onEntered}
-  onEntering={onEntering}
-  onExit={onExit}
-  onExited={onExited}
-  onExiting={onExiting}
+  TransitionProps={{
+    onEnter,
+    onEntered,
+    onEntering,
+    onExit,
+    onExited,
+    onExiting,
+  }}
 >
```

## SpeedDial <meta data-oversett="" data-original-text="SpeedDial">

### ✅ Обновить импорт <meta data-oversett="" data-original-text="✅ Update import">

Переместите компонент из лаборатории в ядро.

Компонент теперь стабилен.

```diff
-import SpeedDial from '@mui/lab/SpeedDial';
-import SpeedDialAction from '@mui/lab/SpeedDialAction';
-import SpeedDialIcon from '@mui/lab/SpeedDialIcon';
+import SpeedDial from '@mui/material/SpeedDial';
+import SpeedDialAction from '@mui/material/SpeedDialAction';
+import SpeedDialIcon from '@mui/material/SpeedDialIcon';
```

## Stepper <meta data-oversett="" data-original-text="Stepper">

### Обновить структуру компонента <meta data-oversett="" data-original-text="Update component structure">

Корневой компонент `Paper` был заменен на `<div>`.

`Stepper` больше не имеет возвышения, и он больше не наследует реквизиты от `Paper`. Это изменение предназначено для поощрения композиции.

```diff
+<Paper square elevation={2}>
-  <Stepper elevation={2}>
+  <Stepper>
      <Step>
        <StepLabel>Hello world</StepLabel>
      </Step>
    </Stepper>
+<Paper>
```

### Удаление встроенных отступов <meta data-oversett="" data-original-text="Remove built-in padding">

Встроенный 24px padding был удален.

Чтобы сохранить его, добавьте следующее:

```diff
-<Stepper>
+<Stepper style={{ padding: 24 }}>
    <Step>
      <StepLabel>Hello world</StepLabel>
    </Step>
  </Stepper>
```

## SvgIcon <meta data-oversett="" data-original-text="SvgIcon">

### Удалить fontSize="default" <meta data-oversett="" data-original-text="Remove fontSize=&quot;default&quot;">

Значение по умолчанию `fontSize` было изменено с `default` на `medium` для единообразия.

В том случае, если вы использовали значение `default`, реквизит можно удалить:

```diff
-<SvgIcon fontSize="default">
+<SvgIcon>
   <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z" />
 </SvgIcon>
```

## Переключить . <meta data-oversett="" data-original-text="Switch">

### Удаление второго аргумента onChange <meta data-oversett="" data-original-text="Remove second onChange argument">

Второй аргумент из `onChange` был устаревшим.

Вы можете извлечь проверенное состояние, обратившись к `event.target.checked`.

```diff
 function MySwitch() {
-  const handleChange = (event: React.ChangeEvent<HTMLInputElement>, checked: boolean) => {
+  const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
+    const checked = event.target.checked;
   };

   return <Switch onChange={handleChange} />;
 }
```

### Обновление реквизита цвета по умолчанию <meta data-oversett="" data-original-text="Update default color prop">

Реквизит `color` теперь "первичный" по умолчанию.

Чтобы продолжать использовать "вторичный" цвет, необходимо явно указать `secondary`.

Это приближает `Switch` к рекомендациям Material Design.

```diff
-<Switch />
+<Switch color="secondary" />
```

### Обновление классов CSS <meta data-oversett="" data-original-text="Update CSS classes">

У этого компонента больше нет классов `.MuiIconButton-root` и `.MuiIconButton-label`.

Вместо этого укажите `.MuiButtonBase-root`.

```diff
  <span class="MuiSwitch-root">
-  <span class="MuiIconButton-root MuiButtonBase-root MuiSwitch-switchBase PrivateSwitchBase-root">
-    <span class="MuiIconButton-label">
-      <input class="MuiSwitch-input PrivateSwitchBase-input">
+  <span class="MuiButtonBase-root MuiSwitch-switchBase PrivateSwitchBase-root">
+    <span class="MuiSwitch-input PrivateSwitchBase-input">
```

## Таблица <meta data-oversett="" data-original-text="Table">

### Переименование значения параметра padding по умолчанию <meta data-oversett="" data-original-text="Rename default padding prop value">

Переименуйте значение `default` реквизита `padding` в `normal`.

```diff
-<Table padding="default" />
-<TableCell padding="default" />
+<Table padding="normal" />
+<TableCell padding="normal" />
```

## TablePagination <meta data-oversett="" data-original-text="TablePagination">

### Настройка меток с помощью реквизита getItemAriaLabel <meta data-oversett="" data-original-text="Customize labels with getItemAriaLabel prop">

Настройка меток действий пагинации таблицы должна выполняться с помощью реквизита `getItemAriaLabel`.

Это повышает согласованность с компонентом `Pagination`.

```diff
  <TablePagination
-  backIconButtonText="Back"
-  nextIconButtonText="Next"
+  getItemAriaLabel={…}
```

### ✅ Переименование onChangeRowsPerPage и onChangePage <meta data-oversett="" data-original-text="✅ Rename onChangeRowsPerPage and onChangePage">

Переименуйте `onChangeRowsPerPage` в `onRowsPerPageChange` и `onChangePage` в `onPageChange` для согласованности с API.

```diff
  <TablePagination
-  onChangeRowsPerPage={()=>{}}
-  onChangePage={()=>{}}
+  onRowsPerPageChange={()=>{}}
+  onPageChange={()=>{}}
```

### Отдельные классы для меток <meta data-oversett="" data-original-text="Separate label classes">

Отдельные классы для разных меток пагинации таблиц.

```diff
  <TablePagination
-  classes={{ caption: 'foo' }}
+  classes={{ selectLabel: 'foo', displayedRows: 'foo' }}
  />
```

### Переместить пользовательский класс на input в select <meta data-oversett="" data-original-text="Move custom class on input to select">

Переместите пользовательский класс на `input` на `select`.

Ключ `input` применяется к другому элементу.

```diff
  <TablePagination
-  classes={{ input: 'foo' }}
+  classes={{ select: 'foo' }}
  />
```

## Вкладки <meta data-oversett="" data-original-text="Tabs">

### Обновление значений реквизитов indicatorColor и textColor по умолчанию <meta data-oversett="" data-original-text="Update default indicatorColor and textColor prop values">

Измените значения реквизитов по умолчанию `indicatorColor` и `textColor` на "primary".

Это сделано для соответствия наиболее распространенным вариантам использования Material Design.

```diff
-<Tabs />
+<Tabs indicatorColor="primary" textColor="inherit" />
```

### Обновление типа события (TypeScript) <meta data-oversett="" data-original-text="Update event type (TypeScript)">

Событие `event` в `onChange` теперь набирается как `React.SyntheticEvent`, а не как `React.ChangeEvent`.

```diff
-<Tabs onChange={(event: React.ChangeEvent<{}>, value: unknown) => {}} />
+<Tabs onChange={(event: React.SyntheticEvent, value: unknown) => {}} />
```

### ✅ Добавление нового реквизита кнопки прокрутки <meta data-oversett="" data-original-text="✅ Add new scroll button props">

API, управляющий кнопками прокрутки, был разделен на два реквизита.

-   Реквизит `scrollButtons` управляет отображением кнопок прокрутки в зависимости от доступного пространства.
-   Реквизит `allowScrollButtonsMobile` удаляет медиазапрос CSS, который систематически скрывает кнопки прокрутки на мобильных устройствах.

```diff
-<Tabs scrollButtons="on" />
-<Tabs scrollButtons="desktop" />
-<Tabs scrollButtons="off" />
+<Tabs scrollButtons allowScrollButtonsMobile />
+<Tabs scrollButtons />
+<Tabs scrollButtons={false} />
```

## Вкладка <meta data-oversett="" data-original-text="Tab">

### Обновление значений minWidth и maxWidth по умолчанию <meta data-oversett="" data-original-text="Update default minWidth and maxWidth">

Минимальная и максимальная ширина по умолчанию были изменены в соответствии со [спецификациями Material Design](https://m2.material.io/components/tabs#specs):

-   `minWidth` была изменена с 72px на 90px.
-   `maxWidth` было изменено с 264px на 360px.

### Удаление span и wrapper <meta data-oversett="" data-original-text="Remove span and wrapper">

Элемент `span`, который оборачивает дочерние элементы, был удален. Также удален элемент `wrapper` classKey.

Более подробно об этом изменении вы можете узнать в [этом запросе на GitHub](https://github.com/mui/material-ui/pull/26926).

```diff
  <button class="MuiTab-root">
-  <span class="MuiTab-wrapper">
      {icon}
      {label}
-  </span>
  </button>
```

## TextField <meta data-oversett="" data-original-text="TextField">

### ✅ Обновление варианта по умолчанию <meta data-oversett="" data-original-text="✅ Update default variant">

Измените вариант по умолчанию с `standard` на `outlined`.

`standard` был удален из руководства по Material Design.

:::success
✅ Это обрабатывается в [кодовом модуле variant-prop - прочитайте](#variant-prop)подробности перед запуском этого кодового модуля.
:::

```diff
-<TextField value="Standard" />
-<TextField value="Outlined" variant="outlined" />
+<TextField value="Standard" variant="standard" />
+<TextField value="Outlined" />
```

### ✅ Переименование рядовМакс <meta data-oversett="" data-original-text="✅ Rename rowsMax">

Переименуйте реквизит `rowsMax` в `maxRows` для согласованности с атрибутами HTML.

```diff
-<TextField rowsMax={6}>
+<TextField maxRows={6}>
```

### ✅ Замените rows на minRows <meta data-oversett="" data-original-text="✅ Replace rows with minRows">

Переименуйте `rows` prop в `minRows` для динамического изменения размера.

Вам необходимо использовать реквизит `minRows` в следующем случае:

```diff
-<TextField rows={2} maxRows={5} />
+<TextField minRows={2} maxRows={5} />
```

### Forward ref вместо inputRef prop <meta data-oversett="" data-original-text="Forward ref instead of inputRef prop">

Измените ожидания переадресации ссылок на пользовательском `inputComponent`.

Компонент должен пересылать реквизит `ref` вместо реквизита `inputRef`.

```diff
-function NumberFormatCustom(props) {
-  const { inputRef, onChange, ...other } = props;
+const NumberFormatCustom = React.forwardRef(function NumberFormatCustom(
+  props,
+  ref,
+) {
  const { onChange, ...other } = props;

  return (
    <NumberFormat
      {...other}
-     getInputRef={inputRef}
+     getInputRef={ref}
```

### Переименование классов marginDense и inputMarginDense <meta data-oversett="" data-original-text="Rename marginDense and inputMarginDense classes">

Переименуйте классы `marginDense` и `inputMarginDense` в `sizeSmall` и `inputSizeSmall` для соответствия реквизиту.

```diff
-<Input margin="dense" />
+<Input size="small" />
```

### Обновление реквизита InputAdornment position <meta data-oversett="" data-original-text="Update InputAdornment position prop">

Установите реквизит InputAdornment `position` в `start` или `end`.

Используйте `start`, если в качестве значения используется реквизит `startAdornment`. Используйте `end`, если в качестве значения используется реквизит `endAdornment`.

```diff
-<TextField startAdornment={<InputAdornment>kg</InputAdornment>} />
-<TextField endAdornment={<InputAdornment>kg</InputAdornment>} />
+<TextField startAdornment={<InputAdornment position="start">kg</InputAdornment>} />
+<TextField endAdornment={<InputAdornment position="end">kg</InputAdornment>} />
```

## TextareaAutosize <meta data-oversett="" data-original-text="TextareaAutosize">

### ✅ Заменить строки на minRows <meta data-oversett="" data-original-text="✅ Replace rows with minRows">

Удалите реквизит `rows`, вместо него используйте реквизит `minRows`.

Это изменение направлено на прояснение поведения реквизита.

```diff
-<TextareaAutosize rows={2} />
+<TextareaAutosize minRows={2} />
```

### ✅ Переименовать rowsMax <meta data-oversett="" data-original-text="✅ Rename rowsMax">

Переименуйте `rowsMax` в `maxRows` для согласованности с атрибутами HTML.

```diff
-<TextareaAutosize rowsMax={6}>
+<TextareaAutosize maxRows={6}>
```

### ✅ Переименовать rowsMin <meta data-oversett="" data-original-text="✅ Rename rowsMin">

Переименуйте реквизит `rowsMin` в `minRows` для согласованности с атрибутами HTML.

```diff
-<TextareaAutosize rowsMin={1}>
+<TextareaAutosize minRows={1}>
```

## ToggleButton <meta data-oversett="" data-original-text="ToggleButton">

### ✅ Обновить импорт <meta data-oversett="" data-original-text="✅ Update import">

Переместите компонент из лаборатории в ядро.

Теперь компонент стабилен.

```diff
-import ToggleButton from '@mui/lab/ToggleButton';
-import ToggleButtonGroup from '@mui/lab/ToggleButtonGroup';
+import ToggleButton from '@mui/material/ToggleButton';
+import ToggleButtonGroup from '@mui/material/ToggleButtonGroup';
```

### Удалить span и label <meta data-oversett="" data-original-text="Remove span and label">

Элемент `span`, который оборачивает дочерние элементы, был удален. `label` classKey также удален.

Более подробно об этом изменении вы можете узнать в [этом запросе на GitHub](https://github.com/mui/material-ui/pull/27111).

```diff
  <button class="MuiToggleButton-root">
-  <span class="MuiToggleButton-label">
      {children}
-  </span>
  </button>
```

## Всплывающая подсказка <meta data-oversett="" data-original-text="Tooltip">

### Интерактивные по умолчанию <meta data-oversett="" data-original-text="Interactive by default">

Теперь всплывающие подсказки по умолчанию интерактивны.

Предыдущее поведение по умолчанию не удовлетворяло [критерию успеха 1.4.3 ("hoverable") в WCAG 2.1](https://www.w3.org/TR/WCAG21/#content-on-hover-or-focus).

Чтобы отразить новое значение по умолчанию, реквизит был переименован в `disableInteractive`.

Если вы хотите восстановить поведение v4, вы можете применить следующее отличие:

```diff
-<Tooltip>
+<Tooltip disableInteractive>

 # Interactive tooltips no longer need the `interactive` prop.
-<Tooltip interactive>
+<Tooltip>
```

## Типографика <meta data-oversett="" data-original-text="Typography">

### Удалить вариант srOnly <meta data-oversett="" data-original-text="Remove srOnly variant">

Удалите вариант `srOnly`.

Вместо него вы можете использовать утилиту `visuallyHidden` в сочетании с реквизитом `sx`.

```diff
+import { visuallyHidden } from '@mui/utils';

-<Typography variant="srOnly">Create a user</Typography>
+<span style={visuallyHidden}>Create a user</span>
```

### Удалить ключи переопределения цвета и стиля <meta data-oversett="" data-original-text="Remove color and style override keys">

Были удалены следующие классы и ключи переопределения стиля:

"colorInherit", "colorPrimary", "colorSecondary", "colorTextPrimary", "colorTextSecondary", "colorError", "displayInline" и "displayBlock".

Эти реквизиты теперь считаются частью системы, а не самого компонента `Typography`.

Если вы все еще хотите добавить для них переопределения, вы можете использовать [обратный вызов в качестве значения в `styleOverrides`.](/material-ui/customization/theme-components/#overrides-based-on-props)

Например:

```diff
 const theme = createTheme({
   components: {
     MuiTypography: {
-      styleOverrides: {
-        colorSecondary: {
-          marginTop: '20px',
-        },
-      },
+      styleOverrides: ({ ownerState }) => ({
+        ...ownerState.color === 'secondary' && {
+          marginTop: '20px',
+        },
+      }),
     },
   },
 });
```

## Тема <meta data-oversett="" data-original-text="Theme">

### Цвета фона по умолчанию <meta data-oversett="" data-original-text="Default background colors">

Цвет фона по умолчанию теперь `#fff` в светлом режиме и `#121212` в темном режиме.

Это соответствует рекомендациям Material Design.

### ✅ Поведение точек останова <meta data-oversett="" data-original-text="✅ Breakpoint behavior">

Точки останова теперь рассматриваются как значения, а не как [диапазоны](https://v4.mui.com/customization/breakpoints/#default-breakpoints).

Поведение `down(key)` было изменено, чтобы определять медиа-запрос ниже значения, определенного соответствующей точкой останова (эксклюзивной), а не выше точки останова.

`between(start, end)` также было обновлено, чтобы определять медиа-запрос для значений между фактическими значениями начала (включительно) и конца (исключая).

При использовании утилиты `down()` breakpoints необходимо обновить ключ точки останова на один шаг вверх.

При использовании утилиты `between(start, end)` точку останова конца также необходимо обновить на один шаг вверх.

Ниже приведены примеры необходимых изменений:

```diff
-theme.breakpoints.down('sm') // '@media (max-width:959.95px)' - [0, sm + 1) => [0, md)
+theme.breakpoints.down('md') // '@media (max-width:959.95px)' - [0, md)
```

```diff
-theme.breakpoints.between('sm', 'md') // '@media (min-width:600px) and (max-width:1279.95px)' - [sm, md + 1) => [0, lg)
+theme.breakpoints.between('sm', 'lg') // '@media (min-width:600px) and (max-width:1279.95px)' - [0, lg)
```

```diff
-theme.breakpoints.between('sm', 'xl') // '@media (min-width:600px)'
+theme.breakpoints.up('sm') // '@media (min-width:600px)'
```

То же самое следует сделать при использовании компонента `Hidden`:

```diff
-<Hidden smDown>{...}</Hidden> // '@media (min-width:600px)'
+<Hidden mdDown>{...}</Hidden> // '@media (min-width:600px)'
```

### Размеры точек останова <meta data-oversett="" data-original-text="Breakpoint sizes">

Точки останова по умолчанию были изменены, чтобы лучше соответствовать распространенным случаям использования, а также рекомендациям Material Design.

Более подробно об этом изменении можно узнать в [этом выпуске GitHub](https://github.com/mui/material-ui/issues/21902).

```diff
 {
   xs: 0,
   sm: 600,
-  md: 960,
+  md: 900,
-  lg: 1280,
+  lg: 1200,
-  xl: 1920,
+  xl: 1536,
 }
```

Если вы предпочитаете старые значения точек останова, используйте приведенный ниже фрагмент:

```js
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  breakpoints: {
    values: {
      xs: 0,
      sm: 600,
      md: 960,
      lg: 1280,
      xl: 1920,
    },
  },
});
```

### ✅ Replace theme.breakpoints.width <meta data-oversett="" data-original-text="✅ Replace theme.breakpoints.width">

Утилита `theme.breakpoints.width` была удалена, поскольку она была лишней.

Используйте `theme.breakpoints.values` для получения тех же значений.

```diff
-theme.breakpoints.width('md')
+theme.breakpoints.values.md
```

### Обновление помощника theme.palette.augmentColor <meta data-oversett="" data-original-text="Update theme.palette.augmentColor helper">

Подпись помощника `theme.palette.augmentColor` была изменена:

```diff
-theme.palette.augmentColor(red);
+theme.palette.augmentColor({ color: red, name: 'brand' });
```

### Удалите помощник theme.typography.round <meta data-oversett="" data-original-text="Remove theme.typography.round helper">

Помощник `theme.typography.round` был удален, потому что он больше не используется.

Если он вам нужен, используйте функцию ниже:

```js
function round(value) {
  return Math.round(value * 1e5) / 1e5;
}
```

## @mui/types <meta data-oversett="" data-original-text="@mui/types">

### Переименуйте экспортируемый тип Omit <meta data-oversett="" data-original-text="Rename the exported Omit type">

Модуль теперь называется `DistributiveOmit`.

Это изменение устраняет путаницу со встроенным помощником `Omit`, представленным в TypeScript v3.5.

Встроенный `Omit`, хотя и похож, но не является дистрибутивным. Это приводит к различиям при применении к союзным типам.[Дополнительные подробности см. в ответе на Stack Overflow](https://stackoverflow.com/a/57103940/1009797).

```diff
-import { Omit } from '@mui/types';
+import { DistributiveOmit } from '@mui/types';
```
