# Mundo Offline

Hoje as aplicações _web_ são largamente usadas, e, em muitos casos, mais do que as nativas. O número de acesso a _websites_ à partir de dispositivos móveis tem crescido constantemente no mundo. Ao contrário do que se esperava, muitas dessas aplicações não possuem a mesma experiência de um aplicativo nativo. Além disso, em locais em que a disponibilidade de conexão com a internet é grande, não vemos o cuidado em desenvolver apps que sejam acessíveis em qualquer lugar.

Nessa ideia de tentar aproximar os dois mundos, _Progressive Web Apps_ surgiu. Um dos pontos mais interessantes, relacionados a esse conjunto de práticas estabelecidos de _PWA_, é o cuidado com a aplicação quando ela está em locais de difícil, ou quase nenhum acesso à _internet_ também se tornou forte.

A verdade é que, antes disso tudo acontecer, tínhamos outro conceito ganhando força, que é o do _Offline First_. Essa técnica consiste em manter o máximo de informações necessárias _offline_, para que o aplicativo web funcione sem depender das adversidades de conexão.

Nós vamos discutir aqui alguns pontos interessantes sobre esse aspecto, principalmente com uso de _APIs_ mais avançadas, como _Service Workers_, _IndexedDB_, _Cache API_, entre outras.

## **Service Workers**

Service Workers é uma API de JavaScript capaz de intereceptar requests, atuando como um proxy, e que possue algumas funcionalidades como Cache API, Push Notifications, Background Sync e, futuramente, Bluetooth API e Geofencing.



Essa API de JavaScript é muito recente e está, aos poucos, sendo implementada nos browsers mais atuais. Internet Explorer, Safari e Android \(versões que ainda não possuíam o Chrome instalado como um app\) ainda não possuem suporte.



Como é um worker, que é instalado no navegador do usuário em uma thread paralela, ele não interfere na performance da aplicação na thread principal, no que diz respeito à consumo de memória, CPU ou GPU.



Nesse capítulo vamos entender como funciona a instalação e configuração de Service Workers e como podemos trabalhar offline usando algumas estratégias de cache, usando Cache API. M

undo Offline

Hoje as aplicações web são largamente usadas, e, em muitos casos, mais do que as nativas. O número de acesso a websites à partir de dispositivos móveis tem crescido constantemente no mundo. Ao contrário do que se esperava, muitas dessas aplicações não possuem a mesma experiência de um aplicativo nativo. Além disso, em locais em que a disponibilidade de conexão com a internet é grande, não vemos o cuidado em desenvolver apps que sejam acessíveis em qualquer lugar.



Nessa ideia de tentar aproximar os dois mundos, Progressive Web Apps surgiu. Um dos pontos mais interessantes, relacionados a esse conjunto de práticas estabelecidos de PWA, é o cuidado com a aplicação quando ela está em locais de difícil, ou quase nenhum acesso à internet também se tornou forte.



A verdade é que, antes disso tudo acontecer, tínhamos outro conceito ganhando força, que é o do Offline First. Essa técnica consiste em manter o máximo de informações necessárias offline, para que o aplicativo web funcione sem depender das adversidades de conexão.



Nós vamos discutir aqui alguns pontos interessantes sobre esse aspecto, principalmente com uso de APIs mais avançadas, como Service Workers, IndexedDB, Cache API, entre outras.



Service Workers

Service Workers é uma API de JavaScript capaz de intereceptar requests, atuando como um proxy, e que possue algumas funcionalidades como Cache API, Push Notifications, Background Sync e, futuramente, Bluetooth API e Geofencing.



Essa API de JavaScript é muito recente e está, aos poucos, sendo implementada nos browsers mais atuais. Internet Explorer, Safari e Android \(versões que ainda não possuíam o Chrome instalado como um app\) ainda não possuem suporte.



Como é um worker, que é instalado no navegador do usuário em uma thread paralela, ele não interfere na performance da aplicação na thread principal, no que diz respeito à consumo de memória, CPU ou GPU.



Nesse capítulo vamos entender como funciona a instalação e configuração de Service Workers e como podemos trabalhar offline usando algumas estratégias de cache, usando Cache API.



