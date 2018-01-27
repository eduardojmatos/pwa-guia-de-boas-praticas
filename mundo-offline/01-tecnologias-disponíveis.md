# Tecnologias Disponíveis

O que é possível fazer hoje nos _browsers_, para casos em que a conexão com a internet ou está indisponível, ou tem uma qualidade baixíssima, como é o caso de vários lugares aqui no Brasil? Temos diversas _APIs_ disponíveis para trabalhamos nesses cenários, como _Application Cache_, _Local Storage_, _IndexedDB_, _Service Workers_, entre outras. Vamos estudar nesse guia as principais e as que nos ajudarão a deixar nossa aplicação progressiva, seguindo os conceitos de _PWA_.

Existem 2 tipos de armazenamento offline nos browsers, os de arquivo e os de dados, e vamos ver, com detalhes, as possibilidades nesses dois tipos.

## Armazenamento de arquivos offline

Para armazenarmos arquivos no browser do usuário, temos 2 APIs de JavaScript disponíveis: _Application Cache_ e _Cache API_. Esse guia não contemplará a fundo a _Application Cache API_, por já ser uma API _deprecated_, o que significa que os browsers, em algum momento, irão parar de dar suporte para a mesma, e até removê-la, como o Firefox recentemente decidiu fazer. Apenas por curiosidade, vamos ver um exemplo de como essa _API_ funciona. O foco é estudarmos _Service Workers_, já que até mesmo o [Safari](https://developer.apple.com/library/content/releasenotes/General/WhatsNewInSafari/Articles/Safari_11_1.html) e o [iOS 11.3](https://webkit.org/blog/8084/release-notes-for-safari-technology-preview-48/) irá suportar essa API - algo aguardado com ansiedade pra quem desenvolve front-end.

### Application Cache

Para armazenar arquivos offline, usando _AppCache_, basta termos um arquivo com a extensão "_.appcache_", listando a _URL_ dos arquivos que queremos armazenar no browser. O arquivo precisa seguir o seguinte formato:

```markdown
<!DOCTYPE html>
<html manifest="files.appcache">
  <head>
    <meta charset="utf-8" />
    <title>AppCache test</title>
    <link rel="stylesheet" href="offline.css">
    <script src="update-cache.js"></script>
  </head>
  <body>
    <img src="images/offline-image.png" />
    <button id="update-cache">Update cache!</button>
  </body>
</html>
```

E o arquivo "_files.appcache_" ficaria da seguinte forma:

```
CACHE MANIFEST
index.html
images/offline-image.png
offline.css
update-cache.js
```

Se visualizarmos o _Developer Tools_ do _Chrome_, vamos perceber alguns _logs_ que aparecem, como na imagem abaixo:

![](/assets/Screen Shot 2018-01-27 at 15.43.21.png)

Quando visitamos novamente a página, os _logs_ mudam:

![](/assets/Screen Shot 2018-01-27 at 15.44.16.png)

E se desabilitarmos o acesso à internet, dentro da aba _Network_, podemos ver que a página continua funcionando:

![](/assets/Screen Shot 2018-01-27 at 15.44.59.png)

_Application Cache_ é a forma mais simples de armazenarmos arquivos. O grande problema dessa API é controlar as atualizações e adição de novos arquivos. Podemos somente forçar a atualização via JavaScript, pois o _Application Cache_ tem uma interface onde é possível fazer essas atualizações via script.

```js
const checkStatus = (status) => {
  console.log('ApplicationCache is:', status);

  if (status === window.applicationCache.UPDATEREADY) {
    window.applicationCache.swapCache();
  }

  if (status === window.applicationCache.IDLE) {
    console.log('updating you cache in 3 seconds');

    setTimeout(() => {
      window.location.reload();
    }, 3000);
    return;
  }

  setTimeout(() => {
    checkStatus(window.applicationCache.status);
  }, 250);
};

/*
 * Updating cache event
 */
const updateCacheButton = document.querySelector('#update-cache');

updateCacheButton.addEventListener('click', (event) => {
  window.applicationCache.update();
  checkStatus(window.applicationCache.status);
});
```

O método _applicationCache.update\(\)_ força a atualização do _cache_ no _browser_ do usuário. Esse método apenas força o _download_ novamente de todos os arquivos que estão no manifesto. Pra que o cache seja de fato atualizado é necessário chamar o método _applicationCache.swapCache\(\)_. Os _logs_ ficam da seguinte forma, com esse _JavaScript_ acima, usado como exemplo:

![](/assets/Screen Shot 2018-01-27 at 15.45.51.png)

Se trocamos o logo, ou alterarmos algo, tanto no CSS, como na imagem ou no HTML, esse método renova a página. Quando o status do _ApplicationCache_ fica _IDLE_ \(que equivale ao número 1 ali no _log_\), podemos forçar um _reload_ automático da página, via _window.location.reload\(\)_.

### Problemas com o ApplicationCache

Como percebemos aqui, a grande dificuldade de trabalhar com _ApplicationCache_ é a gestão de arquivos que queremos armazenar no _browser_ do usuário. Se quisermos adicionar um arquivo novo para ser cacheado, precisamos adicioná-lo na lista do manifesto e forçar uma atualização no browser, como no _script_ demonstrado anteriormente.



