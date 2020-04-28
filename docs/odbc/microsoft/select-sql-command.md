---
title: SELECT-comando SQL | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300936"
---
# <a name="select---sql-command"></a>SELECT – comando SQL
Recupera dados de uma ou mais tabelas.  
  
 O driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro para este comando. Para obter informações específicas do driver, consulte **comentários do driver**.  
  
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
>  Uma *subconsulta*, referida nos argumentos a seguir, é uma seleção dentro de uma seleção e deve ser colocada entre parênteses. Você pode ter até duas subconsultas no mesmo nível (não aninhado) na cláusula WHERE. (Consulte essa seção dos argumentos.) As subconsultas podem conter várias condições de junção.  
  
 [TODOS OS &#124; DISTINTOS]   [*Alias*.] *Select_Item* [como *Column_Name*] [, [*alias*.] *Select_Item* [como *Column_Name*]...]  
 A cláusula SELECT especifica os campos, as constantes e as expressões que são exibidas nos resultados da consulta.  
  
 Por padrão, todos exibe todas as linhas nos resultados da consulta.  
  
 DISTINCT exclui duplicatas de quaisquer linhas dos resultados da consulta.  
  
> [!NOTE]  
>  Você pode usar DISTINCT apenas uma vez por cláusula SELECT.  
  
 *Alias*. qualifica os nomes de item correspondentes. Cada item especificado com *Select_Item* gera uma coluna dos resultados da consulta. Se dois ou mais itens tiverem o mesmo nome, inclua o alias da tabela e um ponto antes do nome do item para impedir que as colunas sejam duplicadas.  
  
 *Select_Item* especifica um item a ser incluído nos resultados da consulta. Um item pode ser um dos seguintes:  
  
-   O nome de um campo de uma tabela na cláusula FROM.  
  
-   Uma constante que especifica que o mesmo valor constante deve aparecer em cada linha dos resultados da consulta.  
  
-   Uma expressão que pode ser o nome de uma função definida pelo usuário.  
  
 **Funções definidas pelo usuário com SELECT**  
  
 Embora o uso de funções definidas pelo usuário na cláusula SELECT tenha benefícios óbvios, você também deve considerar as seguintes restrições:  
  
-   A velocidade das operações executadas com SELECT pode ser limitada pela velocidade em que essas funções definidas pelo usuário são executadas. As manipulações de alto volume que envolvem funções definidas pelo usuário podem ser melhor realizadas usando a API e as funções definidas pelo usuário escritas em linguagem C ou assembly.  
  
-   A única maneira confiável de passar valores para funções definidas pelo usuário invocadas de SELECT é pela lista de argumentos passada para a função quando ela é invocada.  
  
-   Mesmo que você experimente e descubra uma manipulação de supostamente proibido que funcione corretamente em uma determinada versão do FoxPro, não há nenhuma garantia de que ela continuará a funcionar em versões posteriores.  
  
 Além dessas restrições, as funções definidas pelo usuário são aceitáveis na cláusula SELECT. No entanto, lembre-se de que o uso de SELECT pode diminuir o desempenho.  
  
 As seguintes funções de campo estão disponíveis para uso com um item de seleção que é um campo ou uma expressão que envolve um campo:  
  
-   AVG (*Select_Item*) – calcula a média de uma coluna de dados numéricos.  
  
-   COUNT (*Select_Item*) – conta o número de itens selecionados em uma coluna. COUNT (*) conta o número de linhas na saída da consulta.  
  
-   MIN (*Select_Item*) – determina o menor valor de *Select_Item* em uma coluna.  
  
-   MAX (*Select_Item*) – determina o maior valor de *Select_Item* em uma coluna.  
  
-   SUM (*Select_Item*) – totaliza uma coluna de dados numéricos.  
  
 Você não pode aninhar funções de campo.  
  
 COMO *Column_Name*  
 Especifica o cabeçalho de uma coluna na saída da consulta. Isso é útil quando *Select_Item* é uma expressão ou contém uma função de campo e você deseja dar um nome significativo à coluna. *Column_Name* pode ser uma expressão, mas não pode conter caracteres (por exemplo, espaços) que não são permitidos em nomes de campo de tabela.  
  
 DE [*DatabaseName*!] *Tabela* [*Local_Alias*] [, [*DatabaseName*!] *Tabela* [*Local_Alias*]...]  
 Lista as tabelas que contêm os dados que a consulta recupera. Se nenhuma tabela estiver aberta, o Visual FoxPro exibirá a caixa de diálogo **abrir** para que você possa especificar o local do arquivo. Depois de aberto, a tabela permanece aberta após a conclusão da consulta.  
  
 *DatabaseName*! Especifica o nome de um banco de dados que não seja aquele especificado com a fonte de dado. Você deve incluir o nome do banco de dados que contém a tabela se ele não for especificado com a fonte. Inclua o delimitador de ponto de exclamação (!) após o nome do banco de dados e antes do nome da tabela.  
  
 *Local_Alias* especifica um nome temporário para a tabela nomeada na *tabela*. Se você especificar um alias local, deverá usar o alias local em vez do nome da tabela em toda a instrução SELECT. O alias local não afeta o ambiente do Visual FoxPro.  
  
 ONDE *JoinCondition* [e *JoinCondition* ...]    [E &#124; ou *FilterCondition* [e &#124; ou *FilterCondition* ...]]  
 Instrui o Visual FoxPro a incluir apenas determinados registros nos resultados da consulta. Onde é necessário para recuperar dados de várias tabelas.  
  
 *JoinCondition* especifica os campos que vinculam as tabelas na cláusula FROM. Se você incluir mais de uma tabela em uma consulta, deverá especificar uma condição de junção para cada tabela após a primeira.  
  
> [!IMPORTANT]  
>  Considere as seguintes informações ao criar condições de junção:  
  
-   Se você incluir duas tabelas em uma consulta e não especificar uma condição de junção, todos os registros na primeira tabela serão adicionados a todos os registros na segunda tabela, desde que as condições de filtro sejam atendidas. Essa consulta pode produzir resultados longos.  
  
-   Tenha cuidado ao unir tabelas com campos vazios porque o Visual FoxPro corresponde a campos vazios. Por exemplo, se você ingressar no cliente. ZIP e fatura. O ZIP e, se o cliente contiver 100 códigos postais vazios e a fatura contiver 400 códigos postais vazios, a saída da consulta conterá 40.000 registros extras resultantes dos campos vazios. Use a função **Empty ()** para eliminar registros vazios da saída da consulta.  
  
-   Você deve usar o operador AND para conectar várias condições de junção. Cada condição de junção tem o seguinte formato:  
  
     *FieldName1 de comparação FieldName2*  
  
     *FieldName1* é o nome de um campo de uma tabela, *FieldName2* é o nome de um campo de outra tabela e a *comparação* é um dos operadores descritos na tabela a seguir.  
  
|Operador|Comparação|  
|--------------|----------------|  
|=|Igual a|  
|==|Exatamente igual|  
|LIKE|COMO SQL|  
|<>,! =, #|Não igual|  
|>|Mais de|  
|>=|Mais de ou igual a|  
|<|Menor que|  
|<=|Menor que ou igual a|  
  
 Quando você usa o operador = com cadeias de caracteres, ele age de forma diferente, dependendo da configuração do ANSI definido. Quando SET ANSI é definido como OFF, o Visual FoxPro trata comparações de cadeia de caracteres de uma maneira familiar para os usuários Xbase. Quando SET ANSI é definido como ON, o Visual FoxPro segue os padrões ANSI para comparações de cadeias de caracteres. Consulte [set ANSI](../../odbc/microsoft/set-ansi-command.md) e [set Exact](../../odbc/microsoft/set-exact-command.md) para obter mais informações sobre como o Visual FoxPro executa comparações de cadeias de caracteres.  
  
 *FilterCondition* especifica os critérios que os registros devem atender para serem incluídos nos resultados da consulta. Você pode incluir tantas condições de filtro em uma consulta quanto desejar, conectando-as com o operador AND ou OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica ou pode usar **Empty ()** para verificar se há um campo vazio. *FilterCondition* pode pegar qualquer um dos formulários nos exemplos a seguir:  
  
 **Exemplo 1** *FieldName1 de comparação FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Exemplo 2** *expressão de comparação FieldName*  
  
 `payments.amount >= 1000`  
  
 **Exemplo 3** *FieldName comparar* tudo (*subconsulta*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando a condição de filtro inclui tudo, o campo deve atender à condição de comparação para todos os valores gerados pela subconsulta antes que seu registro seja incluído nos resultados da consulta.  
  
 **Exemplo 4** *FieldName compara* qualquer &#124; alguns (*subconsulta*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando a condição de filtro inclui alguma ou alguma, o campo deve atender à condição de comparação para pelo menos um dos valores gerados pela subconsulta.  
  
 O exemplo a seguir verifica se os valores no campo estão dentro de um intervalo de valores especificado:  
  
 **Exemplo 5** *FieldName* [not] entre *Start_Range* e *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 O exemplo a seguir verifica se pelo menos uma linha atende aos critérios na subconsulta. Quando a condição de filtro inclui existir, a condição de filtro será avaliada como true (. T.) a menos que a subconsulta seja avaliada como o conjunto vazio.  
  
 O **exemplo 6** [not] existe (*subconsulta*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Exemplo 7** *FieldName* [not] in *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Quando a condição de filtro inclui no, o campo deve conter um dos valores antes que seu registro seja incluído nos resultados da consulta.  
  
 **Exemplo 8** *FieldName* [não] in (*subconsulta*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 Aqui, o campo deve conter um dos valores retornados pela subconsulta antes que seu registro seja incluído nos resultados da consulta.  
  
 **Exemplo 9** *FieldName* [não] like *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Essa condição de filtro pesquisa cada campo que corresponde a *cExpression*. Você pode usar o sinal de porcentagem (%) e caracteres curinga de sublinhado (_) como parte de *cExpression*. O sublinhado representa um único caractere desconhecido na cadeia de caracteres.  
  
 Agrupar por *GroupColumn* [, *GroupColumn* ...]  
 Agrupa linhas na consulta com base em valores em uma ou mais colunas. *GroupColumn* pode ser um dos seguintes:  
  
-   O nome de um campo de tabela normal.  
  
-   Um campo que inclui uma função de campo SQL.  
  
-   Uma expressão numérica que indica o local da coluna na tabela de resultados. (O número da coluna mais à esquerda é 1.)  
  
 TENDO *FilterCondition*  
 Especifica uma condição de filtro que os grupos devem atender para serem incluídos nos resultados da consulta. TER deve ser usado com GROUP BY e pode incluir quantas condições de filtro desejar, conectadas pelo operador AND ou OR. Você também pode usar não para reverter o valor de uma expressão lógica.  
  
 *FilterCondition* não pode conter uma subconsulta.  
  
 Uma cláusula HAVING sem uma cláusula GROUP BY se comporta como uma cláusula WHERE. Você pode usar aliases locais e funções de campo na cláusula HAVING. Use uma cláusula WHERE para obter um desempenho mais rápido se a cláusula HAVING não contiver nenhuma função de campo.  
  
 [UNION [ALL] *SELECTCommand*]  
 Combina os resultados finais de uma seleção com os resultados finais de outra seleção. Por padrão, a União verifica os resultados combinados e elimina as linhas duplicadas. Use parênteses para combinar várias cláusulas UNION.  
  
 ALL impede que a União elimine linhas duplicadas dos resultados combinados.  
  
 As cláusulas UNION seguem estas regras:  
  
-   Não é possível usar UNION para combinar subconsultas.  
  
-   Ambos os comandos SELECT devem ter o mesmo número de colunas em sua saída de consulta.  
  
-   Cada coluna nos resultados da consulta de uma seleção deve ter o mesmo tipo de dados e a mesma largura que a coluna correspondente na outra seleção.  
  
-   Somente a seleção final pode ter uma cláusula ORDER BY, que deve se referir às colunas de saída por número. Se uma cláusula ORDER BY for incluída, ela afetará o resultado completo.  
  
 Você também pode usar a cláusula UNION para simular uma junção externa.  
  
 Quando você une duas tabelas em uma consulta, somente os registros com valores correspondentes nos campos de junção são incluídos na saída. Se um registro na tabela pai não tiver um registro correspondente na tabela filho, o registro na tabela pai não será incluído na saída. Uma junção externa permite incluir todos os registros na tabela pai na saída, junto com os registros correspondentes na tabela filho. Para criar uma junção externa no Visual FoxPro, você deve usar um comando SELECT aninhado, como no exemplo a seguir:  
  
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
>  Certifique-se de incluir o espaço que precede imediatamente cada ponto e vírgula. Caso contrário, você receberá um erro.  
  
 A seção do comando antes da cláusula UNION seleciona registros de ambas as tabelas que têm valores correspondentes. As empresas do cliente que não têm faturas associadas não estão incluídas. A seção do comando após a cláusula UNION seleciona registros na tabela Customer que não têm registros correspondentes na tabela Orders.  
  
 Em relação à segunda seção do comando, observe o seguinte:  
  
-   A instrução SELECT dentro dos parênteses é processada primeiro. Essa instrução cria uma seleção de todos os números de clientes na tabela Orders.  
  
-   A cláusula WHERE localiza todos os números de clientes na tabela Customer que não estão na tabela Orders. Como a primeira seção do comando forneceu todas as empresas que tinham um número de cliente na tabela Orders, todas as empresas na tabela Customer agora estão incluídas nos resultados da consulta.  
  
-   Como as estruturas de tabelas incluídas em uma União devem ser idênticas, há dois espaços reservados na segunda instrução SELECT para representar *Orders. order_id* e *orders. emp_id* da primeira instrução SELECT.  
  
    > [!NOTE]  
    >  Os espaços reservados devem ser do mesmo tipo que os campos que representam. Se o campo for um tipo de data, o espaço reservado deverá ser {//}. Se o campo for um campo de caractere, o espaço reservado deverá ser a cadeia de caracteres vazia ("").  
  
 ORDENAr por *Order_Item* [ASC &#124; desc] [, *Order_Item* [ASC &#124; desc]...]  
 Classifica os resultados da consulta com base nos dados em uma ou mais colunas. Cada *Order_Item* deve corresponder a uma coluna nos resultados da consulta e pode ser uma das seguintes:  
  
-   Um campo em uma tabela de que também é um item selecionado na cláusula SELECT principal (não em uma subconsulta).  
  
-   Uma expressão numérica que indica o local da coluna na tabela de resultados. (A coluna mais à esquerda é o número 1.)  
  
 ASC especifica uma ordem crescente para os resultados da consulta, de acordo com o item ou itens do pedido, e é o padrão para ORDER BY.  
  
 DESC especifica uma ordem decrescente para resultados da consulta.  
  
 Os resultados da consulta serão exibidos sem ordenação se você não especificar um pedido com ORDER BY.  
  
## <a name="remarks"></a>Comentários  
 SELECT é um comando SQL que é criado no Visual FoxPro como qualquer outro comando do Visual FoxPro. Quando você usa SELECT para representar uma consulta, o Visual FoxPro interpreta a consulta e recupera os dados especificados das tabelas. Você pode criar uma consulta SELECT de dentro da janela de prompt de comando ou de um programa do Visual FoxPro (como com qualquer outro comando do Visual FoxPro).  
  
> [!NOTE]  
>  SELECT não respeita a condição de filtro atual especificada com o filtro de conjunto.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Quando o aplicativo envia a instrução ODBC SQL SELECT para a fonte de dados, o driver ODBC do Visual FoxPro converte o comando no comando SELECT do Visual FoxPro sem conversão, a menos que o comando contenha uma sequência de escape ODBC. Os itens colocados em uma sequência de escape ODBC são convertidos para a sintaxe do Visual FoxPro. Para obter mais informações sobre como usar sequências de escape ODBC, consulte [funções de hora e data](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) e, na *referência do programador de ODBC da Microsoft*, consulte [sequências de escape no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERIR-SQL](../../odbc/microsoft/insert-sql-command.md)   
 [DEFINIR ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [DEFINIR EXATO](../../odbc/microsoft/set-exact-command.md)
