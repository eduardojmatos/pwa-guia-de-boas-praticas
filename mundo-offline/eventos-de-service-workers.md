## Eventos do Service Workers

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

Assim que o evento de _install_ é finalizado, o evento _activate_ é disparado. Um _Service Worker_ entra no estado _active_ no _client_ quando esse evento é resolvido. Dizemos "resolvido", pois o _event.waitUntil_ espera retornarmos uma _Promise_.

