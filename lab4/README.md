# LAB_04 - Serviços

> Informações sobre as atividades exigidas no laboratório neste [LINK](https://github.com/santanche/component2learn/tree/master/labs/04-servicos).

## :arrow_forward: Aluno
* Rafael Mardegan Marquini

## :hammer: Conceitos, Ferramentas e Tecnologias
* Componentização
* Design Pattern: MVC
* [UML](https://www.uml.org/)
* RESTful API
* JSON
* [Insomnia](https://insomnia.rest/)

## :pencil: Tarefas

### :heavy_check_mark: Tarefa 1: Componentes de Negócio
> Delimitar partes do diagrama que deveriam estar dentro de um componente.

![Tarefa 1: Componentes de Negócio](img/tarefa1.png)


### :heavy_check_mark: Tarefa 2: Componentes Técnicos
> Separar os componentes de View daqueles definidos no Controller

![Tarefa 2: Componentes Técnicos](img/tarefa2.png)

### :heavy_check_mark: Tarefa 3: Componentes Técnicos
>  Separar os componentes do Model daqueles definidos no Controller

![Tarefa 3: Componentes Técnicos](img/tarefa3.png)

### :heavy_check_mark: Tarefa 4
>  Encontre dois serviços REST interessantes, que recebam no mínimo dois parâmetros e execute pelo menos uma consulta em cada um deles. Apresente para cada serviço que você escolheu:

#### Serviço 1: 

* **Título:** Dólar comercial (venda e compra) - cotações diárias
* **URI:**

~~~
https://olinda.bcb.gov.br/olinda/servico/PTAX/versao/v1/odata/CotacaoMoedaDia(moeda=@moeda,dataCotacao=@dataCotacao)?@moeda=%27USD%27&@dataCotacao=%2708-28-2020%27&$top=1&$orderby=dataHoraCotacao%20desc&$format=json&$select=cotacaoCompra,cotacaoVenda,dataHoraCotacao
~~~

* **Descrição:** Endpoint do Banco Central do Brasil para consulta de cotação do dólar na data informada (padrão MM-dd-yyyy), coletando o registro "top=1" e ordenado pela data e hora da última cotação de forma descendente. Na URI, é informado o tipo do formato JSON e solicito a seleção apenas dos atributos que me interessam: "cotacaoCompra", "cotacaoVenda", "dataHoraCotacao".
* **Cabeçalho HTTP da requisição:**

~~~http
GET /olinda/servico/PTAX/versao/v1/odata/CotacaoMoedaDia(moeda=@moeda,dataCotacao=@dataCotacao)?@moeda=%27USD%27&@dataCotacao=%2708-28-2020%27&$top=1&$orderby=dataHoraCotacao%20desc&$format=json&$select=cotacaoCompra,cotacaoVenda,dataHoraCotacao HTTP/1.1
Host: olinda.bcb.gov.br
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Cookie: JSESSIONID=0000Tb324Gh0bddWpGDPnE5LhFW:1cn7m3fq4; dtCookie=754EB53DEAC0F85EC09FDB113FB4E414|cHRheHwx; BIGipServer~App~upstream_was_ssl-p=1020268972.47873.0000
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
~~~

* **Cabeçalho da resposta:**

~~~http
HTTP/1.1 200 OK
Date: Sat, 29 Aug 2020 00:21:52 GMT
X-Powered-By: Servlet/3.0
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
Pragma: no-cache
Expires: 0
Strict-Transport-Security: max-age=16070400; includeSubDomains
X-Frame-Options: DENY
OData-Version: 4.0
Keep-Alive: timeout=10, max=100
Connection: Keep-Alive
Content-Type: application/json;charset=UTF-8;odata.metadata=minimal
Content-Language: en-US
~~~

* **Conteúdo da respostas (JSON)**

~~~json
{
    "@odata.context": "https://was-p.bcnet.bcb.gov.br/olinda/servico/PTAX/versao/v1/odata$metadata#_CotacaoMoedaDia(cotacaoCompra,cotacaoVenda,dataHoraCotacao)",
    "value": [
        {
            "cotacaoCompra": 5.4673,
            "cotacaoVenda": 5.4679,
            "dataHoraCotacao": "2020-08-28 13:03:36.552"
        }
    ]
}
~~~

[Mais informações sobre a utilização da API do BCB.](https://dadosabertos.bcb.gov.br/dataset/dolar-americano-usd-todos-os-boletins-diarios)

#### Serviço 2: 

* **Título:** Spotify API
* **URI:** 

~~~
https://api.spotify.com/v1/browse/categories/jazz/playlists?limit=10
~~~

* **Descrição:** Utilizando a API do Spotify foi necessário configurar um dashboard na plataforma Developer e gerar os tokens de acesso. Sendo assim, optei por buscar na categoria **Jazz** as primeiras 10 playlists.
* **Cabeçalho HTTP da requisição:**

~~~http
OPTIONS /v1/browse/categories/jazz/playlists?limit=10 HTTP/2
Host: api.spotify.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Access-Control-Request-Method: GET
Access-Control-Request-Headers: authorization
Origin: null
Connection: keep-alive
TE: Trailers
~~~

* **Cabeçalho da resposta:**

~~~http
HTTP/2 200 OK
access-control-allow-origin: *
access-control-allow-headers: Accept, App-Platform, Authorization, Content-Type, Origin, Retry-After, Spotify-App-Version, X-Cloud-Trace-Context
access-control-allow-methods: GET, POST, OPTIONS, PUT, DELETE, PATCH
access-control-allow-credentials: true
access-control-max-age: 604800
content-length: 0
strict-transport-security: max-age=31536000
x-content-type-options: nosniff
date: Sat, 29 Aug 2020 01:15:40 GMT
server: envoy
via: HTTP/2 edgeproxy, 1.1 google
alt-svc: clear
X-Firefox-Spdy: h2
~~~

* **Conteúdo da respostas (JSON)**

~~~json
{
  "playlists" : {
    "href" : "https://api.spotify.com/v1/browse/categories/jazz/playlists?offset=0&limit=10",
    "items" : [ {
      "collaborative" : false,
      "description" : "The best tunes in jazz history. Cover: John Coltrane",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DXbITWG1ZJKYt"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DXbITWG1ZJKYt",
      "id" : "37i9dQZF1DXbITWG1ZJKYt",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f0000000388b40afd9e31d92a818f355d",
        "width" : null
      } ],
      "name" : "Jazz Classics",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODY2MzE3OCwwMDAwMDAwMGQ0MWQ4Y2Q5OGYwMGIyMDRlOTgwMDk5OGVjZjg0Mjdl",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DXbITWG1ZJKYt/tracks",
        "total" : 70
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DXbITWG1ZJKYt"
    }, {
      "collaborative" : false,
      "description" : "New jazz for open minds. Cover: Soothsayers",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DX7YCknf2jT6s"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX7YCknf2jT6s",
      "id" : "37i9dQZF1DX7YCknf2jT6s",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f00000003a20cec58d7714f4e8e61c354",
        "width" : null
      } ],
      "name" : "State of Jazz",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODU2NTcyMCwwMDAwMDE1MzAwMDAwMTc0MzFmMTIwYjgwMDAwMDE3NDJhNzU1YTBl",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX7YCknf2jT6s/tracks",
        "total" : 50
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DX7YCknf2jT6s"
    }, {
      "collaborative" : false,
      "description" : "The best new releases from swinging bop to free jazz. Cover: Diana Krall",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DX85XJl1mZAlp"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX85XJl1mZAlp",
      "id" : "37i9dQZF1DX85XJl1mZAlp",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f000000035ba2a8ae6663928b18a93868",
        "width" : null
      } ],
      "name" : "Jazz X-Press",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODU2NTcyMCwwMDAwMDAyMzAwMDAwMTc0MzFmMTIwYWMwMDAwMDE3NDJlZDkzYWQx",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX85XJl1mZAlp/tracks",
        "total" : 60
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DX85XJl1mZAlp"
    }, {
      "collaborative" : false,
      "description" : "Relax to the sound of jazz.",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DWVqfgj8NZEp1"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DWVqfgj8NZEp1",
      "id" : "37i9dQZF1DWVqfgj8NZEp1",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f000000038df7fedfed909f10628586fe",
        "width" : null
      } ],
      "name" : "Coffee Table Jazz",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODQ3MDIzNCwwMDAwMDA2NDAwMDAwMTc0MmM0MDIxMTUwMDAwMDE2ZDAwY2EyYTc2",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DWVqfgj8NZEp1/tracks",
        "total" : 132
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DWVqfgj8NZEp1"
    }, {
      "collaborative" : false,
      "description" : "The best music from one of the greatest jazz labels.",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DWTR4ZOXTfd9K"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DWTR4ZOXTfd9K",
      "id" : "37i9dQZF1DWTR4ZOXTfd9K",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f00000003c5b0e400643bb009731deeca",
        "width" : null
      } ],
      "name" : "Jazz Classics Blue Note Edition",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODI4NTU1MiwwMDAwMDAyNTAwMDAwMTc0MjEzZTFhNjQwMDAwMDE3MGM0YWU2ODJj",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DWTR4ZOXTfd9K/tracks",
        "total" : 86
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DWTR4ZOXTfd9K"
    }, {
      "collaborative" : false,
      "description" : "Cosmopolitan rare grooves.",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DWUS3jbm4YExP"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DWUS3jbm4YExP",
      "id" : "37i9dQZF1DWUS3jbm4YExP",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f00000003357265e436826df390eeee94",
        "width" : null
      } ],
      "name" : "Global Funk",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODY2MzE1NSwwMDAwMDAwMGQ0MWQ4Y2Q5OGYwMGIyMDRlOTgwMDk5OGVjZjg0Mjdl",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DWUS3jbm4YExP/tracks",
        "total" : 100
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DWUS3jbm4YExP"
    }, {
      "collaborative" : false,
      "description" : "The irresistible rhythms of Latin jazz. Cover: Tito Puente",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DX661EjJOj3Tu"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX661EjJOj3Tu",
      "id" : "37i9dQZF1DX661EjJOj3Tu",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f000000035e7df2e167e0a8bb5226b428",
        "width" : null
      } ],
      "name" : "Latin Jazz",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU5ODY2MzE3NSwwMDAwMDAwMGQ0MWQ4Y2Q5OGYwMGIyMDRlOTgwMDk5OGVjZjg0Mjdl",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX661EjJOj3Tu/tracks",
        "total" : 100
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DX661EjJOj3Tu"
    }, {
      "collaborative" : false,
      "description" : "Jazz musicians perform classical composer's works. Find out why Bach was great inspiration to many jazz masters, and enjoy imaginative renditions of Chopin, Dvořák, Tchaikovsky, Stravinsky and more.",
      "external_urls" : {
        "spotify" : "https://open.spotify.com/playlist/37i9dQZF1DX2mmt7R81K2b"
      },
      "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX2mmt7R81K2b",
      "id" : "37i9dQZF1DX2mmt7R81K2b",
      "images" : [ {
        "height" : null,
        "url" : "https://i.scdn.co/image/ab67706f000000030e2eb40cc535407b24faf10c",
        "width" : null
      } ],
      "name" : "Jazz – Classical Crossings",
      "owner" : {
        "display_name" : "Spotify",
        "external_urls" : {
          "spotify" : "https://open.spotify.com/user/spotify"
        },
        "href" : "https://api.spotify.com/v1/users/spotify",
        "id" : "spotify",
        "type" : "user",
        "uri" : "spotify:user:spotify"
      },
      "primary_color" : null,
      "public" : null,
      "snapshot_id" : "MTU2OTI1NTQ5OCwwMDAwMDAxZTAwMDAwMTZkNWVlYWExMjMwMDAwMDE2ZDAwYmQ4MGZl",
      "tracks" : {
        "href" : "https://api.spotify.com/v1/playlists/37i9dQZF1DX2mmt7R81K2b/tracks",
        "total" : 49
      },
      "type" : "playlist",
      "uri" : "spotify:playlist:37i9dQZF1DX2mmt7R81K2b"
    } ],
    "limit" : 10,
    "next" : null,
    "offset" : 0,
    "previous" : null,
    "total" : 8
  }
}
~~~

---
Made with :coffee: by Rafa Mardegan.
