

# Понимание пакетов MUI <meta data-oversett="" data-original-text="Understanding MUI packages">

<p class="description">Обзор пакетов MUI и связей между ними.</p>

## Обзор <meta data-oversett="" data-original-text="Overview">

-   Если вы хотите построить систему дизайна на основе Material Design, используйте `@mui/material`.
-   Если вы хотите построить систему с использованием компонентов, которые дают вам полный контроль над CSS вашего приложения, используйте `@mui/base`.
-   Для поиска утилит CSS, помогающих в компоновке пользовательского дизайна с помощью Material UI или MUI Base, используйте `@mui/system`.

### Глоссарий <meta data-oversett="" data-original-text="Glossary">

-   **установить** означает запустить `yarn add $module` или `npm install $module`.
-   **Импортировать** - сделать API модуля доступным в вашем коде, добавив `import ... from '$module'`.

## Пакеты MUI <meta data-oversett="" data-original-text="MUI packages">

Ниже приведен актуальный список публичных пакетов `@mui`.

-   `@mui/material`
-   `@mui/base`
-   `@mui/system`
-   `@mui/styled-engine`
-   `@mui/styled-engine-sc`
-   `@mui/styles`

### Понимание продуктов MUI <meta data-oversett="" data-original-text="Understanding MUI's products">

Компания MUI поддерживает набор проектов React UI с открытым исходным кодом и открытым ядром. Эти проекты входят в две линейки продуктов: MUI Core и MUI X.

На следующей схеме показано, как пакеты MUI связаны друг с другом:

<img src="/static/images/packages/mui-packages.png" style="width: 796px; margin-top: 4px; margin-bottom: 8px;" alt="The first half of the image shows @mui/material and @mui/base as component libraries, and @mui/system and styled engines as styling solutions, both under the MUI Core umbrella. The second half shows @mui/x-data-grid and @mui/x-date-pickers as components from MUI X.">

В этой статье мы рассмотрим только пакеты MUI Core. Посетите [обзор MUI X](/x/introduction/) для получения дополнительной информации о нашей коллекции расширенных компонентов.

## Библиотеки компонентов <meta data-oversett="" data-original-text="Component libraries">

### Material UI <meta data-oversett="" data-original-text="Material UI">

Material UI - это обширная библиотека компонентов, в которой представлена наша реализация Material Design от Google.

`@mui/system` Material UI включена в качестве зависимости, что означает, что вам не нужно устанавливать или импортировать ее отдельно - вы можете импортировать ее компоненты и функции непосредственно с сайта `@mui/material`.

### База MUI <meta data-oversett="" data-original-text="MUI Base">

[MUI Base](/base/getting-started/overview/) - это наша библиотека "нестилизованных" компонентов и крючков. С помощью Base вы получаете полный контроль над CSS и функциями доступности вашего приложения.

Пакет Base включает в себя готовые компоненты с функциональностью, готовой к использованию на производстве, а также низкоуровневые крючки для передачи этой функциональности другим компонентам.

### Совместное использование <meta data-oversett="" data-original-text="Using them together">

Представьте, что вы работаете над приложением, использующим `@mui/material` с пользовательской темой, и вам нужно разработать новый компонент переключателя, который выглядит совсем не так, как в Material Design.

В этом случае, вместо того чтобы переопределять все стили компонента Material UI `Switch`, вы можете использовать API `styled` для настройки компонента Base `SwitchUnstyled` с нуля:

```js
import { styled } from '@mui/material/styles';
import SwitchUnstyled, { switchUnstyledClasses } from '@mui/base/SwitchUnstyled';

const Root = styled('span')(`
  position: relative;
  display: inline-block;
  width: 32px;
  height: 20px;

  & .${switchUnstyledClasses.track} {
    // ...css
  }

  & .${switchUnstyledClasses.thumb} {
    // ...css
  }
`);

export default function CustomSwitch() {
  const label = { slotProps: { input: { 'aria-label': 'Demo switch' } } };

  return <SwitchUnstyled component={Root} {...label} />;
}
```

## Стилизация <meta data-oversett="" data-original-text="Styling">

### Движки стилей <meta data-oversett="" data-original-text="Styled engines">

Material UI полагается на движки стилей для внедрения CSS в ваше приложение. Эти движки поставляются в двух пакетах:

-   `@mui/styled-engine`
-   `@mui/styled-engine-sc`

По умолчанию Material UI использует [Emotion](https://emotion.sh/docs/styled) в качестве движка стилизации - он включен в процесс [установки](/material-ui/getting-started/installation/). Если вы планируете использовать Emotion, то `@mui/styled-engine` является зависимостью в вашем приложении, и вам не нужно устанавливать его отдельно.

Если вы предпочитаете использовать [styled-components](https://styled-components.com/docs/basics#getting-started), то вам нужно установить `@mui/styled-engine-sc` вместо пакетов Emotion. Более подробную информацию смотрите в [руководстве по Styled engine](/material-ui/guides/styled-engine/).

В любом случае, вы не будете особо взаимодействовать с этими пакетами помимо установки - они используются внутри `@mui/system`.

:::warning
До версии 5 Material UI использовал `@mui/styles` в качестве обертки JSS. Сейчас этот пакет устарел и будет удален в будущем. Ознакомьтесь с [руководством по переходу с версии 4 на версию 5](/material-ui/migration/migration-v4/), чтобы узнать, как перейти на более новое решение.
:::

### MUI System <meta data-oversett="" data-original-text="MUI System">

MUI System - это набор утилит CSS, которые помогут вам быстро оформить пользовательский дизайн. Для создания утилит CSS он использует адаптер Emotion (`@mui/styled-engine`) в качестве движка стилей по умолчанию.

#### Преимущества MUI System <meta data-oversett="" data-original-text="Advantages of MUI System">

-   Вы имеете полный контроль над объектом `theme`.
-   Вы можете нормально использовать `sx` prop, так как `styled` API поддерживает его по умолчанию.
-   Вы можете иметь тематические компоненты, используя `styled` через слоты и варианты.

:::warning
Чтобы использовать MUI System, вы должны установить Emotion или styled-components, поскольку соответствующий пакет `styled-engine` зависит от них.
:::

<img src="/static/images/packages/mui-system.png" style="width: 796px; margin-top: 4px; margin-bottom: 8px;" alt="A diagram showing an arrow going from @mui/system to @mui/styled-engine, with a note that it is the default engine. Then, from @mui/styled-engine a solid arrow points to @emotion/react and @emotion/styled while a dashed arrow points to @mui/styled-engine-sc, which points to styled-components.">
