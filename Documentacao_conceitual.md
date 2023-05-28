# <<Documentação Conceitual AFS>>

# HTTP
# Parâmetros de URL
# Funções Assíncronas
# Promessas (Promises)
# Requisições HTTP
# Interceptadores (Middlewares)
# JSON

O termo JSON é o acrônimo para JavaScript Object Notation, sendo ele uma notação para objetos JavaScript. A notação é sintaticamente idêntica à utilizada para construção de um objeto JavaScript, mas um arquivo JSON em si não é um objeto e sim um formato de armazenamento de texto.

Em um arquivo JSON, assim como em JavaScript, objetos são delimitados por chaves e vetores são delimitados por colchetes. Os atributos de um objeto são definidos por um par de chave/valor separados por dois pontos, tendo-se tanto o nome da chave quanto o valor que ela armazena envolvidos por aspas duplas:

```
{"Atributo_que_Armazena_vetor_de_objetos":[
  { "chave_1":"valor_1", "chave_2":"valor_2" },
  { "chave_1":"valor_1", "chave_2":"valor_2" },
  { "chave_1":"valor_1", "chave_2":"valor_2" }
]}
```

O formato JSON pode ser convertido para objetos em diferentes linguagens de programação com a utilização de parsers, mas a linguagem JavaScript possui a função própria `JSON.parse()` para converter um texto em formato JSON em um objeto JavaScript.

O formato JSON pode ser utilizado no envio de dados por requisições HTTP


# XHR
# Isomorfismo
# Lado Cliente e lado Servidor
# XSRF

## Ataques XSRF
## Prevenção a ataques XSRF do Axios