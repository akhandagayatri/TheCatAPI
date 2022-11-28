# TheCatAPI
**The Cat API** é uma API pública de gestão de **informações** e **imagens** de gatos, os reis da internet 🐱.  

Com nossas APIs, você pode:

1.  **Criar** novos registros;
2.  **Buscar** registros por ID;
3.  **Excluir** registros.

> ℹ️ O objeto **_images_** armazena os arquivos de gatos enviados. Imagens sem gatos ou   impróprias serão rejeitadas.

# Pré-requisitos

-   **Autenticação**: é **obrigatório** obter a **API Key**. 
Registre-se em https://thecatapi.com/signup para receber a API key por email.
Ela deve ser informada no **header** das chamadas através da variável `x-api-key.`

-   **Path de chamadas**: utilizar o path [https://api.thecatapi.com/v1](https://api.thecatapi.com/v1)

# Endpoints

Conheça cada endpoint, as formas de requisição e os exemplos de *response body*. 🐾

## POST/images/upload

https://api.thecatapi.com/v1/images/upload

Este endpoint **cria** uma nova imagem quando é informado um arquivo **válido** do tipo:

-   .gif    
-   .jpg    
-   .png    

(*) O **file** é um _body param_  **obrigatório**.

> ⛔ **Imagens sem gatos ou impróprias serão rejeitadas.**

### Exemplo de requisição:

``` json 
curl -X 'POST' \
POST 'https://api.thecatapi.com/v1/images/upload' \
--header 'x-api-key: live_w10RexaKpMeFam5ubRnZZ4hHui6WWajbHQ95pWkGkZsch9kAxa6nSodlPSJ5PnBj' \
--form 'file=@"7iDTcrCER/Cat-100.jpeg"'
```

![201-Created](https://user-images.githubusercontent.com/27686944/204299738-5dfb178e-0c50-4bc1-b5d2-c5cba44fedfb.jpeg)

> 😻 A resposta de código `201 Created` indica que o arquivo da imagem foi criado com sucesso. Ela retorna um JSON com as informações, incluindo o novo `Id`.

### Exemplo de response body:
``` json 
{
    "id": "N40r_E3J-",
    "url": "https://cdn2.thecatapi.com/images/N40r_E3J-.jpg",
    "width": 750,
    "height": 600,
    "original_filename": "Cat-100.jpeg",
    "pending": 0,
    "approved": 1
}
```
## GET/images

https://api.thecatapi.com/v1/images?limit=1

Este endpoint busca **todas** as imagens enviadas para sua conta via `/images/upload.`

(*) O `limit` é um _path param_  **obrigatório**.

Para **limitar** o retorno, use estes _**query params**_:

| Parâmetro	 | Descrição |  Tipo | Obrigatório |
|--|--|--|--|
| `limit` | Número de resultados a serem retornados. O valor máximo é 25. O valor padrão é 1. | `integer` | **Sim**
| `mime_types` | Tipos de imagem a serem retornados: .gif, .jpg, ou .png. O padrão é retornar todos os tipos. | `string` delimitado por vírgulas. | Sim
| `order` | Ordem de retorno: RANDOM, ASC ou DESC. O padrão é RANDOM. | integer | Não

### Exemplo de requisição:

``` json 
curl --location --request 
GET 'https://api.thecatapi.com/v1/images?limit=3' \ 
--header 'x-api-key: live_w10RexaKpMeFam5ubRnZZ4hHui6WWajbHQ95pWkGkZsch9kAxa6nSodlPSJ5PnBj'
```

![200-OK-reduc](https://user-images.githubusercontent.com/27686944/204300801-4c2dd4bb-509a-4fe3-8f24-951f39150728.jpeg)


> 😻 A resposta de código `200 OK` indica que a consulta foi executada com sucesso. Ela retorna um JSON com todas as informações da imagem.

### Exemplo de response body:

``` json 
[
  {
    "breeds": [],
    "id": "N40r_E3J-",
    "url": "https://cdn2.thecatapi.com/images/N40r_E3J-.jpg",
    "width": 750,
    "height": 600,
    "sub_id": null,
    "created_at": "2022-11-26T15:14:36.000Z",
    "original_filename": "Cat-100.jpeg",
    "breed_ids": null
  }
]
```

## GET/images/{image_id}

https://api.thecatapi.com/v1/images/6nd1mD1zw

Este endpoint **busca** a imagem correspondente ao _**path param**_  `image_id`.

(*) O `image_id` é um _path param_  **obrigatório**.

### Exemplo de requisição:

``` json 
curl --location --request 
GET 'https://api.thecatapi.com/v1/images/6nd1mD1zw' \ 
--header 'x-api-key: live_w10RexaKpMeFam5ubRnZZ4hHui6WWajbHQ95pWkGkZsch9kAxa6nSodlPSJ5PnBj'
```
![200-OK-reduc](https://user-images.githubusercontent.com/27686944/204300864-71bca146-bcaa-435c-9b59-d8e9cfc1a232.jpeg)


> 😻 A resposta de código `200 OK` indica que a consulta foi executada com sucesso. Ela retorna um JSON com todas as informações da imagem.

### Exemplo de response body:

``` json 
[
  {
    "breeds": [],
    "id": "N40r_E3J-",
    "url": "https://cdn2.thecatapi.com/images/N40r_E3J-.jpg",
    "width": 750,
    "height": 600,
    "sub_id": null,
    "created_at": "2022-11-26T15:14:36.000Z",
    "original_filename": "Cat-100.jpeg",
    "breed_ids": null
  }
]
```

## DEL/images/{image_id}

https://api.thecatapi.com/v1/images/6nd1mD1zw

Este endpoint **exclui** o registro correspondente ao _**path param**_  `image_id`.

(*) O `image_id` é um _path param_  **obrigatório**.

### Exemplo de requisição:

``` json 
curl --location --request 
DELETE 'https://api.thecatapi.com/v1/images/6nd1mD1zw' \ 
--header 'x-api-key: live_w10RexaKpMeFam5ubRnZZ4hHui6WWajbHQ95pWkGkZsch9kAxa6nSodlPSJ5PnBj'
```
![204-No Content-reduc](https://user-images.githubusercontent.com/27686944/204301141-50031ac7-ad10-4e9f-8ce7-2872c7fc5cb8.jpeg)


> 😻 A resposta de código `204 No Content` indica que a exclusão foi executada com sucesso. Ela retorna um JSON vazio.

> ℹ️ Para confirmar a exclusão do registro, execute o GET /images/{image_id}.

***
😹  *"O tempo gasto com gatos nunca é tempo perdido"*. - Sigmund Freud
