<div style="text-align: center;"><h1> Axios </h1> </div>

## Introdução
Axios é uma biblioteca cliente HTTP baseado-em-promessas para o node.js e para o navegador. É isomórfico, ou seja, pode rodar no navegador e no node.js com a mesma base de código. No lado do servidor usa o código nativo do node.js - o modulo http, enquanto no lado do cliente (navegador) usa XMLHttpRequests.

## Features

Além de possibilitar a realização de requisições, o Axios traz algumas vantagens, como por exemplo:
* Suporte para navegadores mais antigos;
* Tratamento simples de erros;
* Interceptação de respostas;
* Suporte a Promises;
* Conversão automática de dados em JSON;
* Tem suporte a falsificação de solicitações entre sites, conhecido como XRSF.

## Começando a utilizar o Axios

O principal propósito do Axios é permitir a realização de requisições para diferentes APIs. Então nessa sessão, iremos mostrar um simples exemplo de como consumir uma API externa.

### Instalação

Utilizando o npm:

```shell
$ npm install axios
```

Utilizando o bower:

```shell
$ bower install axios
```

Utilizando o yarn:

```shell
$ yarn add axios
```

Utilizando a CDN do jsDelivr:

```javascript
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

Utilizando a CDN do unpkg:

```javascript
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### Configuração do projeto

Em seguida, crie um projeto **React**.

Para organizar melhor o nosso projeto, vamos criar um arquivo chamado **api.js**, que vai ser responsável por toda a configuração e importação da biblioteca **axios**.

Crie uma pasta dentro da pasta raiz do projeto chamada **services/** e dentro dela um arquivo chamado **api.js**.

O código do arquivo **api.js** deve seguir o seguinte modelo:

```javascript
import axios from "axios"; // importa o axios da biblioteca.

const api = axios.create({ // cria e atribui a variavel "api", que é onde será armazenada a API que iremos consumir.
  baseURL: "https://api.minha-api.com", // URL da API que será acessada.
});

export default api; // exportamos nossa variável apipara ser importada em qualquer parte do nosso projeto.
```

Note que as API's precisam ser definidas dentro desse arquivo, seguindo o modelo demonstrado acima.

### Utilizando o Axios

Com a nossa API criada com Axios, vamos abrir o arquivo principal **app.js** e importá-la.

```javascript
import React, { useEffect, useState } from "react";
import api from "./services/api"; // "api.js" sendo importado, nos dando acesso a nossa API definida no arquivo.

export default function App() {
  const [user, setUser] = useState();

  return (
    <div className="App">
      <p>Usuário: {user?.login}</p>
      <p>Biografia: {user?.bio}</p>
    </div>
  );
}
```

No exemplo de código acima, estamos tentando acessar dois atributos (**login** e **bio**) de um usuário (**user**). Esses usuário será retornado através de uma requisição HTTP que faremos através do Axios.

Vamos adicionar a requisição ao trecho de código acima.

```javascript
import React, { useEffect, useState } from "react";
import api from "./services/api"; // "api.js" sendo importado, nos dando acesso a nossa API definida no arquivo.

export default function App() {
  const [user, setUser] = useState();
    
  useEffect(() => {
    api
      .get("/users/usuario-exemplo") // solicita um GET no usuário desejado.
      .then((response) => setUser(response.data)) // caso a solicitação retorne um valor, atribui o valor a "user".
      .catch((err) => { // caso a solicitação retorne um erro, trata o erro da maneira desejada.
        console.error("ops! ocorreu um erro" + err);
      });
  }, []);

  return (
    <div className="App">
      <p>Usuário: {user?.login}</p> 
      <p>Biografia: {user?.bio}</p>
    </div>
  );
}
```

A execução desse código deve renderizar uma página HTML com o "**login**" e a "**bio**" do usuário retornado pela requisição exibidos na tela.

Vale notar que os verbos mais comuns para requisições HTTP são: GET, POST, DELETE e PUT. E para cada verbo, o Axios possui um método com o mesmo nome, como vemos no trecho a seguir:

```javascript
// Verbo GET
 api.get(endpoint)

// Verbo POST
 api.post(endpoint, dados)


// Verbo DELETE
 api.delete(endpoint, dados)

// Verbo PUT
 api.put(endpoint, dados)
```


# Conceitos de Domínio
## URL (identificado por: Arlindo, Brian)

URL é o acrônimo para Uniform Resource Locator, ou Localizador Uniforme de Recursos. Trata-se de um endereço único que é atribuído a cada um dos recursos disponíveis em uma rede, como a internet. A URL é utilizada para localizar e identificar um recurso na rede, sendo que cada um deles possui uma URL única.

### Propriedades de uma URL

Uma URL é composta por um protocolo, um nome de domínio, um caminho, um recurso e um hash. O protocolo é o método de comunicação utilizado para acessar o recurso, como o HTTP ou o FTP. O nome de domínio é o endereço do servidor onde o recurso está localizado, como o `google.com` ou o `facebook.com`. O caminho é o local onde o recurso está localizado no servidor, como a pasta ou diretório. O recurso é o arquivo que está sendo acessado, como um documento HTML ou uma imagem. O hash é utilizado para acessar uma parte específica do recurso, como um elemento HTML ou um trecho de código.

URL também é compostas por parâmetros, que são utilizados para passar informações para o servidor. Os parâmetros são compostos por uma chave e um valor, sendo que cada parâmetro é separado por um caractere &. Por exemplo, na URL `https://www.google.com/search?q=javascript`, o único parâmetro é `q=javascript`, sendo que a chave é `q` e o valor é `javascript`. 

### URL em JavaScript

A Api URL do JavaScript é utilizada para manipular URLs. Ela fornece métodos estáticos e construtores para criar e gerenciar objetos URL, além de fornecer acesso a partes específicas de uma URL. No entanto, geralmente as URLs são construídas na mão, utilizando concatenação de strings.

#### Protocolo e domínio

O protocolo e o domínio são obtidos através das propriedades protocol e hostname, respectivamente. Por exemplo, na URL `https://www.google.com/search?q=javascript`, a base URL (concatenção de protocol + hostname) é `https://www.google.com`.

#### Path

O path é o caminho do recurso, sendo que ele é composto por uma sequência de diretórios e arquivos separados por uma barra (/). O path é utilizado para identificar o recurso que está sendo acessado, sendo que ele é utilizado para acessar o arquivo no servidor. Por exemplo, na URL `https://www.google.com/search?q=javascript`, o path é `/search`.

#### Parâmetros

Para utilizar parâmetros em uma URL, as vezes os valores precisam ser codificados.

#### Encode/Decode

Para codificar os parâmetros, é utilizado o método encodeURI ou o método encodeURIComponent, enquanto para decodificar os parâmetros, é utilizado o método decodeURI ou o método decodeURIComponent.

### URL no Axios

Na Api Axios, o url pode ser manipulado através da propriedade baseURL, que é o endereço base do servidor, e da propriedade url, que seria o path, e da propriedade params. Mas também é possível utilizar a propriedade url para passar o endereço completo do recurso, incluindo o protocolo, o nome de domínio, o caminho do recurso.



## Requisições e respostas HTTP (identificado por: Arlindo, Breno, Brian, Rafael)


Como apresentado em seções anteriores, o protocolo HTTP permite a comunicação entre clientes e servidores de uma aplicação; para tal, ações são realizadas por ambas as partes, podendo elas serem classificadas como requisições (_requests_) ou respostas (_responses_) HTTP.

A principal característica que difere uma requisição de uma resposta é a sua direção de destino: enquanto nas requisições há o envio de mensagem do cliente para o servidor, nas respostas temos o oposto, com o servidor enviando uma mensagem ao cliente. Uma requisição busca o acesso a um recurso provido por um servidor, sendo o papel deste validar a solicitação e gerar uma resposta contendo o resultado almejado (ou não) da requisição, que então é enviado ao cliente.

```http
PATCH /objectserver/restapi/alerts/status HTTP/1.1
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Content-Type: application/json
Host: localhost
Connection: keep-alive
Content-Length: 1092

{
	"rowset": {
		"coldesc": [
			{
				"type": "integer",
				"name": "Acknowledged"
			},
			{
				"type": "string",
				"name": "Location"
			},
			{
				"type": "integer",
				"name": "OwnerUID"
			},
			{
				"type": "integer",
				"name": "OwnerGID"
			},
			{
				"type": "utc",
				"name": "LastOccurrence"
			}
		],
		"rows": [
			{
				"Location": "UPDATED",
				"LastOccurrence": 1341412235,
				"Acknowledged": 1,
				"OwnerUID": 65534,
				"OwnerGID": 1
			}
		]
	}
}
```
<p style="text-align: center;">Requisição HTTP. Fonte: IBM</p>

Nas requisições, o cliente utiliza componentes de uma URL (_Uniform Resource Locator_), que inclui as informações necessárias para o acesso de determinado recurso. Ela é composta por três partes distintas que, juntas, determinam o recurso do servidor a ser acessado, sendo elas, a saber:

1. **A linha de requisição (_request line_)**, obrigatória, onde é apresentado o método de requisição, seu destino (uma URL ou caminho absoluto) e a versão do protocolo HTTP a ser utilizada. Os componentes foram separados por um espaço em branco (" ");

```http
PATCH /objectserver/restapi/alerts/status HTTP/1.1
```
<p style="text-align: center;">Trecho da linha de requisição. Fonte: IBM</p>

2. **Headers HTTP**, definidos visando fornecer ao destinatário informações sobre a mensagem, seu remetente e a maneira pela qual este deseja se comunicar com o recebedor da requisição; e

```http
Accept: application/json
Authorization: Basic dGVzdHVzZXIwMTpuZXRjb29s
Content-Type: application/json
Host: localhost
Connection: keep-alive
Content-Length: 1092
                                                    // linha vazia
```
<p style="text-align: center;">Headers de uma requisição. Fonte: IBM</p>

3. **O corpo da mensagem (_body_)**, se necessário. Também conhecido como corpo da entidade (_entity body_), ele pode ser considerado conteúdo real da mensagem, ao mesmo tempo que é considerado inapropriado para alguns dos métodos de requisição, como o método `GET`. No trecho destacado abaixo, temos um corpo de mensagem formatado conforme o tipo definido no header `Content-Type`, `application/json`.

```http
{
	"rowset": {
		"coldesc": [
			{
				"type": "integer",
				"name": "Acknowledged"
			},
			{
				"type": "string",
				"name": "Location"
			},
			{
				"type": "integer",
				"name": "OwnerUID"
			},
			{
				"type": "integer",
				"name": "OwnerGID"
			},
			{
				"type": "utc",
				"name": "LastOccurrence"
			}
		],
		"rows": [
			{
				"Location": "UPDATED",
				"LastOccurrence": 1341412235,
				"Acknowledged": 1,
				"OwnerUID": 65534,
				"OwnerGID": 1
			}
		]
	}
}
```
<p style="text-align: center;">Corpo da mensagem de uma requisição. Fonte: IBM</p>

A estrutura das respostas HTTP se assemelha a das requisições, com a seguinte ressalva: substituímos a linha de requisição por uma **linha de status**, que guarda, respectivamente, a versão do protocolo HTTP utilizada, o código status de resposta à requisição (_response status code_) e a frase de status (_reason phrase_). Assim como na linha de requisição, os componentes foram separados por um espaço em branco.

```http
HTTP/1.1 200 OK 					// <------ Linha de status
Cache-Control: no-cache
Server: libnhttpd
Date: Wed Jul 4 15:32:03 2012
Connection: Keep-Alive:
Content-Type: application/json;charset=UTF-8
Content-Length: 158

{
	"entry":	{
		"affectedRows": 10,
		"uri": "http://localhost/objectserver/restapi/alerts/status"
	}
}
```

<p style="text-align: center;">Resposta HTTP à requisição. Fonte: IBM</p>

### Métodos HTTP

Os métodos HTTP especificam a ação que o cliente deseja executar em um recurso do servidor. Os principais métodos HTTP são:

* **GET**: Solicita um recurso específico do servidor. É usado para recuperar informações.
* **POST**: Envia dados para o servidor para serem processados. É comumente usado para enviar formulários ou dados de envio.
* **PUT**: Envia dados para substituir um recurso existente no servidor. É usado para atualizar completamente um recurso.
* **PATCH**: Envia dados para atualizar parcialmente um recurso existente no servidor.
* **DELETE**: Remove um recurso específico do servidor.

## Status de Resposta à Requisição HTTP (identificado por: Breno, Rafael)


Responses HTTP são feitas de servidor para cliente. O objetivo é fornecer ao cliente o recurso solicitado, informar ao cliente que a ação solicitada foi realizada ou informar ao cliente que ocorreu um erro no processamento de sua solicitação.

### Status Code

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


## Funções de Middleware/Interceptadores (identificado por: Breno, Rafael)


Antes que entremos nas _funções_ de _middleware_, devemos compreender o significado de **_middleware_**.

Quando empregado na engenharia de _software_, _middleware_ pode ser entendido como uma camada intermediária entre dois aplicativos, agindo como um "tradutor oculto" e possibilitando a comunicação e o gerenciamento de dados para aplicativos distribuídos. Essa definição pode ser encontrada no Dicionário da Computação na Nuvem da Azure, Microsoft.

Agora, ao buscarmos entender o que seriam as **funções** de _middleware_, nos deparamos com uma aplicação do conceito orientada para a manipulação dos objetos de solicitação e de resposta a uma requisição; na Axios, onde elas são conhecidas como _interceptors_ (interceptadores), esse tipo de função nos permite personalizar o comportamento de uma chamada HTTP ou reposta recebida após requisição realizada a outro servidor. Há a possibilidade de adicionarmos uma lógica personalizada à aplicação, como a criação de log ou validação da mensagem recebida ou a adição de _headers_ HTTP à mensagem a ser enviada.

```javascript 
// Manipulando o objeto de solicitação antes que seja realizada a requisição
axios.interceptors.request.use(function (config) {
  // Você pode adicionar lógica à aplicação aqui

  return config;
}, function (erro) {
  // Há, também, a possibilidade de manipular a captura de erro ocorrida em requisição

  return Promise.reject(error);
});

// Manipulando o objeto de resposta após seu recebimento
axios.interceptors.response.use(function (response) {
  // Você pode adicionar lógica à aplicação aqui

  return response;
}, function (erro) {
  // A requisição não teve sucesso? O erro é capturado aqui

  // Há, também, a possibilidade de manipular o objeto de erro
  return Promise.reject(error);
});
```

## JSON (identificado por: Arlindo, Breno, Rafael)


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


## XHR - XMLHttpRequest (identificado por: Arlindo, Breno, Brian)


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



## Lado Cliente e lado Servidor (identificado por: Rafael)


O modelo Cliente-Servidor define duas pontas de comunicação, onde se tem o lado Servidor, que apenas trata requisições, armazena e fornece dados, e o lado Cliente, que apenas requisita e consome os dados fornecidos pelo lado Servidor.



## Isomorfismo (identificado por: Brian)


Uma aplicação isomórfica pode rodar o mesmo código tanto do lado servidor quanto do lado Cliente. Isso permite que aplicações construídas com frameworks isomórficos possam, após serem carregadas no navegador WEB, realizar requisições direto à base de dados que realiza a persistência da aplicação, sem a necessidade de requisitar dados novamente ao servidor.



## XSRF (identificado por: Brian)

Ataques XSRF são ataques de Cross-site Request Forgery, e ocorrem através do envio de requisições Web maliciosas por um usuário autenticado e confiável pela aplicação web, sem o conhecimento do próprio usuário de as estar enviando. Elas podem ser embutidas em e-mails, ou mesmo atributos de imagem HTML, de forma que apenas ao carregar uma página a requisição seja realizada, mesmo sem o usuário efetivamente clicar no link da requisição.

Ao enviar a requisição por um navegador Web, o mesmo automaticamente irá carregar os cookies do usuário na requisição que o autentica na aplicação, e a requisição seria então atendida pelo lado Servidor.

Formas de evitar esse tipo de ataque são o Same-Origin-Policy (SOP), no qual um navegador apenas permite uma página Web enviar requisições para outra apenas se ambas possuírem o mesmo domínio de origem: mesmo esquema de URI, mesmo número de porta e mesmo nome de host, tendo-se um controle de exceção para permitir apenas algumas requisições cruzadas entre domínios (o Cross-origin resource sharing); e ainda utilizar um token de autenticação como o XSRF-TOKEN no header de uma requisição para autenticá-la.

## Cenários de Uso

## Realizar requisições HTTP

### 1. Realizar operações CRUD em um servidor

O Axios permite que você faça operações CRUD em um servidor. Para isso, você pode utilizar os métodos `axios.get()`, `axios.post()`, `axios.put()` e `axios.delete()` e passar como parâmetro a URL do servidor e um objeto com os dados que você deseja enviar. 

Veja exemplos abaixo:

```js
// GET
const res1 = await axios.get('/usuarios')
// POST
const res2 = await axios.post('/usuarios', {
  nome: 'José',
  idade: 31
})
// PUT
const res3 = await axios.put('/usuarios/1', {
  nome: 'José',
  idade: 31
})
// DELETE
const res4 = await axios.delete('/usuarios/1')
```

No exemplo, axios.get('/usuarios') faz uma requisição GET para a rota '/usuarios', axios.post('/usuarios') faz uma requisição POST para a rota '/usuarios' com os dados do usuário a serem criados, axios.put('/usuarios/1') faz uma requisição PUT para a rota '/usuarios/1' para atualizar os dados do usuário com o ID 1, e axios.delete('/usuarios/1') faz uma requisição DELETE para a rota '/usuarios/1' para deletar o usuário com o ID 1.

### 2. Obter a resposta das operações

No passo anterior as requisições ficam guardadas em uma variável que aguarda o retorno do método. Após a promise ser cumprida é possivel acessar o corpo de uma response através do atributo `.data`.

Veja o exemplo abaixo:

```js
const res1 = await axios.get('/usuarios/1')
const nomeDeUsuario = res.data.username
```

No exemplo acima, axios.get('/usuarios/1') faz uma requisição GET para a rota '/usuarios/1', e a resposta é armazenada na variável res1. Em seguida, o nome de usuário é acessado através de res1.data.username.

Lembrando que é importante envolver o código em um bloco `try/catch` para tratar erros e evitar que o programa quebre. Veja a sessão [Tratar mensagens de erro](#1-tratar-erros) para mais info.

Outra forma de ser feito sem precisar de uma função assíncrona é utilizando o método `.then()`.

```js
axios.get('/usuarios/1')
    .then((res)=>{
        setNomeUsuario(res.data.username)
    })
/* .catch((error)=>{ ... }) */
/* aqui você pode usar .catch() ao invés de try/catch para tratar erros */
```

## Cancelar uma chamada de API

Basicamente, você precisa criar um **token de cancelamento** e passa ao **construtor** da requisição. Algo assim:

```javascript
const CancelToken = axios.CancelToken;

// Criamos a origem do token de cancelamento:
const cancelTokenSource = CancelToken.source();

axios.get('/path/of/request', {
  // Passamos o token de cancelamento para o construtor da requisição:
  cancelToken: cancelTokenSource.token
});
```

Note que `cancelTokenSource` (retornado pela aplicação de `CancelToken.source`) possui uma propriedade `token` (que é o token de cancelamento), mas também possui um método `cancel`, que deve ser usado para cancelar a requisição. Você pode utilizá-lo passando um motivo para o cancelamento:

```javascript
cancelTokenSource.cancel('Não é mais de meu interesse enviar esta requisição.');
```

Uma vez que o `cancel` seja invocado, a `Promise` que o construtor da requisição retorna será rejeitada. Você poderá, então, utilizar o `catch` para tratar essa rejeição:

```javascript
axios.get('/path/of/request', {
  // Passamos o token de cancelamento para o construtor da requisição:
  cancelToken: cancelTokenSource.token
}).catch(function (thrown) {
  // Utilizamos o método `isCancel` para saber se o erro da rejeição veio de um cancelamento:
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
    // Trate o erro.
  }
});
```

Como a rejeição é notificada através da rejeição da promessa, não há problemas em tratá-la com `async`/`await`:

```javascript
async function doRequest() {
  try {
    const response = axios.get('/path/of/request', {
      // Passamos o token de cancelamento para o construtor da requisição:
      cancelToken: cancelTokenSource.token
    });

    // Faça algo com `response`.
  } catch (thrown) {
    if (axios.isCancel(thrown)) {
      console.log('Request canceled', thrown.message);
    } else {
      // Trate o erro.
    }
  }
}
```

## Repetição de chamadas de API com interceptadores

Em certas situações, pode ser necessário lidar com erros de rede ou outras condições que exijam a repetição de uma chamada de API. O Axios fornece uma funcionalidade chamada Interceptors, que nos permite interceptar e modificar as requisições e respostas antes de serem tratadas pela aplicação.

Vamos ver um exemplo de como utilizar os Axios Interceptors para repetir uma chamada de API automaticamente em caso de erro.

```javascript
// Utilizando axios
import axios from "axios";

// Definindo um interceptor para requisições
axios.interceptors.request.use((config) => {
  // Aqui você pode adicionar lógica para modificar a requisição, se necessário
  return config;
}, (error) => {
  // Aqui você pode tratar erros de requisição, se necessário
  return Promise.reject(error);
});

// Definindo um interceptor para respostas
axios.interceptors.response.use((response) => {
  // Aqui você pode adicionar lógica para modificar a resposta, se necessário
  return response;
}, (error) => {
  // Aqui você pode tratar erros de resposta, se necessário
  if (error.response && error.response.status === 503) {
    // Exemplo de repetição da chamada em caso de erro 503 (Service Unavailable)
    return axios(error.config);
  }
  return Promise.reject(error);
});

// Fazendo a chamada de API
axios.get('https://api.example.com/data')
  .then((response) => {
    console.log('Dados recebidos:', response.data);
  })
  .catch((error) => {
    console.error('Erro na chamada de API:', error);
  });
```

Neste exemplo, definimos um interceptor para requisições utilizando `axios.interceptors.request.use` e um interceptor para respostas utilizando `axios.interceptors.response.use`. Dentro desses interceptors, podemos adicionar a lógica personalizada necessária.

No interceptor de requisições, podemos modificar a configuração da requisição antes que ela seja enviada. No interceptor de respostas, podemos modificar a resposta antes que ela seja tratada pela aplicação.

No exemplo, estamos lidando com um possível erro 503 (Service Unavailable). Se recebermos essa resposta de erro, utilizamos `axios(error.config)` para repetir automaticamente a chamada de API.

É importante mencionar que os Axios Interceptors são flexíveis e podem ser utilizados para diversos fins, como adicionar cabeçalhos personalizados, manipular tokens de autenticação, realizar tratamento de erros globais, entre outros.

Utilizando os Axios Interceptors, é possível personalizar e controlar o fluxo das chamadas de API de acordo com as necessidades específicas da sua aplicação.


## Implementar um indicador de progresso

Imagine que você tem um app front end que faz upload de arquivos para um servidor. Você quer acompanhar e mostrar ao usuário o progresso do envio desses arquivos.

Isso é possível e fácil de implementar utilizando o Axios.

Vamos como codar essa funcionalidade.

```javascript
 // Utilizando axios
	   import axios from axios;

	   // Criando um FormData que armazena a imagem (arquivo)
	   const data = new FormData();
	   data.append("file", file, filename);
  
	   // Fazendo a requisição para o servidor com método POST
	   // Enviando o arquivo que está na variável data
	   // Passando um objeto de configuração que possui um método onUploadProgress
      axios
        .post("https://my.server.com/posts", data, {
          onUploadProgress: (event) => {
            let progress: number = Math.round(
              (event.loaded * 100) / event.total
            );

            console.log(
              `A imagem ${filename} está ${progress}% carregada... `
            );  
          },
        })
        .then((response) => {
          console.log(
            `A imagem ${filename} já foi enviada para o servidor!`
          );    
        })
        .catch((err) => {
          console.error(
            `Houve um problema ao realizar o upload da imagem ${filename} no servidor AWS`
          );
          console.log(err); 
        });
```

Basicamente é realizado uma requisição do tipo **POST** utilizando o **Axios**, passando a variável `data`, com o arquivo. Passamos também um objeto com a configuração da requisição. Nele contém o método `onUploadProgress` que recebe um `event`, esse `event` contém as propriedades `loaded` e `total`.

`loaded` é o quanto já foi carregado e `total` armazena o tamanho total do arquivo.

Então é feito um cálculo de regra de três para definir a percentagem que já foi carregada no servidor. A variável `progress` armazena esses valores conforme a função `onUploadProgress` é executada automaticamente.

Como estamos lidando com uma **Promises**, no final da execução o método **Then** é executado e conseguimos informar que o arquivo já foi enviado.

Se houver algum erro, o método **Catch** é executado, assim podemos imprimir no log o erro.

## Manipular headers de requests


Axios permite que você intercepte requests e responses, o que pode ser útil para anexar um header de autorização em todas as requests. Para isso, você pode utilizar o método `axios.interceptors.request.use()` e passar como parâmetro uma função que recebe como parâmetro a configuração da request e retorna a configuração da request ou um erro.

Veja um exemplo abaixo:

```js
axios.interceptors.request.use(
  config => {
    // Caso a configuração da request não possua um header de autorização
    // anexa um header de autorização com o token do usuário
    if (!config.headers['Authorization']) {
      config.headers['Authorization'] = `Bearer ${token}`
    }
    return config
  }
)
```

Esse exemplo intercepta a configuração de uma requisição e verifica se a configuração possui um header de autorização. Caso não possua, anexa um header de autorização com o token do usuário. O que pode ser útil para garantir que todas as requests possuam um header de autorização.

Outra abordagem é inicializando uma instância do axios método `axios.create()` e passar como parâmetro um objeto com as configurações que você deseja personalizar, o que também pode ser usado para anexar um header de autorização em todas as requests.

Veja um exemplo abaixo:

```js
const instanciaAxios = axios.create({
  headers: {
    'Authorization': `Bearer ${token}`
  }
})

const res = await instanciaAxios.get('/rota-protegida')
```

Esse exemplo cria uma instância do Axios com um header de autorização anexado. O que pode ser útil para garantir que todas as requests possuam um header de autorização.

## Tratar erros em Responses

### 1. Tratar erros

O Axios possui mecanismos para lidar com diferentes tipos de erros retornados pelo servidor.

Quando uma requisição retorna um status de erro, o Axios irá lançar uma exceção. Essa exceção pode ser capturada usando um bloco try...catch ou através do método catch no final da cadeia de promessas.

Veja um exemplo de tratamento de erro usando try...catch:

```js
try {
  // Caminho bom
  const res = await axios.get('/usuarios/1')
  setNomeUsuario(res.data.username)
} catch (err) {
  // Trate o erro
  console.error(err)
} // finally{ ... }
```

No exemplo acima, a requisição GET é feita para obter os dados do usuário com ID 1. Se a requisição for bem-sucedida, o nome de usuário é acessado através de response.data.username. Caso ocorra um erro, a exceção é capturada no bloco catch e você pode tratar o erro de acordo com suas necessidades.

Outra forma de tratar o erro é usando o método catch:

```js
axios.get('/usuarios/1')
  .then((res) => {
    // Caminho bom
    setNomeUsuario(res.data.username)
  })
  .catch((err) => {
    // Trate o erro
    console.error(err)
  })
  // .finally(()=>{ ... })
```

Nesse exemplo, o método catch é chamado quando ocorre um erro na requisição. O erro é passado como argumento para a função de tratamento de erro, onde você pode realizar as operações desejadas, como exibir uma mensagem de erro ou registrar o erro em um sistema de monitoramento.

### A1. Manipular mensagens de erro em todas as responses

Axios permite que você intercepte requests e responses, o que pode ser útil para manipular mensagens de erro numa response. Para isso, você pode utilizar o método `axios.interceptors.response.use()` e passar como parâmetro uma função que recebe como parâmetro a response e retorna a response ou um erro.

Veja um exemplo abaixo:

```js
axios.interceptors.response.use(
  response => {
    // Caso a resposta seja bem-sucedida, retorna a resposta sem alterações
    return response
  },
  error => {
    if (error.response.status === 400) {
      const errorMessage = error.response.data.message || 'Dados inválidos.';
      throw new Error(errorMessage)
    } else if (error.response.status === 401) {
      const errorMessage = error.response.data.message || 'Você não possui permissão para acessar esse recurso.'
      throw new Error(errorMessage)
    } else if (error.response.status === 404) {
      const errorMessage = error.response.data.message || 'Recurso não encontrado.';
      throw new Error(errorMessage)
    } else {
      throw new Error('Ocorreu um erro na requisição.')
    }
  }
)
```

Esse exemplo intercepta a resposta de uma requisição e verifica o status da resposta. Se o status for 400, 401 ou 404, uma mensagem de erro é lançada. Caso contrário, uma mensagem genérica é lançada. O que pode ser útil para exibir mensagens de erro no front-end de forma mais amigável ao usuário.

### A2. Você deseja capturar todos os erros para salvar num arquivo de log ou enviar para um serviço de monitoramento de erros

Para capturar erros, você pode utilizar o método `axios.interceptors.response.use()` e passar como parâmetro uma função que recebe como parâmetro um objeto com a resposta da requisição.

Veja um exemplo abaixo:

```js
axios.interceptors.response.use(
  response => {
    // Caso a resposta seja bem-sucedida, retorna a resposta sem alterações
    return response
  },
  error => {
    // Aqui você pode salvar o erro num arquivo de log
    // ou enviar para um serviço de monitoramento de erros como o Sentry
    Sentry.captureException(error)

    // Propaga o erro para que seja tratado em outro ponto do código
    throw error
  }
)
```

## Realizar upload de arquivos

Para lidar com arquivos por meio do Axios, é necessário utilizar bibliotecas de formulário, enviando o arquivo pela requisição HTTP dentro de um objeto formulário, e para isso se utiliza da biblioteca `FormData`. Criando uma instância  do `FormData`, se adiciona o arquivo no formulário pelo método `.append(nome_do_campo,valor, nome_do_arquivo)`: 

```js
const FormData = require('form-data');

// Cria uma nova instancia de FormData
const form = new FormData();

// O `arquivo` pode ser um Blob ou Stream
//O terceiro argumento, o nome do arquivo, é essencial
form.append('CampoImagem', arquivo, 'imagem.jpg');
```


Um objeto Blob é um arquivo armazenado em forma de binário, sendo uma forma de armazenamento bem comum de arquivos. Ao recuperar um arquivo em disco com o método `fs.readFile()` se obtém um objeto Blob, por exemplo. Para lidar com esse tipo de objeto no NodeJS é possível utilizar um parser, como o [multer](https://github.com/expressjs/multer). Assim, no front-end o objeto Blob é passado:

```js
const formData = new FormData();
const imagefile = fs.readFile("./imagem/imagem.jpg");

formData.append("fileimage", arquivo, imagem.jpg);
axios.post("http://localhost:xxx/imagem-upload",formData,{
  headers: {
  "Content-Type": `multipart/form-data;
  boundary=${formData._boundary}`,
  }
}).then(response => console.log(response));
```
É obrigatório declarar no Header da requisição o Content-Type como `multipart/form-data`, e o "boundary", ou seja, a forma como o formulário divide sua chave e valor. A forma mais segura de declarar o boundary é `boundary=$formData._boundary`, pois dessa forma é pego o símbolo próprio do formulário que divide os pares de chave e valor do mesmo. 

Quando o NodeJS recebe a requisição, utilizando o framework do Axios, é necessário ainda o `multer` para tratar o objeto Blob e armazená-lo corretamente no parâmetro `req` da requisição, o acessando pelo atributo `req.file`:

```js
const multer = require("multer");

let upload = multer();

// O campo 'fileimage' será a chave que o multer irá 
// procurar pelo arquivo de imagem.
app.post("/imagem-upload", upload.single('fileimage'),
(req, res) => {
  console.log(req.body);
  console.log(req.file);
res.status(200).json({ message: "success!" });
});
```
É também possível fazer upload de um arquivo na forma de um Stream, direto no corpo da requisição, sem necessitar do `multer` no back-end para realizar o parse:

```js
const fileStream = fs.createReadStream('./arquivo.zip');

const form = new FormData();
// Passa o arquivo stream direto ao formulário
form.append('largeFile', fileStream, 'large-file.zip');
```

Dessas formas é possível fazer upload de um arquivo para o servidor com o Axios.

## Autenticar em um Servidor

Para realizar a autenticação em um servidor, o framework Axios possui o parâmetro `auth`, que pode ser passado na requisição para realizar uma autenticação básica (Basic Auth). Ao ser utilizado esse parâmetro, as informações já são encodadas em base64 quando a requisição é realizada

```js
const user = await axios.post(BASE_URL+
'/users', data, { auth: {
  username: USERNAME,
  password: PASSWORD
}})
```
É possível realizar a autenticação também de uma forma mais "manual", criando o authToken (um token de acesso que nada mais é que a combinação do nome de usuário e sua senha) e o encodando em base64 sem a ajuda do Axios, e ainda assim o enviar por uma requisição que utiliza o framework:

```js
const token = `${USERNAME}:${PASSWORD}`;
const encodedToken = Buffer.from(token).toString('base64');
const headers = { 'Authorization': 'Basic '+ encodedToken };

const user = await axios.post(BASE_URL+'/users', data, { headers })
```

Também é possível configurar um auth_token nas configurações globais do Axios e utilizá-lo em todas as requisições: 
```js
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;`
```

## Configurar um timeout para uma chamada de API


O parâmetro timeout define um tempo limite para uma requisição ficar sem resposta antes de abortá-la.

É possível definir um tempo padrão com o parâmetro em uma instância Axios, e posteriormente a sobrescrevê-la em alguma requisição específica:

```js
// Cria uma instancia pelo "config defaults" do framework Axios.
//  Na criação o timeout é 0 por padrão
const instance = axios.create();

// sobrescreve o timeout padrão, 
// de forma que as requisições usando a instância esperarão
//  2.5 segundos antes de serem abortadas
instance.defaults.timeout = 2500;

// Sobrescreve o timeout padrão para esta requisição específica
instance.get('/longRequest', {
  timeout: 5000
});
```

É também possível utilizar o método `timeout()` para abortar requisições o combinando com o método`abortSignal`:

```js
axios.get('/foo/bar', {
   signal: AbortSignal.timeout(5000)
//Aborta a requisição após 5 segundos
}).then(function(response) {
   //...
});

```