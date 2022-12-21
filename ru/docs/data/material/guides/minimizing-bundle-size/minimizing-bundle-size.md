

# Минимизация размера пакета <meta data-oversett="" data-original-text="Minimizing bundle size">

<p class="description">Узнайте больше об инструментах, которые можно использовать для уменьшения размера пакета.</p>

## Размер пакета имеет значение <meta data-oversett="" data-original-text="Bundle size matters">

К размеру пакета в MUI относятся очень серьезно. Снимки размеров делаются на каждом коммите для каждого пакета и критических частей этих пакетов[(посмотреть последний снимок](/size-snapshot/)). В сочетании с [dangerJS](https://danger.systems/js/) мы можем проверять[детальные изменения размера пакета](https://github.com/mui/material-ui/pull/14638#issuecomment-466658459) в каждом Pull Request.

## Когда и как использовать tree-shaking? <meta data-oversett="" data-original-text="When and how to use tree-shaking?">

В современных фреймворках tree-shaking MUI работает из коробки. MUI раскрывает свой полный API на верхнем уровне импорта `@mui`. Если вы используете модули ES6 и бандлер, поддерживающий tree-shaking ([`webpack` >= 2.x](https://webpack.js.org/guides/tree-shaking/), [`parcel` с флагом](https://en.parceljs.org/cli.html#enable-experimental-scope-hoisting/tree-shaking-support)), вы можете смело использовать именованные импорты и получать оптимизированный размер пакета автоматически:

```js
import { Button, TextField } from '@mui/material';
```

⚠️ Следующие инструкции необходимы только в том случае, если вы хотите оптимизировать время запуска разработки или если вы используете старый бандлер, который не поддерживает tree-shaking.

## Среда разработки <meta data-oversett="" data-original-text="Development environment">

Пакеты для разработки могут содержать полную библиотеку, что может привести к **замедлению времени запуска**. Это особенно заметно, если вы используете именованный импорт из `@mui/icons-material`, который может быть в шесть раз медленнее, чем импорт по умолчанию. Например, между следующими двумя импортами, первый (именованный) может быть значительно медленнее, чем второй (по умолчанию):

```js
// 🐌 Named
import { Delete } from '@mui/icons-material';
```

```js
// 🚀 Default
import Delete from '@mui/icons-material/Delete';
```

Если для вас это проблема, у вас есть два варианта:

### Вариант первый: использовать импорт по пути <meta data-oversett="" data-original-text="Option one: use path imports">

Вы можете использовать импорт по пути, чтобы избежать подтягивания неиспользуемых модулей. Например, используйте:

```js
// 🚀 Fast
import Button from '@mui/material/Button';
import TextField from '@mui/material/TextField';
```

вместо импорта верхнего уровня (без плагина Babel):

```js
import { Button, TextField } from '@mui/material';
```

Этот вариант мы документируем во всех демонстрациях, поскольку он не требует настройки. Он рекомендуется для авторов библиотек, которые расширяют компоненты. Перейдите к [варианту 2](#option-two-use-a-babel-plugin) для подхода, который обеспечивает наилучшие DX и UX.

Хотя импорт напрямую таким образом не использует экспорты в [основном файле `@mui/material`,](https://unpkg.com/@mui/material) этот файл может служить удобным справочником о том, какие модули являются публичными.

Помните, что мы поддерживаем импорт только первого и второго уровня. Все, что глубже, считается приватным и может вызвать проблемы, например, дублирование модулей в вашем пучке.

```js
// ✅ OK
import { Add as AddIcon } from '@mui/icons-material';
import { Tabs } from '@mui/material';
//                         ^^^^^^^^ 1st or top-level

// ✅ OK
import AddIcon from '@mui/icons-material/Add';
import Tabs from '@mui/material/Tabs';
//                              ^^^^ 2nd level

// ❌ NOT OK
import TabIndicator from '@mui/material/Tabs/TabIndicator';
//                                           ^^^^^^^^^^^^ 3rd level
```

Если вы используете `eslint`, вы можете отловить проблемный импорт с помощью [правила`no-restricted-imports`](https://eslint.org/docs/latest/rules/no-restricted-imports) . Следующая конфигурация `.eslintrc` выделит проблемный импорт из пакетов `@mui`:

```json
{
  "rules": {
    "no-restricted-imports": [
      "error",
      {
        "patterns": ["@mui/*/*/*", "!@mui/material/test-utils/*"]
      }
    ]
  }
}
```

### Вариант второй: использовать плагин Babel <meta data-oversett="" data-original-text="Option two: use a Babel plugin">

Этот вариант обеспечивает наилучший пользовательский опыт и удобство для разработчиков:

-   UX: Плагин Babel позволяет встряхивать дерево верхнего уровня, даже если ваш бандлер не поддерживает это.
-   DX: Плагин Babel делает время запуска в режиме разработчика таким же быстрым, как и в варианте 1.
-   DX: Этот синтаксис уменьшает дублирование кода, требуя только один импорт для нескольких модулей. В целом, код легче читать, и вы с меньшей вероятностью допустите ошибку при импорте нового модуля.

```js
import { Button, TextField } from '@mui/material';
```

Однако необходимо правильно выполнить два следующих шага.

#### 1\. Настройте Babel <meta data-oversett="" data-original-text="1. Configure Babel">

Выберите один из следующих плагинов:

-   [babel-plugin-import](https://github.com/umijs/babel-plugin-import) со следующей конфигурацией:
    
    `yarn add -D babel-plugin-import`
    
    Создайте файл `.babelrc.js` в корневом каталоге вашего проекта:
    
    ```js
    const plugins = [
      [
        'babel-plugin-import',
        {
          libraryName: '@mui/material',
          libraryDirectory: '',
          camel2DashComponentName: false,
        },
        'core',
      ],
      [
        'babel-plugin-import',
        {
          libraryName: '@mui/icons-material',
          libraryDirectory: '',
          camel2DashComponentName: false,
        },
        'icons',
      ],
    ];
    
    module.exports = { plugins };
    ```
    
-   [babel-plugin-direct-import](https://github.com/umidbekk/babel-plugin-direct-import) со следующей конфигурацией:
    
    `yarn add -D babel-plugin-direct-import`
    
    Создайте файл `.babelrc.js` в корневом каталоге вашего проекта:
    
    ```js
    const plugins = [
      [
        'babel-plugin-direct-import',
        { modules: ['@mui/material', '@mui/icons-material'] },
      ],
    ];
    
    module.exports = { plugins };
    ```
    

Если вы используете Create React App, вам понадобится пара проектов, которые позволяют использовать конфигурацию `.babelrc` без извлечения.

`yarn add -D react-app-rewired customize-cra`

Создайте файл `config-overrides.js` в корневом каталоге:

```js
/* config-overrides.js */
/* eslint-disable react-hooks/rules-of-hooks */
const { useBabelRc, override } = require('customize-cra');

module.exports = override(useBabelRc());
```

При желании, `babel-plugin-import` можно настроить через `config-overrides.js` вместо `.babelrc`, используя эту [конфигурацию](https://github.com/arackaf/customize-cra/blob/master/api.md#fixbabelimportslibraryname-options).

Измените свои команды `package.json`:

```diff
   "scripts": {
-    "start": "react-scripts start",
+    "start": "react-app-rewired start",
-    "build": "react-scripts build",
+    "build": "react-app-rewired build",
-    "test": "react-scripts test",
+    "test": "react-app-rewired test",
     "eject": "react-scripts eject"
  }
```

Наслаждайтесь значительно более быстрым временем запуска.

#### 2\. Преобразование всех ваших импортов <meta data-oversett="" data-original-text="2. Convert all your imports">

Наконец, вы можете преобразовать вашу существующую базу данных в этот вариант с помощью этого [кодового модуля top-level-imports](https://www.npmjs.com/package/@mui/codemod#top-level-imports). Он выполнит следующие различия:

```diff
-import Button from '@mui/material/Button';
-import TextField from '@mui/material/TextField';
+import { Button, TextField } from '@mui/material';
```

## Доступные пакеты <meta data-oversett="" data-original-text="Available bundles">

Пакет, опубликованный на npm, **транспилируется** с помощью [Babel](https://github.com/babel/babel), чтобы учесть [поддерживаемые платформы](/material-ui/getting-started/supported-platforms/).

⚠️ Разработчикам **настоятельно не рекомендуется** импортировать из других пакетов напрямую. В противном случае не гарантируется, что используемые зависимости также используют устаревшие или современные пакеты. Вместо этого используйте эти пакеты на уровне бандлера с помощью, например, [Webpack'а `resolve.alias`:](https://webpack.js.org/configuration/resolve/#resolvealias)

```js
{
  resolve: {
    alias: {
      '@mui/base': '@mui/base/legacy',
      '@mui/lab': '@mui/lab/legacy',
      '@mui/material': '@mui/material/legacy',
      '@mui/styled-engine': '@mui/styled-engine/legacy',
      '@mui/system': '@mui/system/legacy',
      '@mui/utils': '@mui/utils/legacy',
    }
  }
}
```

### Modern bundle <meta data-oversett="" data-original-text="Modern bundle">

Современный пакет находится в [папке`/modern`](https://unpkg.com/@mui/material/modern/) . Он ориентирован на последние выпущенные версии вечнозеленых браузеров (Chrome, Firefox, Safari, Edge). Его можно использовать для создания отдельных пакетов, ориентированных на разные браузеры.

### Устаревший пакет <meta data-oversett="" data-original-text="Legacy bundle">

Если вам нужна поддержка IE 11, вы не можете использовать стандартный или современный пакет без транспиляции. Однако вы можете использовать пакет legacy, который находится в [папке`/legacy`](https://unpkg.com/@mui/material/legacy/) . Вам не нужны дополнительные полифиллы.
