---
product: material-ui
title: React Autocomplete component
components: TextField, Popper, Autocomplete
githubLabel: 'component: autocomplete'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/combobox/
---

# Автозаполнение <meta data-oversett="" data-original-text="Autocomplete">

<p class="description">Автозаполнение - это обычный текстовый ввод, дополненный панелью предлагаемых вариантов.</p>

Виджет полезен для установки значения однострочного текстового поля в одном из двух типов сценариев:

1.  Значение для текстового поля должно быть выбрано из заранее определенного набора допустимых значений, например, поле местоположения должно содержать допустимое имя местоположения: [комбинированное поле](#combo-box).
2.  Текстовое поле может содержать любое произвольное значение, но выгодно предложить пользователю возможные значения, например, поле поиска может предложить похожие или предыдущие поиски, чтобы сэкономить время пользователя: [свободное соло](#free-solo).

Предполагается, что это улучшенная версия пакетов "react-select" и "downshift".

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Комбобокс <meta data-oversett="" data-original-text="Combo box">

Значение должно быть выбрано из предопределенного набора допустимых значений.

{{"demo": "ComboBox.js"}}

### Структура опций <meta data-oversett="" data-original-text="Options structure">

По умолчанию компонент принимает следующие структуры опций:

```ts
interface AutocompleteOption {
  label: string;
}
// or
type AutocompleteOption = string;
```

например:

```js
const options = [
  { label: 'The Godfather', id: 1 },
  { label: 'Pulp Fiction', id: 2 },
];
// or
const options = ['The Godfather', 'Pulp Fiction'];
```

Однако вы можете использовать другие структуры, предоставив реквизит `getOptionLabel`.

### Игровая площадка <meta data-oversett="" data-original-text="Playground">

Каждый из следующих примеров демонстрирует одну из возможностей компонента Autocomplete.

{{"demo": "Playground.js"}}

### Выбор страны <meta data-oversett="" data-original-text="Country select">

Выберите одну из 248 стран.

{{"demo": "CountrySelect.js"}}

### Управляемые состояния <meta data-oversett="" data-original-text="Controlled states">

Компонент имеет два состояния, которыми можно управлять:

1.  состояние "значение" с комбинацией реквизитов `value`/`onChange`. Это состояние представляет собой значение, выбранное пользователем, например, при нажатии кнопки <kbd class="key">Enter</kbd>.
2.  состояние "входное значение" с комбинацией реквизитов `inputValue`/`onInputChange`. Это состояние представляет собой значение, отображаемое в текстовом поле.

:::warning
Эти два состояния изолированы и должны управляться независимо друг от друга.
:::

{{"demo": "ControllableStates.js"}}

## Свободное соло <meta data-oversett="" data-original-text="Free solo">

Установите `freeSolo` в true, чтобы текстовое поле могло содержать любое произвольное значение.

### Поисковый ввод <meta data-oversett="" data-original-text="Search input">

Реквизит разработан для основного варианта использования **поискового ввода** с предложениями, например, поиск Google или react-autowhatever.

{{"demo": "FreeSolo.js"}}

:::warning
Будьте осторожны при использовании режима свободного соло с нестроковыми опциями, так как это может привести к несоответствию типов.

Значение, создаваемое при вводе в текстовое поле, всегда является строкой, независимо от типа опций.
:::

### Создаваемый <meta data-oversett="" data-original-text="Creatable">

Если вы планируете использовать этот режим для [комбобокса](#combo-box) (расширенная версия элемента select), мы рекомендуем установить:

-   `selectOnFocus` чтобы помочь пользователю очистить выбранное значение.
-   `clearOnBlur` чтобы помочь пользователю ввести новое значение.
-   `handleHomeEndKeys` перемещать фокус внутри всплывающего окна с помощью клавиш <kbd class="key">Home</kbd> и <kbd class="key">End</kbd>.
-   Последний вариант, например: `Add "YOUR SEARCH"`.

{{"demo": "FreeSoloCreateOption.js"}}

Можно также вывести диалоговое окно, когда пользователь хочет добавить новое значение.

{{"demo": "FreeSoloCreateOptionDialog.js"}}

## Сгруппированные <meta data-oversett="" data-original-text="Grouped">

Вы можете сгруппировать опции с помощью реквизита `groupBy`. Если вы это сделаете, убедитесь, что опции также отсортированы по тому же измерению, по которому они сгруппированы, иначе вы заметите дублирующиеся заголовки.

{{"demo": "Grouped.js"}}

Чтобы управлять отображением групп, предоставьте пользовательский реквизит `renderGroup`. Это функция, которая принимает объект с двумя полями:

-   `group`\-строка, представляющая имя группы
-   `children`\-коллекция элементов списка, которые принадлежат группе.

В следующем демонстрационном примере показано, как использовать этот реквизит для определения пользовательской разметки и переопределения стилей групп по умолчанию:

{{"demo": "RenderGroup.js"}}

## Отключенные параметры <meta data-oversett="" data-original-text="Disabled options">

{{"demo": "DisabledOptions.js"}}

## `useAutocomplete` <meta data-oversett="" data-original-text="useAutocomplete">

Для продвинутых случаев использования кастомизации используется безголовый хук `useAutocomplete()`. Он принимает почти те же опции, что и компонент Autocomplete, за вычетом всех реквизитов, связанных с рендерингом JSX. Компонент Autocomplete построен на этом хуке.

```tsx
import { useAutocomplete } from '@mui/base/AutocompleteUnstyled';
```

Хук `useAutocomplete` также реэкспортирован из @mui/material для удобства и обратной совместимости.

```tsx
import useAutocomplete from '@mui/material/useAutocomplete';
```

-   📦 [4.5 kB gzipped](/size-snapshot/).

{{"demo": "UseAutocomplete.js", "defaultCodeOpen": false}}

### Настроенный хук <meta data-oversett="" data-original-text="Customized hook">

{{"demo": "CustomizedHook.js"}}

Перейдите в раздел " [Кастомизация](#customization) ", чтобы посмотреть пример с компонентом `Autocomplete` вместо хука.

## Асинхронные запросы <meta data-oversett="" data-original-text="Asynchronous requests">

Компонент поддерживает два различных случая асинхронного использования:

-   [Загрузка при открытии](#load-on-open): он ждет, пока компонент, с которым взаимодействуют, загрузит опции.
-   [Поиск по мере ввода](#search-as-you-type): при каждом нажатии клавиши выполняется новый запрос.

### Загрузка при открытии <meta data-oversett="" data-original-text="Load on open">

Отображается состояние прогресса, пока запрос к сети находится в процессе выполнения.

{{"demo": "Asynchronous.js"}}

### Поиск по мере ввода <meta data-oversett="" data-original-text="Search as you type">

Если ваша логика заключается в получении новых вариантов при каждом нажатии клавиши и использовании текущего значения текстового поля для фильтрации на сервере, возможно, вам стоит подумать о дросселировании запросов.

Кроме того, вам необходимо отключить встроенную фильтрацию компонента `Autocomplete`, переопределив параметр `filterOptions`:

```jsx
<Autocomplete filterOptions={(x) => x} />
```

### Место Google Maps <meta data-oversett="" data-original-text="Google Maps place">

Настроенный пользовательский интерфейс для автозаполнения Google Maps Places. Для этой демонстрации нам необходимо загрузить [Google Maps JavaScript](https://developers.google.com/maps/documentation/javascript/overview) и [Google Places](https://developers.google.com/maps/documentation/places/web-service/overview) API.

{{"demo": "GoogleMaps.js"}}

:::error
Прежде чем начать использовать Google Maps JavaScript API и Places API, необходимо зарегистрироваться и создать учетную запись.
:::

## Множественные значения <meta data-oversett="" data-original-text="Multiple values">

Также известны как теги, пользователю разрешается вводить более одного значения.

{{"demo": "Tags.js"}}

### Фиксированные параметры <meta data-oversett="" data-original-text="Fixed options">

В случае, если вам необходимо заблокировать определенные теги, чтобы их нельзя было удалить, вы можете установить отключенные фишки.

{{"demo": "FixedTags.js"}}

### Флажки <meta data-oversett="" data-original-text="Checkboxes">

{{"demo": "CheckboxesTags.js"}}

### Ограничивающие теги <meta data-oversett="" data-original-text="Limit tags">

Вы можете использовать реквизит `limitTags`, чтобы ограничить количество отображаемых опций, когда они не сфокусированы.

{{"demo": "LimitTags.js"}}

## Размеры <meta data-oversett="" data-original-text="Sizes">

Вам нравятся меньшие вводы? Используйте реквизит `size`.

{{"demo": "Sizes.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

### Пользовательский ввод <meta data-oversett="" data-original-text="Custom input">

Реквизит `renderInput` позволяет вам настроить рендеринг ввода. Первый аргумент этого реквизита рендеринга содержит реквизиты, которые вам нужно переслать. Обратите особое внимание на ключи `ref` и `inputProps`.

{{"demo": "CustomInputAutocomplete.js"}}

### GitHub's picker <meta data-oversett="" data-original-text="GitHub's picker">

В этом демо воспроизводится подборщик ярлыков GitHub:

{{"demo": "GitHubLabel.js"}}

Перейдите в раздел [Customized hook](#customized-hook) для примера настройки с использованием хука `useAutocomplete` вместо компонента.

## Основные моменты <meta data-oversett="" data-original-text="Highlights">

Следующая демонстрация основана на [autosuggest-highlight](https://github.com/moroshko/autosuggest-highlight), небольшой (1 кБ) утилите для выделения текста в компонентах autosuggest и autocomplete.

{{"demo": "Highlights.js"}}

## Пользовательский фильтр <meta data-oversett="" data-original-text="Custom filter">

Компонент предоставляет фабрику для создания метода фильтра, который может быть предоставлен реквизиту `filterOptions`. Вы можете использовать его для изменения поведения фильтра опций по умолчанию.

```js
import { createFilterOptions } from '@mui/material/Autocomplete';
```

### `createFilterOptions(config) => filterOptions` <meta data-oversett="" data-original-text="createFilterOptions(config) => filterOptions">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `config` _(object_ \[optional\]):

-   `config.ignoreAccents` _(bool_ \[необязательно\]): По умолчанию `true`. Удалить диакритические знаки.
-   `config.ignoreCase` _(bool_ \[необязательно\]): По умолчанию `true`. Убрать все строчные буквы.
-   `config.limit` _(число_ \[необязательно\]): По умолчанию равно null. Ограничивает количество предлагаемых вариантов, которые будут показаны. Например, если `config.limit` - это `100`, то будут показаны только первые `100` подходящих вариантов. Это может быть полезно, если совпадает много вариантов, а виртуализация не была настроена.
-   `config.matchFrom` (_'any' | 'start'_ \[необязательно\]): По умолчанию `'any'`.
-   `config.stringify` _(func_ \[необязательно\]): Определяет, как опция преобразуется в строку, чтобы ее можно было сопоставить с фрагментом входного текста.
-   `config.trim` _(bool_ \[необязательно\]): По умолчанию `false`. Удаление пробелов в конце строки.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`filterOptions`: Возвращаемый метод фильтрации может быть предоставлен непосредственно реквизиту `filterOptions` компонента `Autocomplete` или одноименному параметру для хука.

В следующем демонстрационном примере параметры должны начинаться с префикса запроса:

```jsx
const filterOptions = createFilterOptions({
  matchFrom: 'start',
  stringify: (option) => option.title,
});

<Autocomplete filterOptions={filterOptions} />;
```

{{"demo": "Filter.js", "defaultCodeOpen": false}}

### Advanced <meta data-oversett="" data-original-text="Advanced">

Для более богатых механизмов фильтрации, таких как нечеткое соответствие, рекомендуется обратиться к [match-sorter](https://github.com/kentcdodds/match-sorter). Например:

```jsx
import { matchSorter } from 'match-sorter';

const filterOptions = (options, { inputValue }) => matchSorter(options, inputValue);

<Autocomplete filterOptions={filterOptions} />;
```

## Виртуализация <meta data-oversett="" data-original-text="Virtualization">

Поиск в пределах 10 000 случайно сгенерированных вариантов. Список виртуализируется благодаря [react-window](https://github.com/bvaughn/react-window).

{{"demo": "Virtualize.js"}}

## События <meta data-oversett="" data-original-text="Events">

Если вы хотите предотвратить поведение обработчика клавиш по умолчанию, вы можете установить свойство `defaultMuiPrevented` события на `true`:

```jsx
<Autocomplete
  onKeyDown={(event) => {
    if (event.key === 'Enter') {
      // Prevent's default 'Enter' behavior.
      event.defaultMuiPrevented = true;
      // your handler code
    }
  }}
/>
```

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### автозаполнение/автозаполнение <meta data-oversett="" data-original-text="autocomplete/autofill">

Браузеры имеют эвристику, помогающую пользователю заполнять вводимые данные в форме. Однако это может ухудшить UX компонента.

По умолчанию компонент отключает функцию **автозаполнения** ввода (запоминание того, что пользователь вводил для данного поля в предыдущей сессии) с помощью атрибута `autoComplete="off"`. Google Chrome в настоящее время не поддерживает эту настройку атрибута[(выпуск 587466](https://bugs.chromium.org/p/chromium/issues/detail?id=587466)). Возможным обходным решением является удаление атрибута `id`, чтобы компонент генерировал случайное значение.

Помимо запоминания введенных ранее значений, браузер также может предлагать предложения **автозаполнения** (сохраненные логин, адрес или платежные данные). Если вы хотите избежать автозаполнения, вы можете попробовать следующее:

-   Дайте имя вводимому значению, не раскрывая никакой информации, которую может использовать браузер. Например, `id="field1"` вместо `id="country"`. Если вы оставите id пустым, компонент использует случайный id.
    
-   Установите `autoComplete="new-password"` (некоторые браузеры будут предлагать надежный пароль для входов с таким значением атрибута):
    
    ```jsx
    <TextField
      {...params}
      inputProps={{
        ...params.inputProps,
        autoComplete: 'new-password',
      }}
    />
    ```
    

Подробнее читайте в [руководстве на MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Securing_your_site/Turning_off_form_autocompletion).

### VoiceOver в iOS <meta data-oversett="" data-original-text="iOS VoiceOver">

VoiceOver на iOS Safari не очень хорошо поддерживает атрибут `aria-owns`. Вы можете обойти эту проблему с помощью реквизита `disablePortal`.

### ListboxComponent <meta data-oversett="" data-original-text="ListboxComponent">

Если вы предоставляете пользовательский реквизит `ListboxComponent`, вам необходимо убедиться, что у предполагаемого контейнера прокрутки атрибут `role` установлен на `listbox`. Это обеспечит правильное поведение прокрутки, например, при использовании клавиатуры для навигации.

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/combobox/)](https://www.w3.org/WAI/ARIA/apg/patterns/combobox/)

Мы рекомендуем использовать метку для текстового поля. Компонент реализует авторские практики WAI-ARIA.
