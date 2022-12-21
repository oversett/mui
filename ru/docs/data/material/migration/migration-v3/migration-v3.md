

# Миграция с v3 на v4 <meta data-oversett="" data-original-text="Migration from v3 to v4">

<p class="description">Да, v4 уже вышла!</p>

Ищете документацию по v3? Вы можете [найти последнюю версию здесь](https://mui.com/versions/).

:::info
Этот документ находится в процессе разработки. Если вы обновили свой сайт и столкнулись с чем-то, что здесь не описано?[Добавьте свои изменения на GitHub](https://github.com/mui/material-ui/blob/master/docs/data/material/migration/migration-v3/migration-v3.md).
:::

## Введение <meta data-oversett="" data-original-text="Introduction">

Это руководство по обновлению вашего сайта с Material UI v3 до v4. Хотя здесь многое описано, вам, вероятно, не понадобится делать все для вашего сайта. Мы постараемся сделать все возможное, чтобы все было легко и последовательно, чтобы вы могли быстро перейти на v4!

## Почему вы должны мигрировать <meta data-oversett="" data-original-text="Why you should migrate">

На этой странице документации описано, **как** перейти с v3 на v4. О том, **зачем** это делать, рассказывается в [блоге релиза на Medium](https://mui.com/blog/material-ui-v4-is-out/).

## Обновление зависимостей <meta data-oversett="" data-original-text="Updating your dependencies">

Самое первое, что вам нужно будет сделать, это обновить ваши зависимости.

### Обновление версии Material UI <meta data-oversett="" data-original-text="Update Material UI version">

Вам необходимо обновить `package.json`, чтобы использовать последнюю версию Material UI.

```json
"dependencies": {
  "@material-ui/core": "^4.0.0"
}
```

Или выполните команду

```sh
npm install @material-ui/core

or

yarn add @material-ui/core
```

### Обновить версию React <meta data-oversett="" data-original-text="Update React version">

Минимально необходимая версия React была увеличена с `react@^16.3.0` до `react@^16.8.0`. Это позволяет нам полагаться на [Hooks](https://reactjs.org/docs/hooks-intro.html) (мы больше не используем API классов).

### Обновить версию Material UI Styles <meta data-oversett="" data-original-text="Update Material UI Styles version">

Если вы ранее использовали `@material-ui/styles` с v3, вам необходимо обновить `package.json`, чтобы использовать последнюю версию Material UI Styles.

```json
"dependencies": {
  "@material-ui/styles": "^4.0.0"
}
```

Или запустите

```sh
npm install @material-ui/styles

or

yarn add @material-ui/styles
```

## Обработка нежелательных изменений <meta data-oversett="" data-original-text="Handling breaking changes">

### Ядро <meta data-oversett="" data-original-text="Core">

-   Каждый компонент пересылает свою ссылку. Это реализовано с помощью `React.forwardRef()`. Это влияет на внутреннее дерево компонентов и отображаемое имя и поэтому может сломать неглубокие или моментальные тесты.`innerRef` больше не будет возвращать ссылку на экземпляр (или ничего, если внутренний компонент является функциональным компонентом), а будет возвращать ссылку на его корневой компонент. В соответствующих документах API указан корневой компонент.

### Стили <meta data-oversett="" data-original-text="Styles">

-   ⚠️ Material UI зависит от JSS v10. JSS v10 не имеет обратной совместимости с v9. Убедитесь, что JSS v9 не установлен в вашей среде. (Удаление `react-jss` из вашего `package.json` может помочь). Компонент StylesProvider заменяет компонент JssProvider.
    
-   Удалите первый аргумент опции `withTheme()`. (Первый аргумент был заполнителем для потенциальной будущей опции, которая так и не возникла).
    
    Он соответствует [API эмоций](https://emotion.sh/docs/introduction) и [API стилизованных компонентов](https://styled-components.com).
    
    ```diff
    -const DeepChild = withTheme()(DeepChildRaw);
    +const DeepChild = withTheme(DeepChildRaw);
    ```
    
-   Переименуйте `convertHexToRGB` в `hexToRgb`.
    
    ```diff
    -import { convertHexToRgb } from '@material-ui/core/styles/colorManipulator';
    +import { hexToRgb } from '@material-ui/core/styles';
    ```
    
-   Область применения [API ключевых кадров](https://cssinjs.org/jss-syntax/#keyframes-animation). Вы должны применить следующие изменения в вашей кодовой базе. Это поможет изолировать логику анимации:
    
    ```diff
      rippleVisible: {
        opacity: 0.3,
    -   animation: 'mui-ripple-enter 100ms cubic-bezier(0.4, 0, 0.2, 1)',
    +   animation: '$mui-ripple-enter 100ms cubic-bezier(0.4, 0, 0.2, 1)',
      },
      '@keyframes mui-ripple-enter': {
        '0%': {
          opacity: 0.1,
        },
        '100%': {
          opacity: 0.3,
        },
      },
    ```
    

### Тема <meta data-oversett="" data-original-text="Theme">

-   Метод `theme.palette.augmentColor()` больше не выполняет побочный эффект для своего входного цвета. Чтобы использовать его правильно, вы должны использовать возвращаемое значение.
    
    ```diff
    -const background = { main: color };
    -theme.palette.augmentColor(background);
    +const background = theme.palette.augmentColor({ main: color });
    
     console.log({ background });
    ```
    
-   Вы можете смело удалить следующий вариант из создания темы:
    
    ```diff
     typography: {
    -  useNextVariants: true,
     },
    ```
    
-   `theme.spacing.unit` использование устарело, вы можете использовать новый API:
    
    ```diff
     label: {
       [theme.breakpoints.up('sm')]: {
    -    paddingTop: theme.spacing.unit * 12,
    +    paddingTop: theme.spacing(12),
       },
     }
    ```
    
    _Совет: вы можете предоставить более 1 аргумента: `theme.spacing(1, 2) // = '8px 16px'`._
    
    Вы можете использовать [помощник миграции](https://github.com/mui/material-ui/tree/master/packages/mui-codemod/README.md#theme-spacing-api) в вашем проекте, чтобы сделать это более гладко.
    

### Макет <meta data-oversett="" data-original-text="Layout">

-   \[Grid\] Для поддержки произвольных значений интервалов и устранения необходимости мысленно считать по 8, мы изменяем API интервалов:
    
    ```diff
      /**
       * Defines the space between the type `item` component.
       * It can only be used on a type `container` component.
       */
    -  spacing: PropTypes.oneOf([0, 8, 16, 24, 32, 40]),
    +  spacing: PropTypes.oneOf([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]),
    ```
    
    В дальнейшем вы сможете использовать эту тему для реализации [пользовательской функции преобразования расстояний Grid](https://mui.com/system/spacing/#transformation).
    
-   \[Контейнер\] Перемещен с `@material-ui/lab` на `@material-ui/core`.
    
    ```diff
    -import Container from '@material-ui/lab/Container';
    +import Container from '@material-ui/core/Container';
    ```
    

### TypeScript <meta data-oversett="" data-original-text="TypeScript">

#### `value` тип <meta data-oversett="" data-original-text="value type">

Тип `value` для компонентов ввода нормализован для использования `unknown`. Это затрагивает`InputBase`, `NativeSelect`, `OutlinedInput`, `Radio`, `RadioGroup`, `Select`, `SelectInput`, `Switch`, `TextArea`, и `TextField`.

```diff
 function MySelect({ children }) {
-  const handleChange = (event: any, value: string) => {
+  const handleChange = (event: any, value: unknown) => {
     // handle value
   };

   return <Select onChange={handleChange}>{children}</Select>
 }
```

Более подробно это изменение описано в [руководстве по TypeScript](/material-ui/guides/typescript/#handling-value-and-event-handlers).

### Кнопка <meta data-oversett="" data-original-text="Button">

-   \[Button\] Удалите устаревшие варианты кнопок (плоская, приподнятая и fab):
    
    ```diff
    -<Button variant="raised" />
    +<Button variant="contained" />
    ```
    
    ```diff
    -<Button variant="flat" />
    +<Button variant="text" />
    ```
    
    ```diff
    -import Button from '@material-ui/core/Button';
    -<Button variant="fab" />
    +import Fab from '@material-ui/core/Fab';
    +<Fab />
    ```
    
    ```diff
    -import Button from '@material-ui/core/Button';
    -<Button variant="extendedFab" />
    +import Fab from '@material-ui/core/Fab';
    +<Fab variant="extended" />
    ```
    
-   \[ButtonBase\] Компонент, передаваемый в реквизит `component`, должен быть способен удерживать ссылку. В [руководстве по композиции](/material-ui/guides/composition/#caveat-with-refs) объясняется стратегия перехода.
    
    Это также относится к `BottomNavigationAction`, `Button`, `CardActionArea`, `Checkbox`, `ExpansionPanelSummary`, `Fab`, `IconButton`, `MenuItem`, `Radio`, `StepButton`, `Tab`, `TableSortLabel`, а также `ListItem`, если реквизит `button` равен true.
    

### Card <meta data-oversett="" data-original-text="Card">

-   \[CardActions\] Переименуйте реквизит `disableActionSpacing` в `disableSpacing`.
-   \[CardActions\] Удалите CSS-класс `disableActionSpacing`.
-   \[CardActions\] Переименуйте CSS-класс `action` в `spacing`.

### ClickAwayListener <meta data-oversett="" data-original-text="ClickAwayListener">

-   \[ClickAwayListener\] Скрыть реквизит react-event-listener.

### Dialog <meta data-oversett="" data-original-text="Dialog">

-   \[DialogActions\] Переименуйте реквизит `disableActionSpacing` в `disableSpacing`.
-   \[DialogActions\] Переименуйте CSS-класс `action` в `spacing`.
-   \[DialogContentText\] Использовать вариант типографики `body1` вместо `subtitle1`.
-   \[Dialog\] Ребенок должен уметь держать рефлекс. В [руководстве по композиции](/material-ui/guides/composition/#caveat-with-refs)объясняется стратегия переноса.

### Divider <meta data-oversett="" data-original-text="Divider">

-   \[Divider\] Удалите устаревший реквизит `inset`.
    
    ```diff
    -<Divider inset />
    +<Divider variant="inset" />
    ```
    

### ExpansionPanel <meta data-oversett="" data-original-text="ExpansionPanel">

-   \[ExpansionPanelActions\] Переименуйте CSS-класс `action` в `spacing`.
-   \[ExpansionPanel\] Увеличить CSS-специфичность правил стиля `disabled` и `expanded`.
-   \[ExpansionPanel\] Переименовать реквизит `CollapseProps` в `TransitionProps`.

### Список <meta data-oversett="" data-original-text="List">

-   \[List\] Переработайте компоненты списка в соответствии со спецификацией:
    
    -   Компонент `ListItemAvatar` необходим при использовании аватара.
    -   Компонент `ListItemIcon` необходим при использовании левого флажка.
    -   Свойство `edge` должно быть установлено для кнопок с иконками.
-   \[List\] `dense` больше не уменьшает верхний и нижний padding элемента `List`.
    
-   \[ListItem\] Увеличьте CSS-специфичность стилевых правил `disabled` и `focusVisible`.
    

### Меню <meta data-oversett="" data-original-text="Menu">

-   \[MenuItem\] Уберите фиксированную высоту MenuItem. Для вычисления высоты браузер использует padding и line-height.

### Modal <meta data-oversett="" data-original-text="Modal">

-   \[Modal\] Ребенок должен иметь возможность удерживать ссылку. В [руководстве по композиции](/material-ui/guides/composition/#caveat-with-refs) объясняется стратегия переноса.
    
    Это также относится к `Dialog` и `Popover`.
    
-   \[Modal\] Удалите API настройки классов для компонента Modal (уменьшение размера пакета на -74% при автономном использовании).
    
-   \[Modal\] event.defaultPrevented теперь игнорируется. Новая логика закрывает Modal, даже если `event.preventDefault()` вызывается по событию нажатия клавиши escape.`event.preventDefault()` предназначен для остановки поведения по умолчанию, такого как нажатие на чекбокс для установки галочки, нажатие кнопки для отправки формы, нажатие стрелки влево для перемещения курсора в текстовом вводе и т.д. Только специальные элементы HTML имеют такое поведение по умолчанию. Вы должны использовать `event.stopPropagation()`, если не хотите вызывать событие `onClose` на Modal.
    

### Бумага <meta data-oversett="" data-original-text="Paper">

-   \[Бумага\] Уменьшить высоту по умолчанию. Измените высоту бумаги по умолчанию, чтобы она соответствовала карте и панели расширения:
    
    ```diff
    -<Paper />
    +<Paper elevation={2} />
    ```
    
    Это также влияет на `ExpansionPanel`.
    

### Portal \[Портал\] <meta data-oversett="" data-original-text="Portal">

-   \[Портал\] Ребенок должен иметь возможность удерживать ссылку при использовании `disablePortal`. В [руководстве по составлению](/material-ui/guides/composition/#caveat-with-refs) объясняется стратегия перехода.

### Слайд <meta data-oversett="" data-original-text="Slide">

-   \[Слайд\] Ребенок должен иметь возможность удерживать ссылку. [Руководство по составлению](/material-ui/guides/composition/#caveat-with-refs) объясняет стратегию миграции.

### Слайдер <meta data-oversett="" data-original-text="Slider">

-   \[Слайдер\] Перейдите с `@material-ui/lab` на `@material-ui/core`.
    
    ```diff
    -import Slider from '@material-ui/lab/Slider'
    +import Slider from '@material-ui/core/Slider'
    ```
    

### Switch \[Переключатель\] <meta data-oversett="" data-original-text="Switch">

-   \[Switch\] Переработайте реализацию, чтобы упростить переопределение стилей. Переименуйте имена классов в соответствии с формулировкой спецификации:
    
    ```diff
    -icon
    -bar
    +thumb
    +track
    ```
    

### Snackbar <meta data-oversett="" data-original-text="Snackbar">

-   \[Snackbar\] Соответствует новой спецификации.
    
    -   Изменить размеры
    -   Изменить переход по умолчанию с `Slide` на `Grow`.

### SvgIcon <meta data-oversett="" data-original-text="SvgIcon">

-   \[SvgIcon\] Переименовать nativeColor -> htmlColor. React решил ту же проблему с HTML-атрибутом `for`, они решили назвать реквизит `htmlFor`. Это изменение следует тем же доводам.
    
    ```diff
    -<AddIcon nativeColor="#fff" />
    +<AddIcon htmlColor="#fff" />
    ```
    

### Вкладки <meta data-oversett="" data-original-text="Tabs">

-   \[Tab\] Для простоты удалите ключи классов `labelContainer`, `label` и `labelWrapped`. Это позволило нам удалить 2 промежуточных элемента DOM. Вы должны быть в состоянии переместить пользовательские стили в ключ класса `root`.
    
    ![A simpler tab item DOM structure](https://user-images.githubusercontent.com/3165635/53287870-53a35500-3782-11e9-9431-2d1a14a41be0.png)
    
-   \[Tabs\] Удалены устаревшие реквизиты fullWidth и scrollable:
    
    ```diff
    -<Tabs fullWidth scrollable />
    +<Tabs variant="scrollable" />
    ```
    

### Table <meta data-oversett="" data-original-text="Table">

-   \[TableCell\] Удалите устаревшее свойство `numeric`:
    
    ```diff
    -<TableCell numeric>{row.calories}</TableCell>
    +<TableCell align="right">{row.calories}</TableCell>
    ```
    
-   \[TableRow\] Удалите CSS-свойство фиксированной высоты. Высота ячейки вычисляется браузером с помощью padding и line-height.
    
-   \[TableCell\] Переместите режим `dense` в другое свойство:
    
    ```diff
    -<TableCell padding="dense" />
    +<TableCell size="small" />
    ```
    
-   \[TablePagination\] Компонент больше не пытается исправить недопустимые комбинации свойств (`page`, `count`, `rowsPerPage`). Вместо этого он выдает предупреждение.
    

### TextField <meta data-oversett="" data-original-text="TextField">

-   \[InputLabel\] Вы должны иметь возможность переопределять все стили компонента FormLabel, используя CSS API компонента InputLabel. Свойство `FormLabelClasses` было удалено.
    
    ```diff
     <InputLabel
    -  FormLabelClasses={{ asterisk: 'bar' }}
    +  classes={{ asterisk: 'bar' }}
     >
       Foo
     </InputLabel>
    ```
    
-   \[InputBase\] Измените модель размера поля по умолчанию. Теперь она использует следующий CSS:
    
    ```css
    box-sizing: border-box;
    ```
    
    Это решает проблемы со свойством `fullWidth`.
    
-   \[InputBase\] Удалите класс `inputType` из `InputBase`.
    

### Tooltip <meta data-oversett="" data-original-text="Tooltip">

-   \[Tooltip\] Ребенок должен иметь возможность удерживать ссылку. В [руководстве по композиции](/material-ui/guides/composition/#caveat-with-refs) объясняется стратегия переноса.
-   \[Tooltip\] Появляется только после фокуса-видимого фокуса вместо любого фокуса.

### Типографика <meta data-oversett="" data-original-text="Typography">

-   \[Typography\] Удалите устаревшие варианты типографики. Вы можете перейти на новые варианты, выполнив следующие замены:
    
    -   display4 => h1
    -   display3 => h2
    -   display2 => h3
    -   display1 => h4
    -   заголовок => h5
    -   заголовок => h6
    -   подзаголовок => subtitle1
    -   body2 => body1
    -   body1 (по умолчанию) => body2 (по умолчанию)
-   \[Типографика\] Удалите мнительный типографический стиль `display: block` по умолчанию. Вы можете использовать новое свойство `display?: 'initial' | 'inline' | 'block';`.
    
-   \[Типографика\] Переименуйте свойство `headlineMapping` в `variantMapping`, чтобы лучше соответствовать его назначению.
    
    ```diff
    -<Typography headlineMapping={headlineMapping}>
    +<Typography variantMapping={variantMapping}>
    ```
    
-   \[Typography\] Измените вариант по умолчанию с `body2` на `body1`. Размер шрифта по умолчанию 16px лучше, чем 14px. Bootstrap, material.io и даже документация используют 16px в качестве размера шрифта по умолчанию. 14px, как использует Ant Design, понятно, так как у китайских пользователей другой алфавит. 12px рекомендуется в качестве размера шрифта по умолчанию для японского языка.
    
-   \[Типографика\] Удалите цвет по умолчанию из вариантов типографики. Цвет должен наследоваться большую часть времени. Это поведение по умолчанию в Интернете.
    
-   \[Типографика\] Переименуйте `color="default"` в `color="initial"`, следуя логике [этой темы](https://github.com/mui/material-ui/issues/13028). Использование _default_ следует избегать, оно лишено семантики.
    

### Node <meta data-oversett="" data-original-text="Node">

-   [Прекращена поддержка node 6](https://github.com/nodejs/Release/blob/eb91c94681ea968a69bf4a4fe85c656ed44263b3/README.md#release-schedule), вам следует перейти на node 8.

### UMD <meta data-oversett="" data-original-text="UMD">

-   Это изменение облегчает использование Material UI с CDN:
    
    ```diff
     const {
       Button,
       TextField,
    -} = window['material-ui'];
    +} = MaterialUI;
    ```
    
    Это соответствует другим проектам React:
    
    -   material-ui => MaterialUI
    -   react-dom => ReactDOM
    -   prop-types => PropTypes
