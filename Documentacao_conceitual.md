# <<Documentação Conceitual AFS>>


# URL (identificado por: Arlindo)

URL é o acrônimo para Uniform Resource Locator, ou Localizador Uniforme de Recursos. Trata-se de um endereço único que é atribuído a cada um dos recursos disponíveis em uma rede, como a internet. A URL é utilizada para localizar e identificar um recurso na rede, sendo que cada um deles possui uma URL única.

## Propriedades de uma URL

Fontes: https://www.ietf.org/rfc/rfc1738.txt, https://developer.mozilla.org/en-US/docs/Web/API/URL, https://axios-http.com/ptbr/docs/urlencoded

Uma URL é composta por um protocolo, um nome de domínio, um caminho, um recurso e um hash. O protocolo é o método de comunicação utilizado para acessar o recurso, como o HTTP ou o FTP. O nome de domínio é o endereço do servidor onde o recurso está localizado, como o `google.com` ou o `facebook.com`. O caminho é o local onde o recurso está localizado no servidor, como a pasta ou diretório. O recurso é o arquivo que está sendo acessado, como um documento HTML ou uma imagem. O hash é utilizado para acessar uma parte específica do recurso, como um elemento HTML ou um trecho de código.

URL também é compostas por parâmetros, que são utilizados para passar informações para o servidor. Os parâmetros são compostos por uma chave e um valor, sendo que cada parâmetro é separado por um caractere &. Por exemplo, na URL `https://www.google.com/search?q=javascript`, o único parâmetro é `q=javascript`, sendo que a chave é `q` e o valor é `javascript`. 

## URL em JavaScript

A Api URL do JavaScript é utilizada para manipular URLs. Ela fornece métodos estáticos e construtores para criar e gerenciar objetos URL, além de fornecer acesso a partes específicas de uma URL. No entanto, geralmente as URLs são construídas na mão, utilizando concatenação de strings.

### Protocolo e domínio

O protocolo e o domínio são obtidos através das propriedades protocol e hostname, respectivamente. Por exemplo, na URL `https://www.google.com/search?q=javascript`, a base URL (concatenção de protocol + hostname) é `https://www.google.com`.

### Path

O path é o caminho do recurso, sendo que ele é composto por uma sequência de diretórios e arquivos separados por uma barra (/). O path é utilizado para identificar o recurso que está sendo acessado, sendo que ele é utilizado para acessar o arquivo no servidor. Por exemplo, na URL `https://www.google.com/search?q=javascript`, o path é `/search`.

### Parâmetros

Para utilizar parâmetros em uma URL, as vezes os valores precisam ser codificados.

#### Encode/Decode

Para codificar os parâmetros, é utilizado o método encodeURI ou o método encodeURIComponent, enquanto para decodificar os parâmetros, é utilizado o método decodeURI ou o método decodeURIComponent.

## URL no Axios

Na Api Axios, o url pode ser manipulado através da propriedade baseURL, que é o endereço base do servidor, e da propriedade url, que seria o path, e da propriedade params. Mas também é possível utilizar a propriedade url para passar o endereço completo do recurso, incluindo o protocolo, o nome de domínio, o caminho do recurso.


# Requisições HTTP (identificado por: Breno, Rafael, Arlindo)

FONTES: https://www.ibm.com/docs/en/cics-ts/5.3?topic=protocol-http-requests, https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods, https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers, https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Messages

Uma solicitação HTTP é feita de client para servidor. O objetivo de uma request é acessar um recurso no servidor.

## Métodos HTTP
Os métodos HTTP especificam a ação que o cliente deseja executar em um recurso do servidor. Os principais métodos HTTP são:

* **GET**: Solicita um recurso específico do servidor. É usado para recuperar informações.
* **POST**: Envia dados para o servidor para serem processados. É comumente usado para enviar formulários ou dados de envio.
* **PUT**: Envia dados para substituir um recurso existente no servidor. É usado para atualizar completamente um recurso.
* **PATCH**: Envia dados para atualizar parcialmente um recurso existente no servidor.
* **DELETE**: Remove um recurso específico do servidor.

## Cabeçalhos HTTP 

Os headers HTTP são informações adicionais incluídas nas requisições e respostas HTTP. Eles fornecem metadados sobre a requisição ou resposta, como informações de autenticação, informações de codificação, tipos de conteúdo, entre outros.

```
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json
Authorization: Bearer token123
```

Os headers HTTP mais comuns são:

* **Content-Type**: Especifica o tipo de mídia do corpo da requisição ou resposta. Exemplos comuns incluem "application/json" para [JSON](#JSON-identificado-por-Breno-Rafael), "text/html" para HTML e "image/jpeg" para imagens JPEG.
* **Authorization**: Usado para autenticar a requisição com o servidor. Pode incluir tokens de autenticação, credenciais de usuário, chaves de api, etc.
* **Accept**: Indica os tipos de mídia aceitos pelo cliente. É usado para negociar o tipo de conteúdo preferido entre o cliente e o servidor.
* **User-Agent**: Identifica o software ou dispositivo utilizado pelo cliente para fazer a requisição.
* **Cache-Control**: Controla o comportamento de armazenamento em cache do cliente ou servidor.
* **Cookie**: Envia cookies armazenados anteriormente pelo servidor para o cliente.

## Corpo

É relacionado ao atributo Content-Types de um Header, é onde será inserido um objeto [JSON](#JSON-identificado-por-Breno-Rafael), por exemplo. Na API Axios, o Content-Type padrão é `application/json;charset=utf-8`, mas pode ser alterado para `application/x-www-form-urlencoded` ou `multipart/form-data`. Se você quiser enviar arquivos, você deve usar `multipart/form-data`, que especifica que o formulário será enviado como um conjunto de partes, uma para cada arquivo.

Exemplo de requisição usando o método PUT em que o corpo é um objeto JSON
```
PUT /api/posts/123 HTTP/1.1
Host: example.com
Content-Type: application/json
Authorization: Bearer token123

{
  "title": "Novo título do post",
  "content": "Conteúdo atualizado do post"
}
```

Exemplo de requisição usando o método POST em que o corpo é um arquivo binário (imagem jpg)
```
POST /api/files HTTP/1.1
Host: example.com
Authorization: Bearer token123
Content-Type: multipart/form-data; boundary=boundary123

--boundary123
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

<conteúdo binário do arquivo>
--boundary123--
```

# Responses HTTP (identificado por: )

FONTES: https://www.ibm.com/docs/en/cics-ts/5.2?topic=protocol-http-responses, https://www.ibm.com/docs/en/cics-ts/5.3?topic=concepts-status-codes-reason-phrases, https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status

Responses HTTP são feitas de servidor para cliente. O objetivo é fornecer ao cliente o recurso solicitado, informar ao cliente que a ação solicitada foi realizada ou informar ao cliente que ocorreu um erro no processamento de sua solicitação.

## Status Code

Os códigos de resposta HTTP são utilizados para indicar o resultado de uma requisição. Eles fornecem informações sobre o status da requisição e orientam o cliente sobre o próximo passo a ser tomado. Alguns códigos de resposta comuns são:

* **1xx**: Informacional - A requisição foi recebida e o processo continua em andamento.
* **2xx**: Sucesso - A requisição foi processada com sucesso.
  * **200 OK**: A requisição foi bem-sucedida e o resultado foi retornado conforme solicitado.
  * **201 Created**: A requisição foi bem-sucedida e um novo recurso foi criado como resultado.
  * **204 No Content**: A requisição foi bem-sucedida, mas não há conteúdo para ser retornado.
* **3xx**: Redirecionamento - O cliente precisa realizar uma ação adicional para completar a requisição.
  * **301 Moved Permanently**: O recurso solicitado foi movido permanentemente para um novo local.
* **4xx**: Erro do cliente - A requisição contém erros ou não pode ser processada pelo servidor.
  * **400 Bad Request**: A requisição contém sintaxe inválida ou não pode ser processada pelo servidor.
  * **401 Unauthorized**: A autenticação é necessária para acessar o recurso.
  * **403 Forbidden**: O servidor entende a requisição, mas se recusa a autorizá-la.
  * **404 Not Found**: O recurso solicitado não foi encontrado no servidor.
* **5xx**: Erro do servidor - O servidor encontrou um erro ao processar a requisição.
  * 500 **Internal Server Error**: O servidor encontrou um erro interno ao processar a requisição.

## Corpo

O corpo da resposta contém os dados retornados pelo servidor como resultado da requisição. Pode conter informações, mensagens de erro, conteúdo solicitado, entre outros. O tipo de conteúdo e o formato do corpo da resposta são especificados no cabeçalho da resposta.

Uma mensagem de sucesso em que o corpo é um objeto [JSON](#JSON-identificado-por-Breno-Rafael)
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "message": "Requisição bem-sucedida",
  "data": {
    "id": 123,
    "name": "John Doe"
  }
}
```

Uma mensagem de erro do cliente em que o corpo é um texto plano
```
HTTP/1.1 404 Not Found
Content-Type: text/plain

O recurso solicitado não foi encontrado.
```


# Interceptadores (identificado por: Breno, Rafael )
FONTE: https://axios-http.com/docs/interceptors

Interceptadores são códigos a serem executados parar tratar os dados de uma requisição ou resposta antes deles serem enviados pelo lado Servidor ou utilizadps pelo lado Cliente.

# Funções Assíncronas (identificado por: )
FONTES: https://www.alura.com.br/artigos/async-await-no-javascript-o-que-e-e-quando-usar

Chamamos de programação assíncrona o ato de executar uma tarefa em "segundo plano", sem nosso controle direto disso. Sem explicitamente trabalhar com threads e coordená-las.

Funções assíncronas são utilizadas frequentemente em requisições onde não precisamos esperar pela resposta da função. Dessa forma, podemos executar outras tarefas enquanto aguardamos uma resposta.

## Promessas - Promises (identificado por: Breno, )
FONTES: https://javascript.info/promise-basics

Uma promessa é um objeto retornado por uma função assíncrona, que representa o estado atual da operação.

Imagine que você é um cantor de sucesso e os fãs perguntam dia e noite pela sua próxima música.

Para obter algum alívio, você promete enviar a eles quando for publicado. Você dá uma lista aos seus fãs. Eles podem preencher seus endereços de e-mail, para que, quando a música estiver disponível, todos os inscritos a recebam instantaneamente. E mesmo que algo dê muito errado, digamos, um incêndio no estúdio, de modo que você não possa publicar a música, eles ainda serão notificados.

Todos estão felizes: você, porque o povo não te lota mais, e os fãs, porque não vão perder a música.

Esta é uma analogia da vida real para coisas que frequentemente temos na programação:

1. Um “código de produção” que faz algo e leva tempo. Por exemplo, algum código que carrega os dados em uma rede. Isso é um "cantor".

2. Um “código consumidor” que quer o resultado do “código produtor” quando estiver pronto. Muitas funções podem precisar desse resultado. Estes são os “fãs”.

3. Uma promessa é um objeto JavaScript especial que vincula o “código de produção” e o “código de consumo”. Em termos de nossa analogia: esta é a “lista de assinaturas”. O “código de produção” leva o tempo necessário para produzir o resultado prometido, e a “promessa” disponibiliza esse resultado para todo o código assinado quando estiver pronto.

A sintaxe do construtor para um objeto de promessa é:

```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (o código produtor, "cantor")
});
```

A função passada para o novo Promise é chamada de executor. Quando uma nova promessa é criada, o executor é executado automaticamente. Ele contém o código de produção que deve eventualmente produzir o resultado. Nos termos da analogia acima: o executor é o “cantor”.

Seus argumentos resolve e reject são retornos de chamada fornecidos pelo próprio JavaScript. Nosso código está apenas dentro do executor.

Quando o executor obtiver o resultado, seja cedo ou tarde, não importa, ele deve chamar um destes callbacks:

* resolve(valor) — se o trabalho for concluído com sucesso, com o valor do resultado.
* reject(error) — se ocorreu um erro, error é o objeto de erro.

Então, para resumir: o executor é executado automaticamente e tenta executar um trabalho. Ao terminar a tentativa, chama resolve se foi bem-sucedida ou reject se houve um erro.

O objeto de promessa retornado pelo novo construtor Promise tem estas propriedades internas:

* state — inicialmente "pendente", depois muda para "cumprido" quando a resolve é chamada ou "rejeitado" quando reject é chamada.
* result — inicialmente "indefinido", então muda para "valor" quando resolve(valor) é chamado ou "error" quando reject(error) é chamado.

# JSON (identificado por: Breno, Rafael) 
FONTE: https://www.w3schools.com/js/js_json_intro.asp

O termo JSON é o acrônimo para JavaScript Object Notation, sendo ele uma notação para objetos JavaScript. A notação é sintaticamente idêntica à utilizada para construção de um objeto JavaScript, mas um arquivo JSON em si não é um objeto e sim um formato de armazenamento de texto.

Em um arquivo JSON, assim como em JavaScript, objetos são delimitados por chaves e vetores são delimitados por colchetes. Os atributos de um objeto são definidos por um par de chave/valor separados por dois pontos, tendo-se tanto o nome da chave quanto o valor que ela armazena envolvidos por aspas duplas:

```JSON
{"Atributo_que_Armazena_vetor_de_objetos":[
  { "chave_1":"valor_1", "chave_2":"valor_2" },
  { "chave_1":"valor_1", "chave_2":"valor_2" },
  { "chave_1":"valor_1", "chave_2":"valor_2" }
]}
```
O formato JSON pode ser utilizado no envio de dados por requisições HTTP. Um arquivo JSON pode ser convertido para objetos em diferentes linguagens de programação com a utilização de parsers, mas a linguagem JavaScript possui a função própria `JSON.parse()` para converter um texto em formato JSON em um objeto JavaScript. Ao receber um arquivo JSON de uma requisição HTTP, basta se utilizar da função para criar um objeto JavaScript com as informações contidas no JSON:

```javascript
var object = JSON.parse(response);
```


# XHR - XMLHttpRequest (identificado por: Breno, )
FONTES: https://developer.mozilla.org/pt-BR/docs/Glossary/AJAX
https://developer.mozilla.org/pt-BR/docs/Web/API/XMLHttpRequest

O XMLHttpRequest é uma API JavaScript que permite a realização de requisições AJAX, e por consequência para receber requisições HTTP.

O termo AJAX é o acrônimo de Asynchronous JavaScript & XML, e é uma prática de programação que se utiliza do HTML, CSS, JavaScript, DOM e tanto os formatos XML e JSON para atualizar partes de uma página HTML com informações recebidas do servidor, ao invés de recarregá-la por inteiro, como ocorria antes do padrão ser criado. Com o padrão AJAX também se torna possível que a página WEB continue funcionando enquanto a parte que deve ser atualizada carrega para ser exibida de forma assíncrona.

Para utilizar a API XMLHttpRequest basta criar um objeto XMLHttpRequest, chamar o método `.open()` para definir uma URL e uma das requisições REST (GET, POST, PUT, PATCH ou DELETE), e enviar a requisição através do método `.send()`:

```javascript
const XHR =  new XMLHttpRequest();
req.open("GET", "http://www.ex.org/ex.txt",true);
req.send();
```
Após receber a resposta da requisição, armazenada no atributo`response` do objeto XMLHttpRequest, é possível, através da lógica do JavaScript, alterar um componente único da página Web que está sendo exibida.

```htmlembedded
<!DOCTYPE html>
<html>
<body onload = "loadDoc()">

<h1>The XMLHttpRequest Object</h1>

<p id="demo"></p>

<script>
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.response;
    }
  };
  xhttp.open("GET", "demo_get.asp", true);
  xhttp.send();
}
</script>
</body>
</html>
```
Ao carregar a página, o parágrafo de id "demo" irá automaticamente receber um valor que será exibido. Esse é o funcionamento por trás do padrão AJAX, que tanto o Axios quanto o XMLHttpRequest implementam. Recebendo informações formatadas em XML ou JSON por requisições HTTP, é possível atualizar, de forma assíncrona em relação à página Web como um todo, um único componente da página. Isso ocorre através da lógica do JavaScript, que é utilizada para alterar e controlar os elementos HTML que deverão ser exibidos em tela.


# Lado Cliente e lado Servidor (identificado por: )
FONTE: https://www.gta.ufrj.br/ensino/eel878/redes1-2016-1/16_1/p2p/modelo.html

O modelo Cliente-Servidor define duas pontas de comunicação, onde se tem o lado Servidor, que apenas trata requisições, armazena e fornece dados, e o lado Cliente, que apenas requisita e consome os dados fornecidos pelo lado Servidor.

# Isomorfismo (identificado por: )
FONTE: https://www.lullabot.com/articles/what-is-an-isomorphic-application

Uma aplicação isomórfica pode rodar o mesmo código tanto do lado servidor quanto do lado Cliente. Isso permite que aplicações construídas com frameworks isomórficos possam, após serem carregadas no navegador WEB, realizar requisições direto à base de dados que realiza a persistência da aplicação, sem a necessidade de requisitar dados novamente ao servidor.
# XSRF (identificado por: )

FONTE: https://en.wikipedia.org/wiki/Cross-site_request_forgery

Ataques XSRF são ataques de Cross-site Request Forgery, e ocorrem através do envio de requisições Web maliciosas por um usuário autenticado e confiável pela aplicação web, sem o conhecimento do próprio usuário de as estar enviando. Elas podem ser embutidas em e-mails, ou mesmo atributos de imagem HTML, de forma que apenas ao carregar uma página a requisição seja realizada, mesmo sem o usuário efetivamente clicar no link da requisição.

Ao enviar a requisição por um navegador Web, o mesmo automaticamente irá carregar os cookies do usuário na requisição que o autentica na aplicação, e a requisição seria então atendida pelo lado Servidor.

Formas de evitar esse tipo de ataque são o Same-Origin-Policy (SOP), no qual um navegador apenas permite uma página Web enviar requisições para outra apenas se ambas possuírem o mesmo domínio de origem: mesmo esquema de URI, mesmo número de porta e mesmo nome de host, tendo-se um controle de exceção para permitir apenas algumas requisições cruzadas entre domínios (o Cross-origin resource sharing); e ainda utilizar um token de autenticação como o XSRF-TOKEN no header de uma requisição para autenticá-la.