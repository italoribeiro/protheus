1. Igualdade (eq - Equal)

Busca todos os fornecedores onde o Estado seja Ceará (CE).

    Filtro: A2_EST eq 'CE'

    Como fica a requisição:
    GET http://localhost:8080/rest/makro/custom/fornecedor?filter=A2_EST eq 'CE'

Paginação
http://localhost:8080/rest/makro/custom/fornecedor?page=1&pagesize=50&fields=a2_cod,a2_nome,a2_cgc

2. Diferente de (ne - Not Equal)

Busca todos os fornecedores, EXCETO os do estado de São Paulo (SP).

    Filtro: A2_EST ne 'SP'

    Como fica a requisição:
    GET http://localhost:8080/rest/makro/custom/fornecedor?filter=A2_EST ne 'SP'

    
3. Maior que / Menor que (gt / lt)

(gt = Greater Than | lt = Less Than | ge = Greater/Equal | le = Less/Equal)
Muito útil para datas, valores ou para varrer lotes de códigos. Vamos buscar os fornecedores com código maior que 000002.

    Filtro: A2_COD gt '000002'

    Como fica a requisição:  
    GET http://localhost:8080/rest/makro/custom/fornecedor?filter=A2_COD gt '000002'

4. Condições Múltiplas (and / or)

Buscando Fornecedores que sejam do Tipo Jurídico (J) E que o Estado seja Ceará (CE) OU São Paulo (SP).
Dica: Use parênteses para organizar a regra lógica.

    Filtro: A2_TIPO eq 'J' and (A2_EST eq 'CE' or A2_EST eq 'SP')

    Como fica a requisição:
    GET http://localhost:8080/rest/makro/custom/fornecedor?filter=A2_TIPO eq 'J' and (A2_EST eq 'CE' or A2_EST eq 'SP')

5. Busca Parte do Texto (substringof ou startswith)

O FWAdapterBaseV2 tem suporte a funções nativas de string do OData para emular o LIKE do banco de dados.
Para buscar fornecedores que contenham a palavra "SILVA" no nome:

    Filtro: substringof('SILVA', A2_NOME) (Atenção à sintaxe: o valor vem antes da coluna)

    Como fica a requisição:
    GET http://localhost:8080/rest/makro/custom/fornecedor?filter=substringof('SILVA', A2_NOME)
6. O "Combo" Completo da Vida Real

Imagine a tela de consulta de um App. Você quer pesquisar os Fornecedores Ativos que tenham "COMERCIO" no nome, trazer ordenado pelo código, pegando apenas a 1ª página com 10 itens e retornando só o Código, Nome e CGC para economizar a internet do celular.

    Params do Postman:

        filter = substringof('COMERCIO', A2_NOME)

        fields = a2_cod,a2_nome,a2_cgc

        order = A2_COD

        page = 1

        pagesize = 10

    Como fica a requisição:
    GET http://localhost:8080/rest/makro/custom/fornecedor?filter=substringof('COMERCIO', A2_NOME)&fields=a2_cod,a2_nome,a2_cgc&order=A2_COD&page=1&pagesize=10



## 🛠️ Exemplos de Uso da API (CRUD Completo)

Abaixo estão os exemplos de requisição utilizando o `cURL`. O parâmetro `:id` na URL corresponde à concatenação exata do **Código do Fornecedor** com a **Loja** (Ex: `00000501`).

### 1. Atualização Completa (PUT)
Substitui os dados principais do fornecedor. Ideal para formulários completos de edição.

```bash
curl --request PUT 'http://localhost:8080/rest/makro/custom/fornecedor/00000501' \
--header 'Content-Type: application/json' \
--data-raw '{
    "A2_NOME": "NOVO NOME DA EMPRESA S.A",
    "A2_NREDUZ": "NOVO NOME"
}'


2. Atualização Parcial (PATCH)

Atualiza apenas os campos enviados no JSON. Ideal para integrações com Fluig/RM onde apenas uma informação muda (ex: atualização de e-mail ou status), economizando processamento.

curl --request PATCH 'http://localhost:8080/rest/makro/custom/fornecedor/00000501' \
--header 'Content-Type: application/json' \
--data-raw '{
    "A2_EMAIL": "contato_atualizado@empresa.com.br"
}'

3. Exclusão (DELETE)

Realiza a exclusão lógica do fornecedor no Protheus (D_E_L_E_T_ = '*'). O Protheus validará automaticamente se há amarrações (ex: pedidos em aberto) antes de confirmar a exclusão.

curl --request DELETE 'http://localhost:8080/rest/makro/custom/fornecedor/00000501'



