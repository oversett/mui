---
product: material-ui
components: Link
githubLabel: 'component: link'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/link/
---

# Ссылки <meta data-oversett="" data-original-text="Links">

<p class="description">Компонент Link позволяет легко настраивать элементы якоря в соответствии с цветами вашей темы и стилями типографики.</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основные ссылки <meta data-oversett="" data-original-text="Basic links">

Компонент Link построен поверх компонента [Typography](/material-ui/api/typography/), что означает, что вы можете использовать его реквизиты.

{{"demo": "Links.js"}}

Однако компонент Link имеет несколько других реквизитов по умолчанию, чем компонент Typography:

-   `color="primary"` так как ссылка должна выделяться.
-   `variant="inherit"` поскольку ссылка в большинстве случаев будет использоваться как дочерний компонент компонента Typography.

## Подчеркивание <meta data-oversett="" data-original-text="Underline">

Реквизит `underline` может быть использован для установки поведения подчеркивания. По умолчанию используется `always`.

{{"demo": "UnderlineLink.js"}}

## Безопасность <meta data-oversett="" data-original-text="Security">

При использовании `target="_blank"` в ссылках [рекомендуется](https://developers.google.com/web/tools/lighthouse/audits/noopener) всегда устанавливать `rel="noopener"` или `rel="noreferrer"` при ссылках на сторонний контент.

-   `rel="noopener"` предотвращает доступ новой страницы к свойству `window.opener` и обеспечивает ее запуск в отдельном процессе. Без этого целевая страница может перенаправить вашу страницу на вредоносный URL.
-   `rel="noreferrer"` имеет тот же эффект, но также предотвращает отправку заголовка _Referer_ на новую страницу. ⚠️ Удаление заголовка referrer повлияет на аналитику.

## Сторонняя библиотека маршрутизации <meta data-oversett="" data-original-text="Third-party routing library">

Одним из частых случаев использования является выполнение навигации только на клиенте, без HTTP-перехода на сервер. Компонент `Link` предоставляет реквизит `component` для обработки этого случая использования. Здесь представлено [более подробное руководство](/material-ui/guides/routing/#link).

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/link/)](https://www.w3.org/WAI/ARIA/apg/patterns/link/)

-   При предоставлении содержания для ссылки избегайте общих описаний типа "нажмите здесь" или "перейдите на". Вместо этого используйте [конкретные описания](https://developers.google.com/web/tools/lighthouse/audits/descriptive-link-text).
-   Для лучшего восприятия пользователем ссылки должны выделяться из текста на странице. Например, вы можете сохранить стандартное поведение `underline="always"`.
-   Если ссылка не имеет значимого href, [ее следует отображать с помощью элемента `<button>`](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/blob/HEAD/docs/rules/anchor-is-valid.md) . Демонстрация ниже показывает, как правильно отображать ссылку с помощью `<button>`:

{{"demo": "ButtonLink.js"}}

### Доступность клавиатуры <meta data-oversett="" data-original-text="Keyboard accessibility">

-   Интерактивные элементы должны получать фокус в последовательном порядке, когда пользователь нажимает клавишу <kbd class="key">Tab</kbd>.
-   Пользователи должны иметь возможность открыть ссылку, нажав клавишу <kbd class="key">Enter</kbd>.

### Доступность считывателя экрана <meta data-oversett="" data-original-text="Screen reader accessibility">

-   Когда ссылка получает фокус, устройства чтения с экрана должны объявлять описательное имя ссылки. Если ссылка открывается в новом окне или вкладке браузера, добавьте символ [`aria-label`](https://www.w3.org/WAI/WCAG22/Techniques/aria/ARIA8) например, _"Чтобы узнать больше, посетите страницу "О сайте", которая откроется в новом окне"._
