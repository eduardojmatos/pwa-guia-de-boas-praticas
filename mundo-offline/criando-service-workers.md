# Criando Service Workers

Para criar um _Service Worker_ é necessário um arquivo com todos os _handlers_ de eventos que usaremos. Antes disso, precisamos registrar o arquivo do _Service Worker_ criado, como no exemplo abaixo.

```js
// no local da sua aplicação principal

// Checando se existe o Service Worker no browser do usuário
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js', { scope: '/' }).then((registration) => {
    console.log(`Registration success in ${registration.scope} e o status é ${registration.state}`);
  }).catch((error) => console.log(`Errors happen... ${error}`));
} else {
  console.log('Service Worker is not working on your browser :(');
}
```

Dessa forma, já é possível saber se o registro do arquivo foi feito. Mas atenção para alguns detalhes:

* O `scope` ali é em qual nível de _path_ o _Service Workers_ vai interceptar os _requests_. Se você colocar `/javascripts/` ele irá interceptar todos os _requests_ que tenham o _path_ "javascripts";
* Sempre precisa passar o _path_ certinho do script do Service Worker, pra não haver erro no carregamento do arquivo.

Lembrando que, ao checar a existência de Service Workers na interface do _navigator _estamos seguindo um dos conceitos pilares do PWA, que é o de _Progressive_. Se tiver suporte, ok. Se não, a aplicação continua funcionando da mesma forma, mas claro, sem as vantagens todas dessa API.

## Lifecycle de Service Workers



