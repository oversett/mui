

# Миграция из @material-ui/pickers <meta data-oversett="" data-original-text="Migration from @material-ui/pickers">

<p class="description">Пакет @material-ui/pickers был перемещен в @mui/lab.</p>

:::info
**Стабильный пакет доступен**: Пикеры недоступны в `@mui/lab` после `v5.0.0-alpha.89`. Они были перемещены из `@mui/lab` в пакеты MUI X `@mui/x-date-pickers` и `@mui/x-date-pickers-pro`. Для миграции с `@mui/lab` на `@mui/x-date-pickers` вы можете следовать специальному [руководству по миграции](/x/react-date-pickers/migration-lab/).
:::

:::warning
**Компоненты выбора даты были переписаны**. В большинстве мест логика была переписана с нуля, поэтому невозможно сохранить весь список изменений. Вот обзор наиболее важных концепций, которые были изменены. Если вы собираетесь обновить систему, самым простым способом может быть прохождение по каждому использованию picker в вашей кодовой базе и переписывание их по одному. Не забывайте запускать тесты после каждого!
:::

Это руководство представляет собой обзор основных концепций, которые были изменены в pickers v3.2.10.

## Установка <meta data-oversett="" data-original-text="Installation">

Вам необходимо установить пакет `@mui/lab`, если он еще не установлен. ⚠️ Убедитесь, что вы установили последнюю версию, `"@mui/lab": ^5.0.0-alpha.30"` или выше.

## Импортирует <meta data-oversett="" data-original-text="Imports">

Версия `keyboard` для пикеров больше не публикуется. Во всех версиях мобильных и настольных пикеров реализован ввод с клавиатуры для доступности.

```diff
-import { KeyboardDatePicker } from '@material-ui/pickers';
+import DatePicker from '@mui/lab/DatePicker';

-<KeyboardDatePicker />
+<DatePicker />
```

Также, вместо того, чтобы предоставлять `variant` реквизит, они были перемещены в разные импорты, что означает, что ваш пакет не будет включать `Dialog`, если вы используете только настольный пикер.

-   `<DesktopDatePicker />` - Только настольный вид.
-   `<MobileDatePicker />` - Только мобильный вид.
-   `<DatePicker />` - Мобильный или настольный вид в зависимости от предпочтений пользователя **.**
-   `<StaticDatePicker />` - Само представление пикера, без ввода или любой другой обертки.

```diff
-import { DatePicker } from '@material-ui/pickers';
+import DesktopDatePicker from '@mui/lab/DesktopDatePicker';

-<DatePicker variant="inline" />
+<DesktopDatePicker />
```

Это же соглашение применяется к `TimePicker` - `<DesktopTimePicker>` и `<MobileTimePicker />`.

## MuiPickersUtilsProvider . <meta data-oversett="" data-original-text="MuiPickersUtilsProvider">

`MuiPickersUtilsProvider` был удален в пользу `LocalizationProvider`. Кроме того, пикеры не требуют ручной установки адаптеров date-io. Все включено в `lab`.

❌ До:

```js
import AdapterDateFns from '@date-io/date-fns';
import { MuiPickersUtilsProvider } from '@material-ui/pickers';
```

✅ После:

```jsx
import AdapterDateFns from '@mui/lab/AdapterDateFns';
import LocalizationProvider from '@mui/lab/LocalizationProvider';


function App() {
  return (
    <LocalizationProvider dateAdapter={AdapterDateFns}>
      ...
    </LocalizationProvider>
  )
);
```

## Ввод рендера <meta data-oversett="" data-original-text="Render input">

Мы ввели новый **обязательный** реквизит `renderInput`. Это упрощает использование не-MUI компонентов ввода текстового поля.

```jsx
<DatePicker renderInput={(props) => <TextField {...props} />} />
<TimePicker renderInput={(props) => <TextField {...props} />} />
```

Ранее реквизит распространялся на компонент `<TextField />`. Теперь для их предоставления вам нужно будет использовать новый реквизит `renderInput`:

```diff
 <DatePicker
-  label="Date"
-  helperText="Something"
+  renderInput={props => <TextField label="Date" helperText="Something" /> }
 />
```

## Управление состояниями <meta data-oversett="" data-original-text="State management">

Логика управления состояниями/значениями для пикеров была переписана с нуля. Теперь пикеры будут вызывать реквизит `onChange` при завершении каждого представления даты пикера. Обработчик `onError` также полностью изменился. Тройная проверка ваших пикеров с интеграцией форм, потому что проблемы с интеграцией форм могут быть очень тонкими.

## Не требуется маска <meta data-oversett="" data-original-text="No required mask">

Маска больше не требуется. Также, если предоставленная вами маска не действительна, пикеры будут просто игнорировать маску и разрешать произвольный ввод.

```jsx
<DatePicker
  mask="mm"
  value={new Date()}
  onChange={console.log}
  renderInput={(props) => (
    <TextField {...props} helperText="invalid mask" />
  )}
/>

<DatePicker
  value={new Date()}
  onChange={console.log}
  renderInput={(props) => (
    <TextField {...props} helperText="valid mask" />
  )}
/>
```

## И многое другое <meta data-oversett="" data-original-text="And many more">

-   ```diff
     <DatePicker
    -  format="DD-MMM-YYYY"
    +  inputFormat="DD-MMM-YYYY"
    ```
    

Изменений много, будьте осторожны, убедитесь, что ваши тесты и сборка прошли. Если вы используете сборщик дат в расширенном виде, скорее всего, будет проще переписать его.

Пожалуйста, откройте запрос на исправление руководства, если вы заметили возможность сделать это.
