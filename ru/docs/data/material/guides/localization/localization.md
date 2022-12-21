

# Локализация <meta data-oversett="" data-original-text="Localization">

<p class="description">Локализация (также называемая "l10n") - это процесс адаптации продукта или контента к конкретной местности или рынку.</p>

По умолчанию в MUI используется английская локализация (Соединенные Штаты). Если вы хотите использовать другие локали, следуйте приведенным ниже инструкциям.

## Текст локали <meta data-oversett="" data-original-text="Locale text">

Используйте тему для глобальной настройки текста локали:

```jsx
import { createTheme, ThemeProvider } from '@mui/material/styles';
import { zhCN } from '@mui/material/locale';

const theme = createTheme(
  {
    palette: {
      primary: { main: '#1976d2' },
    },
  },
  zhCN,
);

<ThemeProvider theme={theme}>
  <App />
</ThemeProvider>;
```

### Пример <meta data-oversett="" data-original-text="Example">

{{"demo": "Locales.js"}}

:::warning
Компоненты [Data Grid и Data Grid Pro](/x/react-data-grid/) имеют свою собственную [локализацию](/x/react-data-grid/localization/).
:::

### Поддерживаемые локали <meta data-oversett="" data-original-text="Supported locales">

| Локаль | Языковой тег BCP 47 | Имя импорта |
| --- | --- | --- |
| Амхарский | am-ET | `amET` |
| арабский (Египет) | ar-EG | `arEG` |
| Арабский (Саудовская Аравия) | ar-SA | `arSA` |
| Арабский (Судан) | ar-SD | `arSD` |
| армянский | hy-AM | `hyAM` |
| Азербайджанский | az-AZ | `azAZ` |
| Бангла | bn-BD | `bnBD` |
| Болгарский | bg-BG | `bgBG` |
| Каталонский | ca-ES | `caES` |
| Китайский (Гонконг) | zh-HK | `zhHK` |
| Китайский (упрощенный) | zh-CN | `zhCN` |
| Китайский (Тайвань) | zh-TW | `zhTW` |
| Хорватский | hr-HR | `hrHR` |
| Чешский | cs-CZ | `csCZ` |
| Датский | da-DK | `daDK` |
| голландский | nl-NL | `nlNL` |
| Английский (Соединенные Штаты) | en-US | `enUS` |
| Эстонский | et-EE | `etEE` |
| Финский | fi-FI | `fiFI` |
| Французский | fr-FR | `frFR` |
| Немецкий | de-DE | `deDE` |
| Греческий | el-GR | `elGR` |
| иврит | he-IL | `heIL` |
| Хинди | hi-IN | `hiIN` |
| Венгерский | hu-HU | `huHU` |
| Исландский | is-IS | `isIS` |
| индонезийский | id-ID | `idID` |
| итальянский | it-IT | `itIT` |
| Японский | ja-JP | `jaJP` |
| Кхмерский | kh-KH | `khKH` |
| Казахский | kk-KZ | `kkKZ` |
| Корейский | ko-KR | `koKR` |
| Македонский | mk-MK | `mkMK` |
| Норвежский (bokmål) | nb-NO | `nbNO` |
| персидский | fa-IR | `faIR` |
| Польский | pl-PL | `plPL` |
| Португальский | pt-PT | `ptPT` |
| Португальский (Бразилия) | pt-BR | `ptBR` |
| Румынский | ro-RO | `roRO` |
| Русский | ru-RU | `ruRU` |
| Сербский | sr-RS | `srRS` |
| сингальский | si-LK | `siLK` |
| словацкий | sk-SK | `skSK` |
| Испанский | es-ES | `esES` |
| Шведский | sv-SE | `svSE` |
| Тайский | th-TH | `thTH` |
| Турецкий | tr-TR | `trTR` |
| Украинский | uk-UA | `ukUA` |
| Урду (Пакистан) | ur-PK | `urPK` |
| Вьетнамский | vi-VN | `viVN` |

Вы можете [найти исходный текст](https://github.com/mui/material-ui/blob/master/packages/mui-material/src/locale/index.ts) в репозитории GitHub.

Чтобы создать свой собственный перевод или изменить английский текст, скопируйте этот файл в свой проект, внесите необходимые изменения и импортируйте локаль оттуда.

Пожалуйста, рассмотрите возможность внесения новых переводов в MUI, открыв запрос на исправление. Однако MUI стремится поддерживать [100 наиболее распространенных](https://en.wikipedia.org/wiki/List_of_languages_by_number_of_native_speakers) [локалей](https://www.ethnologue.com/guides/ethnologue200), мы можем не принимать вклады для локалей, которые не часто используются, например, `gl-ES`, носителями которого являются "всего" 2,5 миллиона человек.

## Поддержка RTL <meta data-oversett="" data-original-text="RTL Support">

Поддерживаются языки с правосторонним переводом, такие как арабский, персидский или иврит. Для их использования следуйте [этому руководству](/material-ui/guides/right-to-left/).
