---
product: material-ui
title: React Text Field component
components: FilledInput, FormControl, FormHelperText, Input, InputAdornment, InputBase, InputLabel, OutlinedInput, TextField
githubLabel: 'component: text field'
materialDesign: https://m2.material.io/components/text-fields
unstyled: /base/react-input/
---

# Текстовое поле <meta data-oversett="" data-original-text="Text Field">

<p class="description">Текстовые поля позволяют пользователям вводить и редактировать текст.</p>

Текстовые поля позволяют пользователям вводить текст в пользовательский интерфейс. Они обычно появляются в формах и диалогах.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовое текстовое поле <meta data-oversett="" data-original-text="Basic TextField">

Компонент-обертка `TextField` представляет собой полный элемент управления формой, включающий метку, ввод и текст подсказки. Он имеет три варианта: очерченный (по умолчанию), заполненный и стандартный.

{{"demo": "BasicTextFields.js"}}

**Примечание:** Стандартный вариант `TextField` больше не документирован в [руководстве по Material Design](https://m2.material.io/)[(вот почему](https://medium.com/google-design/the-evolution-of-material-designs-text-fields-603688b3fe03)), но MUI будет продолжать его поддерживать.

## Реквизиты формы <meta data-oversett="" data-original-text="Form props">

Поддерживаются стандартные атрибуты формы, например, `required`, `disabled`, `type` и т.д., а также `helperText`, который используется для предоставления контекста о вводимом поле, например, как оно будет использоваться.

{{"demo": "FormPropsTextFields.js"}}

## Валидация <meta data-oversett="" data-original-text="Validation">

Реквизит `error` переключает состояние ошибки. Реквизит `helperText` может быть использован для предоставления пользователю обратной связи об ошибке.

{{"demo": "ValidationTextFields.js"}}

## Многострочный <meta data-oversett="" data-original-text="Multiline">

Реквизит `multiline` преобразует текстовое поле в элемент [TextareaAutosize](/material-ui/react-textarea-autosize/). Если реквизит `rows` не установлен, высота текстового поля динамически соответствует его содержимому (с помощью [TextareaAutosize](/material-ui/react-textarea-autosize/)). Вы можете использовать реквизиты `minRows` и `maxRows` для его привязки.

{{"demo": "MultilineTextFields.js"}}

## Выберите <meta data-oversett="" data-original-text="Select">

Реквизит `select` заставляет текстовое поле использовать внутренний компонент [Select](/material-ui/react-select/).

{{"demo": "SelectTextFields.js"}}

## Иконки <meta data-oversett="" data-original-text="Icons">

Существует несколько способов отображения значка в текстовом поле.

{{"demo": "InputWithIcon.js"}}

### Украшения ввода <meta data-oversett="" data-original-text="Input Adornments">

Основным способом является `InputAdornment`. Он может быть использован для добавления префикса, суффикса или действия к вводу. Например, вы можете использовать кнопку с иконкой для скрытия или раскрытия пароля.

{{"demo": "InputAdornments.js"}}

## Размеры <meta data-oversett="" data-original-text="Sizes">

Вам нравятся вводимые данные меньшего размера? Используйте реквизит `size`.

{{"demo": "TextFieldSizes.js"}}

Высоту ввода в варианте `filled` можно еще больше уменьшить, выведя метку за его пределы.

{{"demo": "TextFieldHiddenLabel.js"}}

## Маржа <meta data-oversett="" data-original-text="Margin">

Реквизит `margin` может быть использован для изменения вертикального интервала текстового поля. Использование `none` (по умолчанию) не применяет поля к `FormControl`, в то время как `dense` и `normal` применяют.

{{"demo": "LayoutTextFields.js"}}

## Полная ширина <meta data-oversett="" data-original-text="Full width">

`fullWidth` можно использовать для того, чтобы поле ввода занимало всю ширину своего контейнера.

{{"demo": "FullWidthTextField.js"}}

## Неконтролируемый и контролируемый <meta data-oversett="" data-original-text="Uncontrolled vs. Controlled">

Компонент может быть управляемым или неуправляемым.

{{"demo": "StateTextFields.js"}}

## Компоненты <meta data-oversett="" data-original-text="Components">

`TextField` состоит из более мелких компонентов ([`FormControl`](/material-ui/api/form-control/),[`Input`](/material-ui/api/input/),[`FilledInput`](/material-ui/api/filled-input/),[`InputLabel`](/material-ui/api/input-label/),[`OutlinedInput`](/material-ui/api/outlined-input/), и [`FormHelperText`](/material-ui/api/form-helper-text/) ), которые можно использовать непосредственно для значительной настройки вводимых форм.

Вы также могли заметить, что в компоненте `TextField` отсутствуют некоторые собственные свойства ввода HTML. Это сделано специально. Компонент берет на себя заботу о наиболее используемых свойствах. Затем пользователь может использовать базовый компонент, показанный в следующем примере. Тем не менее, вы можете использовать `inputProps` (и свойства `InputProps`, `InputLabelProps` ), если хотите избежать некоторого шаблона.

{{"demo": "ComposedTextField.js"}}

## Входы <meta data-oversett="" data-original-text="Inputs">

{{"demo": "Inputs.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

Свойство `color` изменяет цвет подсветки текстового поля при фокусировке.

{{"demo": "ColorTextFields.js"}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedInputs.js"}}

Персонализация не ограничивается CSS. Вы можете использовать композицию для создания пользовательских компонентов и придания уникальности вашему приложению. Ниже приведен пример с использованием компонента [`InputBase`](/material-ui/api/input-base/) компонента, вдохновленный Google Maps.

{{"demo": "CustomizedInputBase.js", "bg": true}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/text-field/).

## `useFormControl` <meta data-oversett="" data-original-text="useFormControl">

Для более сложных случаев использования кастомизации существует хук `useFormControl()`, который возвращает значение контекста родительского компонента `FormControl`.

**API**

```jsx
import { useFormControl } from '@mui/material/FormControl';
```

**Возвращает**

`value` _(object_):

-   `value.adornedStart` _(bool_): Указывает, имеет ли дочерний компонент `Input` или `Select` начальное украшение.
-   `value.setAdornedStart` _(func_): Функция-установщик для значения состояния `adornedStart`.
-   `value.color` _(string_): Используемый цвет темы, наследуется от `FormControl` `color` prop .
-   `value.disabled` _(bool_): Указывает, отображается ли компонент в отключенном состоянии, унаследовано от `FormControl` `disabled` prop.
-   `value.error` _(bool_): Указывает, отображается ли компонент в состоянии ошибки, унаследовано от `FormControl` `error` prop.
-   `value.filled` _(bool_): Указывает, заполнен ли ввод
-   `value.focused` _(bool_): Указывает, отображается ли компонент и его дочерние элементы в сфокусированном состоянии.
-   `value.fullWidth` _(bool_): Указывает, занимает ли компонент всю ширину своего контейнера, унаследовано от `FormControl` `fullWidth` prop
-   `value.hiddenLabel` _(bool_): Указывает, скрывается ли метка, унаследовано от `FormControl` `hiddenLabel` prop
-   `value.required` _(bool_): Указывает ли метка, что ввод является обязательным, унаследовано от `FormControl` `required` prop
-   `value.size` _(string_): Размер компонента, унаследовано от `FormControl` `size` prop
-   `value.variant` _(строка_): Вариант, используемый компонентом `FormControl` и его дочерними компонентами, унаследовано от `FormControl` `variant` prop
-   `value.onBlur` _(func_): Должна вызываться при размытии входного сигнала.
-   `value.onFocus` _(func_): Должен вызываться при фокусировке ввода
-   `value.onEmpty` _(func_): Должен вызываться, когда вход опустошен
-   `value.onFilled` _(func_): Должен вызываться при заполнении ввода

**Пример**

{{"demo": "UseFormControl.js"}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### Shrink <meta data-oversett="" data-original-text="Shrink">

Состояние "сжимания" метки ввода не всегда корректно. Предполагается, что метка ввода сжимается, как только в ней что-то отображается. В некоторых случаях мы не можем определить состояние "сжимания" (ввод чисел, ввод данных, ввод Stripe). Вы можете заметить наложение.

![shrink](/static/images/text-fields/shrink.png)

Чтобы обойти эту проблему, вы можете принудительно определить состояние "сжатия" метки.

```jsx
<TextField InputLabelProps={{ shrink: true }} />
```

или

```jsx
<InputLabel shrink>Count</InputLabel>
```

### Плавающая метка <meta data-oversett="" data-original-text="Floating label">

Плавающая метка позиционируется абсолютно точно. Она не влияет на макет страницы. Убедитесь, что вводимые данные больше метки для корректного отображения.

### type="number" <meta data-oversett="" data-original-text="type=&quot;number&quot;">

Ввод типа type="number" потенциально может привести к проблемам с удобством использования:

-   Разрешение некоторых нечисловых символов ('e', '+', '-', '.') и молчаливое отбрасывание других.
-   Функциональность прокрутки для увеличения/уменьшения числа может привести к случайным и труднозаметным изменениям.

и многое другое - более подробное объяснение см. в [этой статье](https://technology.blog.gov.uk/2020/02/24/why-the-gov-uk-design-system-team-changed-the-input-type-for-numbers/) команды GOV.UK Design System.

Для валидации чисел одной из жизнеспособных альтернатив является использование стандартного input type="text" с атрибутом _pattern_, например:

```jsx
<TextField inputProps={{ inputMode: 'numeric', pattern: '[0-9]*' }} />
```

В будущем мы, возможно, предоставим [компонент ввода чисел](https://github.com/mui/material-ui/issues/19154).

### Вспомогательный текст <meta data-oversett="" data-original-text="Helper text">

Реквизит helper text влияет на высоту текстового поля. Если разместить рядом два текстовых поля, одно с вспомогательным текстом, а другое без него, они будут иметь разную высоту. Например:

{{"demo": "HelperTextMisaligned.js"}}

Это можно исправить, передав символ пробела в реквизит `helperText`:

{{"demo": "HelperTextAligned.js"}}

## Интеграция со сторонними библиотеками ввода <meta data-oversett="" data-original-text="Integration with 3rd party input libraries">

Вы можете использовать сторонние библиотеки для форматирования ввода. Вам необходимо предоставить пользовательскую реализацию элемента `<input>` со свойством `inputComponent`.

В следующей демонстрации используются библиотеки [react-imask](https://github.com/uNmAnNeR/imaskjs) и [react-number-format](https://github.com/s-yadav/react-number-format). Та же концепция может быть применена, например, к [react-stripe-element](https://github.com/mui/material-ui/issues/16037).

{{"demo": "FormattedInputs.js"}}

Предоставленный компонент ввода должен отображать ref со значением, которое реализует следующий интерфейс:

```ts
interface InputElement {
  focus(): void;
  value?: string;
}
```

```jsx
const MyInputComponent = React.forwardRef((props, ref) => {
  const { component: Component, ...other } = props;

  // implement `InputElement` interface
  React.useImperativeHandle(ref, () => ({
    focus: () => {
      // logic to focus the rendered component from 3rd party belongs here
    },
    // hiding the value e.g. react-stripe-elements
  }));

  // `Component` will be your `SomeThirdPartyComponent` from below
  return <Component {...other} />;
});

// usage
<TextField
  InputProps={{
    inputComponent: MyInputComponent,
    inputProps: {
      component: SomeThirdPartyComponent,
    },
  }}
/>;
```

## Accessibility . <meta data-oversett="" data-original-text="Accessibility">

Для того чтобы текстовое поле было доступным, **ввод должен быть связан с меткой и вспомогательным текстом**. Лежащие в основе узлы DOM должны иметь такую структуру:

```jsx
<div class="form-control">
  <label for="my-input">Email address</label>
  <input id="my-input" aria-describedby="my-helper-text" />
  <span id="my-helper-text">We'll never share your email.</span>
</div>
```

-   Если вы используете компонент `TextField`, вам просто нужно предоставить уникальный `id`, если вы не используете `TextField` только на стороне клиента. Пока пользовательский интерфейс не будет гидратирован `TextField` без явного `id` не будет иметь связанных меток.
-   Если вы составляете компонент:

```jsx
<FormControl>
  <InputLabel htmlFor="my-input">Email address</InputLabel>
  <Input id="my-input" aria-describedby="my-helper-text" />
  <FormHelperText id="my-helper-text">We'll never share your email.</FormHelperText>
</FormControl>
```

## Взаимодополняющие проекты <meta data-oversett="" data-original-text="Complementary projects">

Для более продвинутых случаев использования, вы можете воспользоваться преимуществами:

-   [react-hook-form](https://react-hook-form.com/): React hook для валидации формы.
-   [react-hook-form-mui](https://github.com/dohomi/react-hook-form-mui): MUI и react-hook-form в сочетании.
-   [formik-material-ui](https://github.com/stackworx/formik-mui): Связки для использования MUI с [formik](https://formik.org/).
-   [redux-form-material-ui](https://github.com/erikras/redux-form-material-ui): Связки для использования MUI с [Redux Form](https://redux-form.com/).
-   [mui-rff](https://github.com/lookfirst/mui-rff): Связки для использования MUI с [React Final Form](https://final-form.org/react).
-   [@ui-schema/ds-material](https://www.npmjs.com/package/@ui-schema/ds-material) Связки для использования Material UI с [UI Schema](https://github.com/ui-schema/ui-schema). Совместимость с JSON Schema.
-   [@data-driven-forms/mui-component-mapper](https://data-driven-forms.org/provided-mappers/mui-component-mapper): Связки для использования Material UI с [Data Driven Forms](https://github.com/data-driven-forms/react-forms).
