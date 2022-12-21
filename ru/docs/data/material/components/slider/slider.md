---
product: material-ui
title: React Slider component
components: Slider
githubLabel: 'component: slider'
materialDesign: https://m2.material.io/components/sliders
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/slidertwothumb/
unstyled: /base/react-slider/
---

# Слайдер <meta data-oversett="" data-original-text="Slider">

<p class="description">Слайдеры позволяют пользователям делать выбор из диапазона значений.</p>

Ползунки отражают диапазон значений вдоль полосы, из которого пользователь может выбрать одно значение. Они идеально подходят для регулировки таких параметров, как громкость, яркость или применение фильтров изображения.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Непрерывные ползунки <meta data-oversett="" data-original-text="Continuous sliders">

Непрерывные ползунки позволяют пользователям выбирать значение в субъективном диапазоне.

{{"demo": "ContinuousSlider.js"}}

## Размеры <meta data-oversett="" data-original-text="Sizes">

Для меньшего размера ползунка используйте опору `size="small"`.

{{"demo": "SliderSizes.js"}}

## Дискретные ползунки <meta data-oversett="" data-original-text="Discrete sliders">

Дискретные ползунки можно настроить на определенное значение, обратившись к индикатору его значения. Для каждого шага можно сгенерировать метку с помощью `marks={true}`.

{{"demo": "DiscreteSlider.js"}}

### Маленькие шаги <meta data-oversett="" data-original-text="Small steps">

Вы можете изменить приращение шага по умолчанию.

{{"demo": "DiscreteSliderSteps.js"}}

### Пользовательские метки <meta data-oversett="" data-original-text="Custom marks">

Вы можете иметь пользовательские метки, предоставив богатый массив реквизиту `marks`.

{{"demo": "DiscreteSliderMarks.js"}}

### Ограниченные значения <meta data-oversett="" data-original-text="Restricted values">

Вы можете ограничить выбираемые значения теми, которые предоставлены в реквизите `marks` с помощью `step={null}`.

{{"demo": "DiscreteSliderValues.js"}}

### Ярлык всегда виден <meta data-oversett="" data-original-text="Label always visible">

Вы можете заставить ярлык большого пальца быть всегда видимым с помощью `valueLabelDisplay="on"`.

{{"demo": "DiscreteSliderLabel.js"}}

## Ползунок диапазона <meta data-oversett="" data-original-text="Range slider">

Ползунок можно использовать для установки начала и конца диапазона, предоставив массив значений реквизиту `value`.

{{"demo": "RangeSlider.js"}}

### Минимальное расстояние <meta data-oversett="" data-original-text="Minimum distance">

В обработчике событий `onChange` можно задать минимальное расстояние между значениями. По умолчанию, когда вы наводите указатель на большой палец и одновременно перетаскиваете другой палец, активный палец поменяется на наведенный. Вы можете отключить это поведение с помощью параметра `disableSwap`. Если вы хотите, чтобы диапазон сдвигался при достижении минимального расстояния, вы можете использовать параметр `activeThumb` в `onChange`.

{{"demo": "MinimumDistanceSlider.js"}}

## Слайдер с полем ввода <meta data-oversett="" data-original-text="Slider with input field">

В этом примере поле ввода позволяет задать дискретное значение.

{{"demo": "InputSlider.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "ColorSlider.js"}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Вот несколько примеров настройки компонента. Подробнее об этом можно узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSlider.js"}}

### Музыкальный проигрыватель <meta data-oversett="" data-original-text="Music player">

{{"demo": "MusicPlayerSlider.js"}}

## Вертикальные ползунки <meta data-oversett="" data-original-text="Vertical sliders">

{{"demo": "VerticalSlider.js"}}

**ВНИМАНИЕ**: Chrome, Safari и более новые версии Edge, т.е. любой браузер, основанный на WebKit, отображает `<Slider orientation="vertical" />` как горизонтальный[(проблема хрома #1158217](https://bugs.chromium.org/p/chromium/issues/detail?id=1158217)). При применении `-webkit-appearance: slider-vertical;` слайдер отображается как вертикальный.

Однако при применении `-webkit-appearance: slider-vertical;` клавиатурная навигация для горизонтальных клавиш (<kbd class="key">Arrow Left</kbd>, <kbd class="key">Arrow Right</kbd>) меняется на противоположную[(проблема хрома #1162640](https://bugs.chromium.org/p/chromium/issues/detail?id=1162640)). Обычно кнопки вверх и вправо должны увеличивать, а влево и вниз - уменьшать значение. Если вы примените `-webkit-appearance`, то сможете предотвратить клавиатурную навигацию для горизонтальных клавиш со стрелками для действительно вертикального слайдера. Это может быть менее запутанным для пользователей, чем изменение направления.

{{"demo": "VerticalAccessibleSlider.js"}}

## Дорожка <meta data-oversett="" data-original-text="Track">

Дорожка показывает диапазон, доступный для выбора пользователем.

### Убранный трек <meta data-oversett="" data-original-text="Removed track">

Трек может быть отключен с помощью `track={false}`.

{{"demo": "TrackFalseSlider.js"}}

### Инвертированная дорожка <meta data-oversett="" data-original-text="Inverted track">

Трек может быть инвертирован с помощью `track="inverted"`.

{{"demo": "TrackInvertedSlider.js"}}

## Нелинейная шкала <meta data-oversett="" data-original-text="Non-linear scale">

Вы можете использовать реквизит `scale` для представления `value` в другом масштабе.

В следующей демонстрации значение _x_ представляет значение _2^x_. Увеличение _x_ на единицу увеличивает представленное значение в _2_ раза.

{{"demo": "NonLinearSlider.js"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/slidertwothumb/)](https://www.w3.org/WAI/ARIA/apg/patterns/slidertwothumb/).

Компонент выполняет большую часть работы, необходимой для обеспечения доступности. Однако вам необходимо убедиться, что:

-   Каждый большой палец имеет удобную для пользователя метку (`aria-label`, `aria-labelledby` или `getAriaLabel` prop).
-   Каждый палец имеет удобный для пользователя текст для его текущего значения. Это не требуется, если значение соответствует семантике метки. Вы можете изменить имя с помощью `getAriaValueText` или `aria-valuetext`.

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### IE 11 <meta data-oversett="" data-original-text="IE 11">

Метка значения слайдера не центрируется в IE 11. Выравнивание не обрабатывается, чтобы облегчить настройку в последних браузерах. Вы можете решить эту проблему с помощью:

```css
.MuiSlider-valueLabel {
  left: calc(-50% - 4px);
}
```
