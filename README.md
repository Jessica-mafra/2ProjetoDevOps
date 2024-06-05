Projeto Prático: Configuração e Otimização do Servidor NGINX
2º Projeto Prático - DevOps
Configuração e Otimização do Servidor NGINX
Desafio
Configure e otimize um servidor NGINX para atuar como servidor web, proxy reverso e gateway de API. O projeto deve focar em otimização de desempenho, implementação de HTTPS, configuração de regras de proxy reverso e gerenciamento de servidores web seguros.

Etapas
a. Configuração Básica: Configure o NGINX para atuar como servidor web para um site ou aplicativo.

b. Proxy Reverso: Configure regras de proxy reverso para direcionar o tráfego para diferentes serviços ou aplicativos.

c. Segurança e HTTPS: Implemente HTTPS com certificados SSL/TLS e configure políticas de segurança.

d. Otimização de Desempenho: Aplique técnicas de otimização para melhorar o desempenho do NGINX.

e. Documentação: Documente a configuração e as decisões tomadas durante o projeto.

Começando

Pré-requisitos

Nesse projeto foi utilizado o esquema de container Docker, devido a sua facilidade de uso e desempenho.

[Nginx](https://www.nginx.com/) - O servidor web usado
[Docker](https://www.docker.com/) - Software utilizado

Instalação

Siga estas etapas para configurar o ambiente de desenvolvimento:

- Configure o arquivo docker-compose para receber a imagem do servidor nginx para que possamos trabalhar com ele dentro do container.
- Crie o arquivo de configuração do servidor nginx.
- Após todas as configurações, suba o container usando o comando: 

```bash
# Subindo container docker
  docker-compose up -d
  sudo apt-get install docker-ce
```

Você pode verificar se o container está ativo usando o comando:
```bash
  docker ps
```
 Implantação
Para implantar o servidor em um sistema ativo, siga as práticas recomendadas de segurança e monitore o desempenho regularmente.

Baseado nos conceitos de servidor e, em particular, no NGINX, foram utilizados conceitos de proxy reverso, solicitações HTTP e HTTPS, balanceamento de carga e estrutura de microserviços.

Nginx
NGINX é um servidor web open source de alta performance que entrega conteúdo estático de forma rápida e fácil de configurar. Ele oferece recursos de balanceamento de carga, proxy reverso e streaming, além de gerenciar milhares de conexões simultâneas, resultando em maior velocidade e escalabilidade.

Proxy Reverso
Um proxy reverso é um servidor que fica na frente dos servidores web e encaminha as solicitações dos clientes (por exemplo, navegadores web) para esses servidores. Os proxies reversos ajudam a aumentar a segurança, o desempenho e a confiabilidade. No projeto, o proxy reverso é utilizado para analisar o conteúdo conforme as regras de negócio definidas antes de encaminhá-lo aos servidores.

Solicitações HTTP e HTTPS
O HTTP é um protocolo para transferência de texto que permite a comunicação com um servidor web. Inicialmente, ele servia apenas para "pegar" conteúdo de um servidor, mas com o tempo, passou a ser usado também para enviar informações ao servidor. No entanto, o HTTP transmite dados em texto claro, o que pode expor informações sensíveis.

Para solucionar esse problema, foi criado o HTTPS, que usa criptografia de chaves para garantir que apenas o usuário final possa ler as informações transmitidas. Isso é especialmente importante para proteger dados confidenciais durante a transmissão. O HTTPS criptografa os dados, tornando-os seguros contra interceptações.

Certificado OpenSSL
Para simular a segurança de um site, utilizamos certificados OpenSSL, garantindo a segurança das informações transmitidas entre os servidores. Ao adicionar um certificado configurado ao host do site, transformamos um site HTTP não seguro em um site HTTPS seguro. O ícone de cadeado no navegador indica que o site está protegido por HTTPS.

Ao gerar um certificado autoassinado e configurá-lo em um projeto, indicamos ao cliente que o site é confiável. Protocolos como TLS e SSL envolvem o tráfego normal em pacotes criptografados, permitindo que servidores enviem informações com segurança sem que mensagens sejam interceptadas ou lidas por terceiros. Para mais informações sobre como gerar um certificado OpenSSL, consulte SSL Dragon.

Balanceamento de Carga
Quando um usuário faz requisições ao servidor, o proxy reverso distribui essas requisições entre os servidores. Se as requisições fossem distribuídas igualmente entre servidores de diferentes capacidades, o desempenho seria prejudicado. O balanceamento de carga resolve esse problema ao configurar a quantidade de requisições que cada servidor pode receber, garantindo que servidores mais potentes recebam mais requisições e servidores menos potentes recebam menos. Isso otimiza os recursos disponíveis e melhora o desempenho geral do sistema.

Estrutura do Projeto
Este projeto segue uma arquitetura baseada em microserviços, onde cada funcionalidade é dividida em módulos independentes. Essa abordagem facilita a manutenção, escalabilidade e desenvolvimento de novas funcionalidades.

Estrutura de Diretórios

A estrutura do projeto está organizada da seguinte maneira:

```
├── conf.d
├── estrutura_projeto.txt
├── html
│   ├── erro
│   │   ├── index.css
│   │   ├── index.html
│   │   └── index.js
│   ├── index.html
│   └── teste
│       └── index.html
├── index.html
├── load-balancer.conf
├── mime.types
├── nginx.conf
├── noticias.conf
├── novidades.conf
└── servidores
    └── microservicos
        ├── html
        │   └── index.html
        ├── noticias
        │   ├── html
        │   │   ├── erro
        │   │   │   ├── index.css
        │   │   │   ├── index.html
        │   │   │   └── index.js
        │   │   ├── index.html
        │   │   └── teste
        │   │       └── index.html
        │   └── index.html
        ├── noticias.conf
        ├── novidades
        │   ├── html
        │   │   ├── erro
        │   │   │   ├── index.css
        │   │   │   ├── index.html
        │   │   │   └── index.js
        │   │   ├── index.html
        │   │   └── teste
        │   │       └── index.html
        │   └── index.html
        └── novidades.conf
```

Descrição dos Diretórios e Arquivos

- `conf.d`: Diretório para arquivos de configuração gerais.
- `estrutura_projeto.txt`: Arquivo de texto contendo a descrição da estrutura do projeto.
- `html`: Diretório raiz para arquivos HTML.
  - `erro`: Contém arquivos relacionados a páginas de erro.
    - `index.css`: Folha de estilo CSS para a página de erro.
    - `index.html`: Página de erro principal.
    - `index.js`: Script JavaScript para a página de erro.
  - `teste`: Contém arquivos HTML para testes.
    - `index.html`: Página HTML de teste.
  - `index.html`: Página HTML principal do projeto.
- `index.html`: Página HTML principal na raiz do projeto.
- `load-balancer.conf`: Arquivo de configuração do balanceador de carga.
- `mime.types`: Arquivo de tipos MIME.
- `nginx.conf`: Arquivo de configuração do servidor Nginx.
- `noticias.conf`: Arquivo de configuração específico para o microserviço de notícias.
- `novidades.conf`: Arquivo de configuração específico para o microserviço de novidades.
- `servidores`: Diretório para servidores e microserviços.
  - `microservicos`: Diretório contendo os diferentes microserviços.
    - `html`: Contém a página HTML do microserviço.
      - `index.html`: Página HTML do microserviço.
    - `noticias`: Diretório do microserviço de notícias.
      - `html`: Contém arquivos HTML específicos do microserviço de notícias.
        - `erro`: Contém arquivos de erro específicos do microserviço de notícias.
          - `index.css`: Folha de estilo CSS para a página de erro.
          - `index.html`: Página de erro do microserviço de notícias.
          - `index.js`: Script JavaScript para a página de erro.
        - `index.html`: Página HTML principal do microserviço de notícias.
        - `teste`: Contém arquivos HTML de teste para o microserviço de notícias.
          - `index.html`: Página HTML de teste do microserviço de notícias.
      - `index.html`: Página HTML principal do microserviço de notícias.
      - `noticias.conf`: Arquivo de configuração do microserviço de notícias.
    - `novidades`: Diretório do microserviço de novidades.
      - `html`: Contém arquivos HTML específicos do microserviço de novidades.
        - `erro`: Contém arquivos de erro específicos do microserviço de novidades.
          - `index.css`: Folha de estilo CSS para a página de erro.
          - `index.html`: Página de erro do microserviço de novidades.
          - `index.js`: Script JavaScript para a página de erro.
        - `index.html`: Página HTML principal do microserviço de novidades.
        - `teste`: Contém arquivos HTML de teste para o microserviço de novidades.
          - `index.html`: Página HTML de teste do microserviço de novidades.
      - `index.html`: Página HTML principal do microserviço de novidades.
      - `novidades.conf`: Arquivo de configuração do microserviço de novidades.

Configuração e Deploy
Configuração
Servidor Nginx:

Configure o arquivo nginx.conf com as definições básicas do servidor.
Inclua os arquivos de configuração dos microserviços (noticias.conf, novidades.conf) no arquivo principal nginx.conf ou no diretório conf.d.
Balanceador de Carga:

Configure o arquivo load-balancer.conf para definir as regras de balanceamento de carga entre os microserviços.
Tipos MIME:

Configure o arquivo mime.types para suportar todos os tipos de conteúdo que serão servidos pelo servidor.

 Deploy

Estrutura de Diretórios:

Garanta que todos os diretórios e arquivos estejam organizados conforme a estrutura descrita acima.
Configurações dos Microserviços:

Cada microserviço deve possuir sua própria configuração (noticias.conf, novidades.conf) e ter seus arquivos HTML, CSS e JavaScript organizados nos diretórios apropriados.
Iniciar o Servidor:

Utilize os comandos adequados para iniciar o servidor Nginx e assegurar que todas as configurações sejam carregadas corretamente.
Manutenção
A estrutura modular do projeto facilita a manutenção, permitindo que alterações em um microserviço específico não afetem os outros. Para realizar atualizações ou corrigir bugs, siga estas etapas:

Identificação do Microserviço:

Localize o microserviço que necessita de manutenção na estrutura de diretórios.
Aplicação das Alterações:

Realize as modificações necessárias nos arquivos de configuração ou no código-fonte do microserviço.
Testes:

Execute testes nos microserviços alterados para garantir que as mudanças não introduzam novos bugs.
Deploy das Alterações:

Após validar as alterações, implemente as mudanças no ambiente de produção.

Ferramentas utilizadas no projeto:

* [Nginx](https://www.nginx.com/) - O servidor web usado.
* [Docker](https://www.docker.com/) - Software utilizado.
* [Openssl](https://sadique.io/blog/2012/06/05/managing-security-certificates-from-the-console-on-windows-mac-os-x-and-linux/) - Ferramenta para gerar certificado.



