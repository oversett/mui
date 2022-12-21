

# Переход на Grid v2 <meta data-oversett="" data-original-text="Migration to Grid v2">

<p class="description">Это руководство объясняет, как и зачем переходить с Material UI Grid v1 на v2.</p>

## Почему вам следует перейти <meta data-oversett="" data-original-text="Why you should migrate">

Grid v2 имеет несколько новых функций и множество улучшений по сравнению с оригиналом:

-   Grid v2 использует переменные CSS, которые удаляют специфику CSS из селекторов классов. Теперь вы можете использовать `sx` prop в Grid для управления любым стилем, который вы хотите.
-   Все сетки считаются элементами без указания `item` prop.
-   Долгожданная [функция смещения](/material-ui/react-grid2/#offset) дает вам больше гибкости при позиционировании.
-   [Вложенные сетки](/material-ui/react-grid2/#nested-grid) теперь не имеют ограничений по глубине.
-   Флаг `disableEqualOverflow` отключает горизонтальную полосу прокрутки в небольших видовых экранах.

:::info
Grid v2 в настоящее время рассматривается как `Unstable_`, так как мы даем сообществу время опробовать его и предложить свои отзывы. Мы сделаем его стабильным и откажемся от v1 в следующем крупном выпуске Material UI.
:::

## В Material UI v4 <meta data-oversett="" data-original-text="With Material UI v4">

Grid v2 вводится в Material UI v5, поэтому сначала вам нужно следовать [руководству по миграции Material UI](/material-ui/migration/migration-v4/).

## С Material UI v5 <meta data-oversett="" data-original-text="With Material UI v5">

Ожидается, что миграция будет плавной, поскольку большинство API-интерфейсов останется прежним. Однако есть одно принципиальное изменение, которое мы хотели бы прояснить:

Реализация отрицательного поля в Grid v2 по умолчанию распределяется одинаково по всем сторонам (как и в Grid в Material UI v4).

{{"demo": "GridsDiff.js", "bg": true, "hideToolbar": true}}

### Импортировать <meta data-oversett="" data-original-text="Import">

```diff
- import Grid from '@mui/material/Grid';
+ import Grid from '@mui/material/Unstable_Grid2';
```

### Удалить реквизиты <meta data-oversett="" data-original-text="Remove props">

Реквизиты `item` и `zeroMinWidth` были удалены в Grid v2:

```diff
- <Grid item zeroMinWidth xs={6}>
+ <Grid xs={6}>
```

### Отрицательные поля <meta data-oversett="" data-original-text="Negative margins">

Если вы хотите применить отрицательные поля, аналогичные Grid v1, укажите `disableEqualOverflow: true` в контейнере сетки:

{{"demo": "GridDisableEqualOverflow.js", "bg": true, "hideToolbar": true}}

Чтобы применить ко всем сеткам, добавьте реквизит по умолчанию в тему:

```js
import { createTheme, ThemeProvider } from '@mui/material/styles';
import Grid from '@mui/material/Unstable_Grid2';

const theme = createTheme({
  components: {
    MuiGrid2: {
      defaultProps: {
        // all grids under this theme will apply
        // negative margin on the top and left sides.
        disableEqualOverflow: true,
      },
    },
  },
});

function Demo() {
  return (
    <ThemeProvider theme={theme}>
      <Grid container>...grids</Grid>
    </ThemeProvider>
  );
}
```

## Страница документации <meta data-oversett="" data-original-text="Documentation page">

Просмотрите [документацию Grid v2](/material-ui/react-grid2/#fluid-grids) для всех демонстраций и примеров кода.
