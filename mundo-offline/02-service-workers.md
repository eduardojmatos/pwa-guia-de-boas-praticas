# Service Workers

Assim como os _Web Workers_, o _Service Worker_ é um _JavaScript_ que "instalamos" no browser do usuário. Ele trabalha em uma camada entre o _browser_ e o servidor, interceptando cada _request_ que o usuário fizer. Dessa forma, podemos decidir se vamos trazer os arquivos do armazenamento local ou se vamos diretamente no servidor. Esse poder de decisão é o grande trunfo do Service Workers. Como vimos com o ApplicationCache, isso não era possível.

Abaixo, um gráfico mostrando aonde _Service Workers_ atua.

![](/assets/Screen Shot 2018-01-27 at 16.04.05.png)

Junto com _Service Workers_ surgiu a _Cache API_, uma interface inteligente pra armazenarmos arquivos no _browser_. Nos próximos exemplos veremos como ela funciona e quais as estratégias podemos utilizar pra controlar arquivos localmente.

# Criando Service Workers

Para criar um _Service Worker_ é necessário um arquivo com todos os _handlers_ de eventos que usaremos. Antes disso, precisamos registrar o arquivo do _Service Worker_ criado, no cliente, que no caso é a página visitada.

```js
// no local da sua aplicação principal

// Checando se existe o Service Worker no browser do usuário
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js', { scope: '/' }).then((registration) => {
    console.log(`Registration success in ${registration.scope} and the status is ${registration.state}`);
  }).catch((error) => console.log(`Errors happened... ${error}`));
} else {
  console.log('Service Worker is not working on your browser :(');
}
```

Dessa forma, já é possível saber se o registro do arquivo foi feito. Mas atenção para alguns detalhes:

* O `scope` ali é em qual nível de _path_ o _Service Workers_ vai interceptar os _requests_. Se você colocar `/javascripts/` ele irá interceptar todos os _requests_ que tenham o _path_ "javascripts";
* Sempre precisa passar o _path_ certinho do script do Service Worker, pra não haver erro no carregamento do arquivo.

Lembrando que, ao checar a existência de _Service Workers_ na interface do _navigator_ estamos seguindo um dos conceitos pilares do PWA, que é o de _Progressive_. Se tiver suporte, ok. Se não, a aplicação continua funcionando da mesma forma, mas claro, sem as vantagens todas dessa API.

## Estado de um Service Worker

Quando fazemos uma operação de registro, no retorno da _Promise_, temos a interface _Service Worker Registration_ disponível. Esse objeto possui algumas propriedades e métodos que nos permitem saber o status do registro do worker, controlar o momento de atualização dele e um _handler_ de evento pra saber quando um _worker_ novo está sendo instalado.

No retorno da _Promise_ do método _register_ podemos conferir o status da seguinte forma:

```js
navigator.serviceWorker.register('/sw.js', { scope: '/' }).then((registration) => {
  console.log(`Registration success in ${registration.scope} e o status é ${registration.state}`);
}).catch((error) => console.log(`Errors happened... ${error}`));
```

## 



