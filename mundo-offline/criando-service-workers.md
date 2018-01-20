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

Lembrando que, ao checar a existência de _Service Workers_ na interface do _navigator_ estamos seguindo um dos conceitos pilares do PWA, que é o de _Progressive_. Se tiver suporte, ok. Se não, a aplicação continua funcionando da mesma forma, mas claro, sem as vantagens todas dessa API.

## Lifecycle de Service Workers

Quando registramos um Service Worker no browser, alguns eventos acontecem, e eles podem ser facilmente interceptados por listeners. Os eventos que ocorrem são:

1- install;  
2- waiting;  
3- activate;  
4- fetch.

### Install

Esse evento acontece logo quando um _Service Worker_ é registrado num _client_. _Client,_ aqui, é a página que registrou o mesmo. Você pode ter mais de uma página sendo _client_ do mesmo _Service Worker_, desde que obedeçam as regras de segurança, como estar no mesmo_ scope_ de _path_, mesmo domínio e https.

No evento de _install_, geralmente fazemos o setup de tudo que é básico para nossa aplicação funcionar. É aí que podemos adicionar scripts comuns para seu _app_, assets no geral e tudo que é essencial pra que as coisas funcionem, da forma mais mínima possível.

Um exemplo do evento _install_:

```js
self.addEventListener('install', (event) => {
  console.log('instalando Service Worker...');

  event.waitUntil(
    caches.open('version-1').then(cache => cache.add('logo.svg'))
  );
});
```

\*logo veremos um pouco mais sobre algo que veio junto com _Service Workers_, que é a _Cache API._

### Waiting

Dentro da variável _event,_ retornada pelo listener do evento de _install_, é possível utilizar uma _Promise_ que só retorna o _status_ de _installed_ assim que ela for resolvida. Como visto no exemplo anterior do evento _install_, é possível somente retornar que o _Service Worker_ foi instalado depois que a _Promise_ interna do _waitUntil_ for resolvida. Dessa forma podemos fazer o "_setup_" de coisas internas da nossa aplicação, antes de começar a interceptar os _requests_ ou _pushes_. No exemplo acima, adicionamos o "logo.svg" à "version-1" do _cache_.

É importante ressaltar que, o _waitUntil_ está disponível dentro dos _listeners_ de _install_ _e fetch,_ permitindo-nos controlar quando esses eventos vão retornar e avisar o _browser_ que estão resolvidos.

### Activate

Assim que o evento de install é finalizado, o evento _activate_ é disparado.



