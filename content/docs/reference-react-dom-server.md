---
id: react-dom-server
title: ReactDOMServer
layout: docs
category: Reference
permalink: docs/react-dom-server.html
---

Objekt `ReactDOMServer` pozwala na renderowanie komponentów do oznaczeń statycznych (ang. *static markup*). Zazwyczaj jest używany na serwerze Node:

```js
// ES modules
import ReactDOMServer from 'react-dom/server';
// CommonJS
var ReactDOMServer = require('react-dom/server');
```

## Informacje ogólne {#overview}

Następujące metody mogą być używane zarówno w środowisku serwera, jak i przeglądarki:

- [`renderToString()`](#rendertostring)
- [`renderToStaticMarkup()`](#rendertostaticmarkup)

Te dodatkowe metody są zależne od pakietu (`stream`), który **jest dostępny tylko na serwerze** i nie zadziała w przeglądarce.

- [`renderToNodeStream()`](#rendertonodestream)
- [`renderToStaticNodeStream()`](#rendertostaticnodestream)

* * *

## Dokumentacja {#reference}

### `renderToString()` {#rendertostring}

```javascript
ReactDOMServer.renderToString(element)
```

Metoda zamienia Reactowy element na jego początkowy HTML. Zwraca ciąg znaków HTML. Możesz użyć tej metody do generowania HTML na serwerze i wysłania tych znaczników w początkowym żądaniu do szybszego ładowania się stron oraz umożliwienia wyszukiwarkom śledzenia Twoich stron w celach SEO.

Gdy wywołasz [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) na węźle, który już ma znacznik wyrenderowany na serwerze, React go zachowa i doda tylko obsługę zdarzeń, pozwalając na bardzo wydajne pierwsze załadowanie strony.

* * *

### `renderToStaticMarkup()` {#rendertostaticmarkup}

```javascript
ReactDOMServer.renderToStaticMarkup(element)
```

Podobne do [`renderToString`](#rendertostring), poza tym, że nie tworzy dodatkowych atrybutów DOM, których React używa wewnętrznie, takich jak `data-reactroot`. Jest to przydatne, gdy chcesz użyć Reacta jako prosty generator statycznych stron, a usunięcie dodatkowych atrybutów pozwoli na zaoszczędzenie kilku bajtów.

Gdy planujesz użyć Reacta po stronie klienta do tworzenia interaktywnych znaczników, nie używaj tej metody. Zamiast tego, użyj [`renderToString`](#rendertostring) na serwerze oraz [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) po stronie klienta.

* * *

### `renderToNodeStream()` {#rendertonodestream}

```javascript
ReactDOMServer.renderToNodeStream(element)
```

Metoda zamienia Reactowy element na jego początkowy HTML. Zwraca [Readable stream](https://nodejs.org/api/stream.html#stream_readable_streams), którego danymi wyjściowymi jest ciąg znaków HTML. Dane wyjściowe HTML tego streama są dokładnie takie jakie by zwrócił [`ReactDOMServer.renderToString`](#rendertostring). Możesz użyć tej metody do generowania HTML na serwerze i wysłania tych znaczników w początkowym żądaniu do szybszego ładowania się stron oraz umożliwienia wyszukiwarkom śledzenia Twoich stron w celach SEO.

If you call [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) on a node that already has this server-rendered markup, React will preserve it and only attach event handlers, allowing you to have a very performant first-load experience.

> Note:
>
> Server-only. This API is not available in the browser.
>
> The stream returned from this method will return a byte stream encoded in utf-8. If you need a stream in another encoding, take a look at a project like [iconv-lite](https://www.npmjs.com/package/iconv-lite), which provides transform streams for transcoding text.

* * *

### `renderToStaticNodeStream()` {#rendertostaticnodestream}

```javascript
ReactDOMServer.renderToStaticNodeStream(element)
```

Similar to [`renderToNodeStream`](#rendertonodestream), except this doesn't create extra DOM attributes that React uses internally, such as `data-reactroot`. This is useful if you want to use React as a simple static page generator, as stripping away the extra attributes can save some bytes.

The HTML output by this stream is exactly equal to what [`ReactDOMServer.renderToStaticMarkup`](#rendertostaticmarkup) would return.

If you plan to use React on the client to make the markup interactive, do not use this method. Instead, use [`renderToNodeStream`](#rendertonodestream) on the server and [`ReactDOM.hydrate()`](/docs/react-dom.html#hydrate) on the client.

> Note:
>
> Server-only. This API is not available in the browser.
>
> The stream returned from this method will return a byte stream encoded in utf-8. If you need a stream in another encoding, take a look at a project like [iconv-lite](https://www.npmjs.com/package/iconv-lite), which provides transform streams for transcoding text.
