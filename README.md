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

