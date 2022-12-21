---
product: material-ui
title: React Stepper component
components: MobileStepper, Step, StepButton, StepConnector, StepContent, StepIcon, StepLabel, Stepper
githubLabel: 'component: stepper'
materialDesign: https://m1.material.io/components/steppers.html
---

# Степпер <meta data-oversett="" data-original-text="Stepper">

<p class="description">Степперы передают прогресс через пронумерованные шаги. Это позволяет создать рабочий процесс, подобный мастеру.</p>

Степперы отображают прогресс через последовательность логических и пронумерованных шагов. Они также могут использоваться для навигации. После сохранения шага степперы могут отображать переходное сообщение обратной связи.

-   **Типы шагов**: Редактируемые, не редактируемые, мобильные, дополнительные.
-   **Типы степперов**: Горизонтальные, вертикальные, линейные, нелинейные.

{{"component": "modules/components/ComponentLinkHeader.js"}}

:::warning
Степперы больше не документируются в [руководстве по Material Design](https://m2.material.io/), но Material UI будет продолжать их поддерживать.
:::

## Горизонтальный степпер <meta data-oversett="" data-original-text="Horizontal stepper">

Горизонтальные степперы идеальны, когда содержимое одного шага зависит от предыдущего.

Избегайте использования длинных имен шагов в горизонтальных степперах.

### Линейный <meta data-oversett="" data-original-text="Linear">

Линейный степпер позволяет пользователю выполнять шаги в последовательности.

Управление `Stepper` осуществляется путем передачи индекса текущего шага (на основе нуля) в качестве параметра `activeStep`. Ориентация `Stepper` задается с помощью параметра `orientation`.

В этом примере также показано использование дополнительного шага путем размещения реквизита `optional` на втором компоненте `Step`. Обратите внимание, что вы сами решаете, когда необязательный шаг будет пропущен. Как только вы определите это для конкретного шага, вы должны установить `completed={false}`, чтобы обозначить, что, хотя индекс активного шага вышел за пределы необязательного шага, на самом деле он не завершен.

{{"demo": "HorizontalLinearStepper.js"}}

### Нелинейные <meta data-oversett="" data-original-text="Non-linear">

Нелинейные степперы позволяют пользователю войти в многошаговый поток в любой точке.

Этот пример похож на обычный горизонтальный степпер, за исключением того, что шаги больше не устанавливаются автоматически на `disabled={true}` на основе реквизита `activeStep`.

Использование `StepButton` здесь демонстрирует кликабельные метки шагов, а также установку флага `completed`. Однако, поскольку доступ к шагам может быть нелинейным, определять, когда все шаги завершены (или даже если они должны быть завершены), будет ваша собственная реализация.

{{"demo": "HorizontalNonLinearStepper.js"}}

### Альтернативная метка <meta data-oversett="" data-original-text="Alternative label">

Ярлыки можно разместить под иконкой шага, установив флаг `alternativeLabel` на компоненте `Stepper`.

{{"demo": "HorizontalLinearAlternativeLabelStepper.js"}}

### Ошибочный шаг <meta data-oversett="" data-original-text="Error step">

{{"demo": "HorizontalStepperWithError.js"}}

### Настроенный горизонтальный степпер <meta data-oversett="" data-original-text="Customized horizontal stepper">

Здесь приведен пример настройки компонента. Подробнее об этом можно узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSteppers.js"}}

## Вертикальный степпер <meta data-oversett="" data-original-text="Vertical stepper">

Вертикальные степперы предназначены для узких экранов. Они идеально подходят для мобильных устройств. В них могут быть реализованы все возможности горизонтального степпера.

{{"demo": "VerticalLinearStepper.js"}}

### Производительность <meta data-oversett="" data-original-text="Performance">

Если вам необходимо сделать содержимое шага доступным для поисковых систем или отобразить дорогие деревья компонентов внутри модала, оптимизируя при этом отзывчивость взаимодействия, возможно, будет хорошей идеей сохранить шаг смонтированным:

```jsx
<StepContent TransitionProps={{ unmountOnExit: false }} />
```

## Мобильный степпер <meta data-oversett="" data-original-text="Mobile stepper">

Этот компонент реализует компактный степпер, подходящий для мобильного устройства. Он имеет более ограниченную функциональность, чем вертикальный степпер. См. раздел " [Мобильные ступеньки](https://m1.material.io/components/steppers.html#steppers-types-of-steps) ".

Мобильный степпер поддерживает три варианта отображения прогресса по доступным ступеням: текст, точки и прогресс.

### Текст <meta data-oversett="" data-original-text="Text">

Текущий шаг и общее количество шагов отображаются в виде текста.

{{"demo": "TextMobileStepper.js", "bg": true}}

### Текст с эффектом карусели <meta data-oversett="" data-original-text="Text with carousel effect">

В этом демо используется[react-swipeable-views](https://github.com/oliviertassinari/react-swipeable-views) для создания карусели.

{{"demo": "SwipeableTextMobileStepper.js", "bg": true}}

### Точки <meta data-oversett="" data-original-text="Dots">

Используйте точки, когда количество шагов невелико.

{{"demo": "DotsMobileStepper.js", "bg": true}}

### Прогресс <meta data-oversett="" data-original-text="Progress">

Используйте индикатор прогресса, если шагов много или если есть шаги, которые необходимо вставить в процесс (на основе ответов на предыдущие шаги).

{{"demo": "ProgressMobileStepper.js", "bg": true}}
