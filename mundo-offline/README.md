# Mundo Offline

Hoje as aplicações _web_ são largamente usadas, e, em muitos casos, mais do que as nativas. O número de acesso a _websites_ à partir de dispositivos móveis tem crescido constantemente no mundo. Ao contrário do que se esperava, muitas dessas aplicações não possuem a mesma experiência de um aplicativo nativo. Além disso, em locais em que a disponibilidade de conexão com a internet é grande, não vemos o cuidado em desenvolver apps que sejam acessíveis em qualquer lugar.

Nessa ideia de tentar aproximar os dois mundos, _Progressive Web Apps_ surgiu. Um dos pontos mais interessantes, relacionados a esse conjunto de práticas estabelecidos de _PWA_, é o cuidado com a aplicação quando ela está em locais de difícil, ou quase nenhum acesso à _internet_ também se tornou forte.

A verdade é que, antes disso tudo acontecer, tínhamos outro conceito ganhando força, que é o do _Offline First_. Essa técnica consiste em manter o máximo de informações necessárias _offline_, para que o aplicativo web funcione sem depender das adversidades de conexão.

Nós vamos discutir aqui alguns pontos interessantes sobre esse aspecto, principalmente com uso de _APIs_ mais avançadas, como _Service Workers_, _IndexedDB_, _Cache API_, entre outras.

## **Service Workers**

_Service Workers_ é uma _API_ de _JavaScript_ capaz de intereceptar requests, atuando como um proxy, e que possue algumas funcionalidades como _Cache API_, _Push Notifications_, _Background Sync_ e, futuramente, _Bluetooth API_ e _Geofencing_.

Essa _API_ de _JavaScript_ é muito recente e está, aos poucos, sendo implementada nos _browsers_ mais atuais. Internet Explorer, Safari e Android \(versões que ainda não possuíam o Chrome instalado como um _app_\) ainda não possuem suporte. Sua aparição foi provocada devido a uma antiga _API_, _Application Cache_, que é muito difícil de lidar, principalmente porque se trata de um arquivo de texto, com as _URLs de arquivos que vão ser cacheados. Existem muitos outros pontos ruins dessa API_ que não serão tratados aqui.

Como é um _worker_, que é instalado no navegador do usuário em uma _thread_ paralela, ele não interfere na performance da aplicação na _thread_ principal, no que diz respeito à consumo de memória, _CPU_ ou _GPU_.

Nesse capítulo vamos entender como funciona a instalação e configuração de _Service Workers_ e como podemos trabalhar offline usando algumas estratégias de _cache_, usando _Cache API_.

