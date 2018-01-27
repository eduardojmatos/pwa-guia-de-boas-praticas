# Mundo Offline

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
  </head>
  <body>
    <img src="imagem-offline.jpg" />
  </body>
</html>
```



