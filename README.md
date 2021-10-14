![](https://github.com/caiohscruz/pokedex-vue-formacao-nodejs/blob/master/public/app.gif?raw=true)

## :computer: Projeto

Uma pokédex simples desenvolvida com VueJS, os dados dos pokémons são obtidos via requisição para uma API REST [PokéApi](https://pokeapi.co). Realizei o deploy da aplicação na Heroku, confira: [pokedex (vue-poke-api.herokuapp.com)](https://vue-poke-api.herokuapp.com/)

## :satellite: De onde?

Este é o quarto projeto do curso [Formação NodeJS](https://www.udemy.com/course/formacao-nodejs/).

## :books: Aprendizado

A proposta do projeto era bem simples:
- obter dados da PokeAPI (REST API);
- listar os pokémons na tela;
- incluir um botão para trocar a sprite de cada pokemon;
- um mecanismo de busca por nome, mas a forma como o professor implementou retornava apenas um pokemon, isso se fosse informado o nome dele da forma como foi armazenado no sistema, considerando maiúsculas e minúsculas.

Dentre as alterações que fiz, destacaria:
- mudei o mecanismo de busca para que retorne pokémons até com trechos de nome, ignorando a diferença entre maiúsculas e minúsculas, fazendo o uso de toUpperCase e regex;
- inclui a opção de filtrar por tipo, os botões para tal são incluídos dinamicamente conforme os cards vão sendo carregados pela primeira vez, de forma que só há opções de filtro correspondentes aos tipos dos pokemons que foram carregados da API;

Dentre as novidades, eu destacaria, fora trabalhar com o próprio VueJS, ter conhecido o framework Bulma, que é uma alternativa ao Bootstrap, e aprender a realizar o deploy de aplicações VueJS.

## :rocket:Tecnologias

Esse projeto foi desenvolvido com as seguintes tecnologias:

- HTML
- CSS
- Bulma
- JavaScript
- VueJS
- NodeJS
- Express
- Axios
- Serve-Static
