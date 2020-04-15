---
title: SELECT - Comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640189a5a31d0c21642b037e906bd6361690a9a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300936"
---
# <a name="select---sql-command"></a>SELECT – comando SQL
Recupera dados de uma ou mais tabelas.  
  
 O Visual FoxPro ODBC Driver suporta a sintaxe nativa visual foxpro para este comando. Para obter informações específicas do motorista, consulte **Observações do motorista**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
  
> [!NOTE]  
>  Uma *subconsulta*, referida nos argumentos a seguir, é um SELECT dentro de um SELECT e deve ser fechada entre parênteses. Você pode ter até duas subconsultas no mesmo nível (não aninhado) na cláusula WHERE. (Veja essa seção dos argumentos.) As subconsultas podem conter várias condições de adesão.  
  
 [TODOS &#124; DISTINTOS]   [*Alias*.] *Select_Item* [AS *Column_Name]*[, [*Alias*.] *Select_Item* [COMO *COLUMN_NAME]...*  
 A cláusula SELECT especifica os campos, as constantes e as expressões exibidas nos resultados da consulta.  
  
 Por padrão, ALL exibe todas as linhas nos resultados da consulta.  
  
 DISTINCT exclui duplicatas de quaisquer linhas dos resultados da consulta.  
  
> [!NOTE]  
>  Você pode usar DISTINCT apenas uma vez por cláusula SELECT.  
  
 *Alias*. qualifica nomes de itens correspondentes. Cada item especificado com *Select_Item* gera uma coluna dos resultados da consulta. Se dois ou mais itens tiverem o mesmo nome, inclua o alias da tabela e um período antes do nome do item para evitar que as colunas sejam duplicadas.  
  
 *Select_Item* especifica um item a ser incluído nos resultados da consulta. Um item pode ser um dos seguintes:  
  
-   O nome de um campo de uma tabela na cláusula FROM.  
  
-   Uma constante especificando que o mesmo valor constante deve aparecer em cada linha dos resultados da consulta.  
  
-   Uma expressão que pode ser o nome de uma função definida pelo usuário.  
  
 **Funções definidas pelo usuário com SELECT**  
  
 Embora o uso de funções definidas pelo usuário na cláusula SELECT tenha benefícios óbvios, você também deve considerar as seguintes restrições:  
  
-   A velocidade das operações realizadas com select pode ser limitada pela velocidade com que tais funções definidas pelo usuário são executadas. Manipulações de alto volume envolvendo funções definidas pelo usuário podem ser melhor realizadas usando API e funções definidas pelo usuário escritas em C ou linguagem de montagem.  
  
-   A única maneira confiável de passar valores para funções definidas pelo usuário invocadas do SELECT é pela lista de argumentos passada para a função quando ela é invocada.  
  
-   Mesmo que você experimente e descubra uma manipulação supostamente proibida que funciona corretamente em uma determinada versão do FoxPro, não há garantia de que ele continuará a funcionar em versões posteriores.  
  
 Além dessas restrições, as funções definidas pelo usuário são aceitáveis na cláusula SELECT. No entanto, lembre-se de que o uso do SELECT pode retardar o desempenho.  
  
 As seguintes funções de campo estão disponíveis para uso com um item selecionado que é um campo ou uma expressão envolvendo um campo:  
  
-   AVG(*Select_Item*--Médias de uma coluna de dados numéricos.  
  
-   COUNT *(Select_Item*)-Conta o número de itens selecionados em uma coluna. COUNT(*) conta o número de linhas na saída de consulta.  
  
-   *MIN(Select_Item*)-Determina o menor valor de *Select_Item* em uma coluna.  
  
-   O MAX(*Select_Item*)-Determina o maior valor de *Select_Item* em uma coluna.  
  
-   Soma(*Select_Item*)-Totaliza uma coluna de dados numéricos.  
  
 Você não pode aninhar funções de campo.  
  
 COMO *COLUMN_NAME*  
 Especifica o título de uma coluna na saída de consulta. Isso é útil quando *Select_Item* é uma expressão ou contém uma função de campo e você deseja dar à coluna um nome significativo. *Column_Name* pode ser uma expressão, mas não pode conter caracteres (por exemplo, espaços) que não são permitidos em nomes de campo de tabela.  
  
 DE [*Nome do banco de dados*!] *Tabela* [*Local_Alias*] [, [*Nome do banco de dados*!] *Tabela* [*Local_Alias*] ...]  
 Lista as tabelas que contêm os dados que a consulta recupera. Se nenhuma tabela estiver aberta, o Visual FoxPro exibirá a caixa de diálogo **Abrir** para que você possa especificar o local do arquivo. Depois de aberto, a tabela permanece aberta após a consulta ser concluída.  
  
 *Nome do banco de dados*! especifica o nome de um banco de dados diferente do especificado com a fonte de dados. Você deve incluir o nome do banco de dados que contém a tabela se o banco de dados não for especificado com a fonte de dados. Inclua o ponto de exclamação (!) delimitador após o nome do banco de dados e antes do nome da tabela.  
  
 *Local_Alias* especifica um nome temporário para a tabela nomeada na *Tabela*. Se você especificar um alias local, você deve usar o alias local em vez do nome da tabela durante toda a declaração SELECT. O alias local não afeta o ambiente Visual FoxPro.  
  
 ONDE *AderemCondição* [E *AderemCondição* ...]    [E &#124; ou *filtroCondição* [E &#124; ou *Condição de Filtro* ...]]  
 Diz ao Visual FoxPro para incluir apenas certos registros nos resultados da consulta. ONDE é necessário para recuperar dados de várias tabelas.  
  
 *O JoinCondition* especifica campos que vinculam as tabelas na cláusula FROM. Se você incluir mais de uma tabela em uma consulta, você deve especificar uma condição de adesão para cada tabela após a primeira.  
  
> [!IMPORTANT]  
>  Considere as seguintes informações ao criar condições de adesão:  
  
-   Se você incluir duas tabelas em uma consulta e não especificar uma condição de adesão, cada registro na primeira tabela será juntado a cada registro na segunda tabela, desde que as condições do filtro sejam atendidas. Tal consulta pode produzir resultados demorados.  
  
-   Tenha cuidado ao juntar mesas com campos vazios porque o Visual FoxPro corresponde a campos vazios. Por exemplo, se você aderir ao CUSTOMER. ZIP e FATURA. ZIP e se o CLIENTE contiver 100 CEP vazios e invoice contiver 400 CEP vazios, a saída de consulta contém 40.000 registros extras resultantes dos campos vazios. Use a função **EMPTY()** para eliminar registros vazios da saída de consulta.  
  
-   Você deve usar o operador AND para conectar várias condições de adesão. Cada condição de adesão tem a seguinte forma:  
  
     *Nome do campode 1 nome de comparação2*  
  
     *FieldName1* é o nome de um campo de uma tabela, *FieldName2* é o nome de um campo de outra tabela, e *Comparação* é um dos operadores descritos na tabela a seguir.  
  
|Operador|Comparação|  
|--------------|----------------|  
|=|Igual a|  
|==|Exatamente igual|  
|LIKE|SQL LIKE|  
|<>, !=, #|Não igual|  
|>|Mais do que|  
|>=|Mais do que ou igual a|  
|<|Menor que|  
|<=|Menor que ou igual a|  
  
 Quando você usa o operador = com strings, ele age de forma diferente, dependendo da configuração do SET ANSI. Quando o SET ANSI é definido como OFF, o Visual FoxPro trata comparações de strings de uma maneira familiar aos usuários do Xbase. Quando o SET ANSI é definido como ON, o Visual FoxPro segue os padrões ANSI para comparações de strings. Consulte [SET ANSI](../../odbc/microsoft/set-ansi-command.md) e [SET EXACT](../../odbc/microsoft/set-exact-command.md) para obter mais informações sobre como o Visual FoxPro executa comparações de strings.  
  
 *FilterCondition* especifica os critérios que os registros devem atender para serem incluídos nos resultados da consulta. Você pode incluir quantas condições de filtro em uma consulta quiser, conectando-as com o operador And ou OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **EMPTY()** para verificar se há um campo vazio. *FilterCondition* pode pegar qualquer um dos formulários nos seguintes exemplos:  
  
 **Exemplo 1** *FieldName1 Comparison FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Exemplo 2** *Expressão de comparação de nome de campo*  
  
 `payments.amount >= 1000`  
  
 **Exemplo 3** *Comparação fieldname* ALL *(Subquery)*  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando a condição do filtro inclui ALL, o campo deve atender à condição de comparação de todos os valores gerados pela subconsulta antes de seu registro ser incluído nos resultados da consulta.  
  
 **Exemplo 4** *Comparação fieldname* ANY &#124; SOME *(Subquery)*  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando a condição do filtro inclui QUALQUER ou ALGUM, o campo deve atender à condição de comparação de pelo menos um dos valores gerados pela subconsulta.  
  
 O exemplo a seguir verifica se os valores no campo estão dentro de um intervalo de valores especificado:  
  
 **Exemplo 5** *Nome de Campo* [NÃO] ENTRE *Start_Range* E *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 O exemplo a seguir verifica se pelo menos uma linha atende aos critérios da subconsulta. Quando a condição do filtro inclui EXISTE, a condição do filtro avalia-se como True (. T.) a menos que a subconsulta avalie para o conjunto vazio.  
  
 **Exemplo 6** [NÃO] EXISTE *(Subquery)*  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Exemplo 7** *FieldName* [NÃO] EM *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Quando a condição do filtro inclui IN, o campo deve conter um dos valores antes de seu registro ser incluído nos resultados da consulta.  
  
 **Exemplo 8** *Nome de Campo* [NÃO] IN *(Subquery)*  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 Aqui, o campo deve conter um dos valores devolvidos pela subconsulta antes de seu registro ser incluído nos resultados da consulta.  
  
 **Exemplo 9** *FieldName* [NÃO] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Esta condição de filtro procura cada campo que corresponde *a cExpression*. Você pode usar o sinal percentual (%) e sublinhar (_ ) caracteres curinga como parte de *cExpression*. O sublinhado representa um único personagem desconhecido na seqüência.  
  
 GRUPO POR *GrupoColuna* [, *GroupColumn* ...]  
 Grupos de linhas na consulta com base em valores em uma ou mais colunas. *GroupColumn* pode ser um dos seguintes:  
  
-   O nome de um campo de mesa regular.  
  
-   Um campo que inclui uma função de campo SQL.  
  
-   Uma expressão numérica que indica a localização da coluna na tabela de resultados. (O número da coluna mais à esquerda é 1.)  
  
 HAVING *FilterCondition*  
 Especifica uma condição de filtro que os grupos devem atender para serem incluídos nos resultados da consulta. Having deve ser usado com GROUP BY e pode incluir quantas condições de filtro quiser, conectadas pelo operador AND ou OR. Você também pode usar NÃO para reverter o valor de uma expressão lógica.  
  
 *FilterCondition* não pode conter uma subconsulta.  
  
 Uma cláusula TER sem uma cláusula GROUP BY comporta-se como uma cláusula WHERE. Você pode usar aliases locais e funções de campo na cláusula HAVING. Use uma cláusula WHERE para um desempenho mais rápido se a cláusula HAVING não contiver funções de campo.  
  
 [UNION [ALL] *SELECTCommand*]  
 Combina os resultados finais de um SELECT com os resultados finais de outro SELECT. Por padrão, a UNION verifica os resultados combinados e elimina linhas duplicadas. Use parênteses para combinar várias cláusulas da UNIÃO.  
  
 A ALL impede a UNION de eliminar as linhas duplicadas dos resultados combinados.  
  
 As cláusulas da UNIÃO seguem estas regras:  
  
-   Você não pode usar o UNION para combinar subconsultas.  
  
-   Ambos os comandos SELECT devem ter o mesmo número de colunas na saída de consulta.  
  
-   Cada coluna nos resultados de consulta de um SELECT deve ter o mesmo tipo de dados e largura que a coluna correspondente na outra SELECT.  
  
-   Apenas o SELECT final pode ter uma cláusula ORDER BY, que deve se referir às colunas de saída por número. Se uma cláusula DE ORDEM BY for incluída, ela afetará o resultado completo.  
  
 Você também pode usar a cláusula da UNIÃO para simular uma adesão externa.  
  
 Quando você junta duas tabelas em uma consulta, apenas os registros com valores correspondentes nos campos de junção são incluídos na saída. Se um registro na tabela pai não tiver um registro correspondente na tabela filho, o registro na tabela pai não será incluído na saída. Uma junta externa permite incluir todos os registros na tabela dos pais na saída, juntamente com os registros correspondentes na tabela filho. Para criar uma junta externa no Visual FoxPro, você deve usar um comando SELECT aninhada, como no exemplo a seguir:  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  Certifique-se de incluir o espaço que imediatamente precede cada ponto e vírgula. Caso contrário, você receberá um erro.  
  
 A seção do comando antes da cláusula DA UNIÃO seleciona registros de ambas as tabelas que tenham valores correspondentes. As empresas clientes que não possuem faturas associadas não estão incluídas. A seção do comando após a cláusula DO SINDICATO seleciona registros na tabela do cliente que não possuem registros correspondentes na tabela de pedidos.  
  
 Em relação à segunda seção do comando, observe o seguinte:  
  
-   A declaração SELECT dentro dos parênteses é processada primeiro. Esta declaração cria uma seleção de todos os números de clientes na tabela de pedidos.  
  
-   A cláusula WHERE encontra todos os números de clientes na tabela do cliente que não estão na tabela de pedidos. Como a primeira seção do comando forneceu todas as empresas que tinham um número de cliente na tabela de pedidos, todas as empresas na tabela de clientes estão agora incluídas nos resultados da consulta.  
  
-   Como as estruturas das tabelas incluídas em uma UNIÃO devem ser idênticas, há dois espaços reservados na segunda declaração SELECT para representar *ordens.order_id* e *ordens.emp_id* da primeira declaração SELECT.  
  
    > [!NOTE]  
    >  Os espaços reservados devem ser do mesmo tipo que os campos que representam. Se o campo for um tipo de data, o espaço reservado deve ser { / / }. Se o campo for um campo de caracteres, o espaço reservado deve ser a seqüência vazia ("").  
  
 ORDEM POR *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC] ...]  
 Classifica os resultados da consulta com base nos dados em uma ou mais colunas. Cada *Order_Item* deve corresponder a uma coluna nos resultados da consulta e pode ser uma das seguintes:  
  
-   Um campo em uma tabela DE QUE também é um item selecionado na cláusula SELECT principal (não em uma subquery).  
  
-   Uma expressão numérica que indica a localização da coluna na tabela de resultados. (A coluna mais à esquerda é o número 1.)  
  
 O ASC especifica uma ordem ascendente para resultados de consulta, de acordo com o item ou itens do pedido, e é o padrão para ORDER BY.  
  
 O DESC especifica uma ordem descendente para resultados de consulta.  
  
 Os resultados da consulta aparecerão desordenados se você não especificar um pedido com order BY.  
  
## <a name="remarks"></a>Comentários  
 SELECT é um comando SQL que é incorporado ao Visual FoxPro como qualquer outro comando Visual FoxPro. Quando você usa SELECT para fazer uma consulta, o Visual FoxPro interpreta a consulta e recupera os dados especificados das tabelas. Você pode criar uma consulta SELECT dentro da janela Prompt de comando ou de um programa Visual FoxPro (como em qualquer outro comando Visual FoxPro).  
  
> [!NOTE]  
>  Select não respeita a condição atual do filtro especificada com SET FILTER.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Quando seu aplicativo envia a declaração ODBC SQL SELECT para a fonte de dados, o Driver Visual FoxPro ODBC converte o comando no comando Visual FoxPro SELECT sem tradução, a menos que o comando contenha uma seqüência de fuga ODBC. Os itens incluídos em uma seqüência de fuga ODBC são convertidos em sintaxe Visual FoxPro. Para obter mais informações sobre como usar seqüências de fuga ODBC, consulte [Funções de hora e data](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) e na referência do *programador Microsoft ODBC,* consulte [Seqüências de fuga no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR TABELA - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERIR - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [DEFINIR ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [DEFINIR EXATO](../../odbc/microsoft/set-exact-command.md)
