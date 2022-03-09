# Desafio Front-End GOAT

## Status do desafio

__FINALIZADO__

## Começando
- Faça um fork deste repositório.
- Run `npm install` para instalar as dependencias do projeto.
- Run `npm run dev` para rodar o projeto.
- Run `npm run serve` para rodar o JSON server (simulador da API Rest)

## Requisitos
- Desenvolver um projeto de gerenciamento de usuários (CRUD), consumindo dados da API especificada logo abaixo.
  - Listar Usuários: __GET__ `/usuarios` obtém todos os usuários.
  - Buscar Usuário: __GET__ `/usuarios/1` obtém o usuário cujo id é 1.
  - Criar Usuário: __POST__ `/usuarios` adiciona um usuário à coleção.
  - Editar Usuário: __PUT__ `/usuarios/1` edita o usuário cujo id é 1.
  - Excluir Usuário: __DELETE__ `/usuarios/1` deleta o usuário cujo id é 1. 

## Extras (Não obrigatórios, mas será visto como um diferencial)
- Utilizar máscaras nos campos dos formulários.
- Utilizar alguma biblioteca de componentes, preferencialmente Vuetify. 
- Utilizar Vuex para gerenciamento de estado.
- Realizar testes unitários.
- Caso deseje usar mais de uma página utilizar Vue Router para gerenciamento de rotas.  
- Caso deseje, você pode adicionar dependências ou outros recursos que julgar necessário em seu código.
    
## API a ser consumida (Exemplo)
O JSON abaixo que simula o banco fica localizado no arquivo `db.json` dentro do projeto, configurado com o JSON server e deve ser utilizado para realizar as requisições do seu projeto.

```json
"usuarios": [
        {
            "id": 1,
            "nome": "Quin Travis",
            "matricula": "2864687",
            "email": "ut.pharetra@goat.com",
            "cpf": "37445653007"
        },
        {
            "id": 2,
            "nome": "Ginger Dominguez",
            "matricula": "7138228",
            "email": "eget@goat.com",
            "cpf": "18384905070"
        },
]
```    

## Instruções para entrega
- O seu projeto deve estar público.
- Caso tenha usado outros recursos especificar no `Readme`.
- Caso você termine antes do prazo final, sinta-se à vontade em enviar com antecedência.

__ATENÇÃO__: foque em entregar alguma coisa fechada e funcional, Caso não termine tudo a tempo, envie o código assim mesmo, pois o seu trabalho será avaliado até onde você conseguiu fazer.

*Desejo um bom teste para você!*

