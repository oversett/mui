---
product: material-ui
title: Circular, Linear progress React components
components: CircularProgress, LinearProgress
githubLabel: 'component: progress'
materialDesign: https://m2.material.io/components/progress-indicators
---

# Прогресс <meta data-oversett="" data-original-text="Progress">

<p class="description">Индикаторы прогресса, обычно известные как спиннеры, выражают неопределенное время ожидания или отображают длительность процесса.</p>

Индикаторы прогресса информируют пользователей о состоянии текущих процессов, таких как загрузка приложения, отправка формы или сохранение обновлений.

-   **Детерминированные** индикаторы показывают, сколько времени займет операция.
-   **Неопределенные** индикаторы отображают неопределенное время ожидания.

Анимация компонентов максимально полагается на CSS, чтобы работать еще до загрузки JavaScript.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Круговой <meta data-oversett="" data-original-text="Circular">

### Круговой неопределенный <meta data-oversett="" data-original-text="Circular indeterminate">

{{"demo": "CircularIndeterminate.js"}}

### Цвет окружности <meta data-oversett="" data-original-text="Circular color">

{{"demo": "CircularColor.js"}}

### Круговой детерминант <meta data-oversett="" data-original-text="Circular determinate">

{{"demo": "CircularDeterminate.js"}}

### Интерактивная интеграция <meta data-oversett="" data-original-text="Interactive integration">

{{"demo": "CircularIntegration.js"}}

### Циркулярная с меткой <meta data-oversett="" data-original-text="Circular with label">

{{"demo": "CircularWithValueLabel.js"}}

## Линейный <meta data-oversett="" data-original-text="Linear">

### Линейный неопределенный <meta data-oversett="" data-original-text="Linear indeterminate">

{{"demo": "LinearIndeterminate.js"}}

### Линейный цветной <meta data-oversett="" data-original-text="Linear color">

{{"demo": "LinearColor.js"}}

### Линейный детерминированный <meta data-oversett="" data-original-text="Linear determinate">

{{"demo": "LinearDeterminate.js"}}

### Линейный буферный <meta data-oversett="" data-original-text="Linear buffer">

{{"demo": "LinearBuffer.js"}}

### Линейный с этикеткой <meta data-oversett="" data-original-text="Linear with label">

{{"demo": "LinearWithValueLabel.js"}}

## Нестандартные диапазоны <meta data-oversett="" data-original-text="Non-standard ranges">

Компоненты прогресса принимают значения в диапазоне 0 - 100. Это упрощает работу для пользователей экранных читалок, для которых эти значения по умолчанию являются минимальными и максимальными. Иногда, однако, вы можете работать с источником данных, где значения выходят за пределы этого диапазона. Вот как можно легко преобразовать значение в любом диапазоне в шкалу 0 - 100:

```jsx
// MIN = Minimum expected value
// MAX = Maximium expected value
// Function to normalise the values (MIN / MAX could be integrated)
const normalise = (value) => ((value - MIN) * 100) / (MAX - MIN);

// Example component that utilizes the `normalise` function at the point of render.
function Progress(props) {
  return (
    <React.Fragment>
      <CircularProgress variant="determinate" value={normalise(props.value)} />
      <LinearProgress variant="determinate" value={normalise(props.value)} />
    </React.Fragment>
  );
}
```

## Персонализация <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Более подробно об этом вы можете узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedProgressBars.js", "defaultCodeOpen": false}}

## Задержка появления <meta data-oversett="" data-original-text="Delaying appearance">

Есть [3 важных ограничения](https://www.nngroup.com/articles/response-times-3-important-limits/), которые необходимо знать о времени отклика. Эффект пульсации компонента `ButtonBase` гарантирует, что пользователь чувствует, что система реагирует мгновенно. Обычно не требуется специальной обратной связи при задержках более 0,1, но менее 1,0 секунды. После 1,0 секунды можно отобразить загрузчик, чтобы поток мыслей пользователя не прерывался.

{{"demo": "DelayingAppearance.js"}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### Высокая загрузка процессора <meta data-oversett="" data-original-text="High CPU load">

При высокой нагрузке может пропасть анимация штрихов или отображаться случайная ширина колец `CircularProgress`. Чтобы не блокировать основной поток рендеринга, необходимо выполнять ресурсоемкие операции в веб-рабочем или пакетно.

![heavy load](/static/images/progress/heavy-load.gif)

Если это невозможно, вы можете воспользоваться реквизитом `disableShrink` для смягчения проблемы. См. [этот вопрос](https://github.com/mui/material-ui/issues/10327).

{{"demo": "CircularUnderLoad.js"}}

### Высокочастотные обновления <meta data-oversett="" data-original-text="High frequency updates">

`LinearProgress` использует переход для свойства CSS transform, чтобы обеспечить плавное обновление между различными значениями. Длительность перехода по умолчанию составляет 200 мс. Если родительский компонент обновляет свойство `value` слишком быстро, вы, по крайней мере, ощутите задержку в 200 мс между повторным рендерингом и полным обновлением индикатора выполнения.

Если вам необходимо выполнять 30 повторных рендерингов в секунду или более, мы рекомендуем отключить переход:

```css
.MuiLinearProgress-bar {
  transition: none;
}
```

### IE 11 <meta data-oversett="" data-original-text="IE 11">

Анимация кругового компонента прогресса в IE 11 ухудшена. Анимация штриха не работает (эквивалентно `disableShrink`), а круговая анимация шатается. Последнюю проблему можно решить с помощью:

```css
.MuiCircularProgress-indeterminate {
  animation: circular-rotate 1.4s linear infinite;
}

@keyframes circular-rotate {
  0% {
    transform: rotate(0deg);
    /* Fix IE11 wobbly */
    transform-origin: 50% 50%;
  }
  100% {
    transform: rotate(360deg);
  }
}
```
