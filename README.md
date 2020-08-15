# Contexto

## Objetivos

### 1 - Geral
Criar uma aplicação para auxiliar a produção de prescrições nutricionais.

### 2 - Especificos
- Criar uma área de administração que permita o gerenciamento de cadastros diversos.
- Criar uma área para que o paciente possa acompanhar as prescrições nutricionais.

# Requisitos

## Obrigatórios:
- Django >= 3.1
- Python >= 3.7
- Uso do Git (compartilhar o repositório)

## Complementares:
- Docker
- Testes unitários (pytest)
- Vue.js (área do paciente)

# Especificações técnicas

## Interface administrativa
Você deverá implementar uma interface administrativa (pode usar django-admin) na qual a nutricionista  poderá cadastrar paciente, refeições e receitas.

A interface administrativa deve conter as respectivas funcionalidades:

### Cadastrar paciente
Deve ser possível cadastrar os pacientes para vincular nas prescrições:

* **Nome:** nome do paciente (obrigatório)
* **Data nascimento:** data nascimento (obrigatório)
* **Sexo:** sexo do paciente (obrigatório)
* **E-mail:** email para acessar a área do paciente (obrigatório)
* **Senha:** senha para acessar a área do paciente (obrigatório)

### Cadastrar refeições
Deve ser possível cadastrar as refeições (ex: CAFÉ DA MANHÃ, ALMOÇO, SOBREMESA, JANTAR E ETC) para montar uma prescrição:

* **Nome:** nome da refeição (obrigatório)
* **Ordem:** para ordenar as refeições numa sequência lógica (obrigatório)

### Cadastrar receita
Deve ser possível criar uma receita:

* **Nome:** nome da receita (obrigatório)
* **Descrição:** modo de preparo da receita (obrigatório)
* **Tipo refeição:** seleção das refeições onde a receita deve aparecer (obrigatório)
* **Tags:** seleção de tags para que agrupar as receitas (não obrigatórias)

#### Orientações:
* As tags deve representar (sem ovo, sem carne vermelha, e etc)

### Cadastrar prescrição
Deve ser possível criar prescrição uma prescrição e associar a um paciente:

* **Paciente:** seleção do paciente (obrigatório)
* **Data da prescrição :** seleção da data (obrigatório)
* **Peso:** peso do paciente (obrigatório)
* **Receitas:** seleção das receitas (obrigatório)
* **Observação:** descritivo complementar (não obrigatório)

#### Orientações:
* Para elaborar a prescrição o(a) nutricionista deve selecionar o paciente (pré-cadastro), indicar a data, o peso em kg e selecionar as refeições
* Deve ser ordenada por tipos de refeições e suas respectivas receitas;
* Deve ser possível filtrar as receitas pelos filtros cadastrados;

## Interface do paciente
Você deverá implementar uma interface do paciente para que ele possa fazer login, acessar suas prescrições e ver na íntegra cada uma delas

### API
Você deverá construir uma API, seguindo os padrões e boas práticas do REST contendo os seguintes endpoints:

### Autenticação

Com exceção do endpoint de login, todos os endpoints da API devem ser protegidos por autenticação e necessitam receber token via cabeçalho HTTP `Authorization`. Veja um exemplo de requisição:

```
GET /prescricoes/
Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b
```

### Listar prescrições nutricionais
Lista todas prescrições do usuário (paciente) logado.

#### Requisição
```
GET /prescricoes/
Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b
```

#### Resposta
```json
[
    {
        "id": 2,
        "paciente": 3,
        "peso": 80,
        "criado_em": "2020-08-15T19:31:15-0300",
    },
    {
        "id": 1,
        "paciente": 4,
        "peso": 84,
        "criado_em": "2020-06-10T19:00:15-0300",
    }
]
```

### Detalhar prescrição nutricional
Acessar os detalhes da prescrição

#### Requisição
```
GET /prescricoes/<id_prescricao>/
Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b
```

#### Resposta
```json
[
    {
        "id": 1,
        "paciente": 4,
        "peso": 80,
        "criado_em": "2020-08-15T19:31:15-0300",
        "refeicoes": [
            {
                "id": 1,
                "receita": {
                    "id": 1,
                    "nome": "Crepioca",
                    "descricao": "2 ovos mexidos e farinha de tapioca",
                },
                "tipo_refeicao": "café da manha",
                "obs": "observações ..."
            }
        ]
    }
]
```

### Tela
Deverá apresentar a listagem de prescrições associadas ao paciente e o “show” da prescrição selecionada.

#### Orientações:
* Uso do django-templates (recomendamos usar o tabler para montar as telas [veja](https://tabler.io/))

# Envio do teste
Após o término do teste, envie a url do repositório para vagas@corumbaconsultoria.com.br