# Criando Service Workers

Para criar um _Service Worker_ é necessário um arquivo com todos os _handlers_ de eventos que usaremos. Antes disso, precisamos registrar o arquivo do _Service Worker_ criado, como no exemplo abaixo.

```js
// no local da sua aplicação principal
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js', { scope: '/' }).then((registration) => {
    console.log(`Registration success in ${registration.scope}`);
  }).catch((error) => console.log(`Errors happen... ${error}`));
} else {
  console.log('Service Worker is not working on your browser :(');
}
```

Dessa forma, já é possível saber se o registro do arquivo foi feito. Mas atenção para alguns detalhes:

* O `scope` ali é em qual nível de _path_ o _Service Workers_ vai interceptar os _requests_. Se você colocar `/javascripts/` ele irá interceptar todos os _requests_ que tenham o _path_ "javascripts";

## Lifecycle de Service Workers



