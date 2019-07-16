---
title: SELECT – comando SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85f281aefe79a09806c42e13cd771f976362d053
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943782"
---
# <a name="select---sql-command"></a>SELECT – comando SQL
Recupera dados de uma ou mais tabelas.  
  
 O Driver de ODBC do Visual FoxPro dá suporte à sintaxe de linguagem do Visual FoxPro nativo para esse comando. Para obter informações específicas do driver, consulte **Driver comentários**.  
  
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
>  Um *subconsulta*, referenciado em argumentos a seguir, é um SELECT dentro de uma seleção e devem ser colocados entre parênteses. Você pode ter até duas subconsultas no mesmo nível (não aninhado) na cláusula WHERE. (Consulte a seção de argumentos.) Subconsultas podem conter várias condições de junção.  
  
 [Todos os &#124; DISTINCT]   [*Alias*.] *Select_Item* [AS *Column_Name*] [, [*Alias*.] *Select_Item* [AS *Column_Name*]...]  
 A cláusula SELECT especifica os campos, constantes e expressões que são exibidas nos resultados da consulta.  
  
 Por padrão, todos os exibe todas as linhas nos resultados da consulta.  
  
 DISTINCT exclui duplicatas de todas as linhas dos resultados da consulta.  
  
> [!NOTE]  
>  Você pode usar apenas uma vez DISTINCT por cláusula SELECT.  
  
 *Alias*. qualifica nomes de item correspondentes. Cada item que você especificar com *Select_Item* gera uma coluna dos resultados da consulta. Se dois ou mais itens têm o mesmo nome, inclua o alias de tabela e um ponto antes do nome do item para impedir que colunas sendo duplicado.  
  
 *Select_Item* Especifica um item a ser incluído nos resultados da consulta. Um item pode ser um dos seguintes:  
  
-   O nome de um campo de uma tabela na cláusula FROM.  
  
-   Uma constante especificando que o mesmo valor constante deve aparecer em cada linha dos resultados da consulta.  
  
-   Uma expressão que pode ser o nome de uma função definida pelo usuário.  
  
 **Funções definidas pelo usuário com SELECT**  
  
 Embora o uso de funções definidas pelo usuário na cláusula SELECT tem benefícios óbvios, você também deve considerar as seguintes restrições:  
  
-   A velocidade das operações executadas com SELECT pode ser limitada pela velocidade com que essas funções definidas pelo usuário são executadas. Manipulações de alto volume que envolvem funções definidas pelo usuário podem ser melhor realizadas usando a API e funções definidas pelo usuário, escritas em C ou linguagem de assembly.  
  
-   O único modo confiável para passar valores para as funções definidas pelo usuário chamadas a partir de SELECT é a lista de argumentos passada para a função quando ela for invocada.  
  
-   Mesmo se você experimentar e descobrir uma manipulação supostamente proibida que funciona corretamente em uma determinada versão do FoxPro, não há nenhuma garantia, que ele continuará a funcionar em versões posteriores.  
  
 Essas restrições, além de funções definidas pelo usuário são aceitáveis na cláusula SELECT. No entanto, lembre-se de que o uso de SELECT pode prejudicar o desempenho.  
  
 As funções de campo a seguir estão disponíveis para uso com o item de seleção que é um campo ou uma expressão que envolva um campo:  
  
-   AVG (*Select_Item*)-calcula a média de uma coluna de dados numéricos.  
  
-   CONTAGEM (*Select_Item*)-conta o número de selecionar itens em uma coluna. Count(*) conta o número de linhas na saída da consulta.  
  
-   MIN (*Select_Item*) – determina o menor valor de *Select_Item* em uma coluna.  
  
-   MAX (*Select_Item*) – determina o maior valor de *Select_Item* em uma coluna.  
  
-   Soma (*Select_Item*)-totais de uma coluna de dados numéricos.  
  
 Você não pode aninhar funções de campo.  
  
 AS *Column_Name*  
 Especifica o título de uma coluna na saída da consulta. Isso é útil quando *Select_Item* é uma expressão ou contém um campo de função e você deseja atribuir um nome significativo de coluna. *Column_Name* pode ser uma expressão, mas não pode conter caracteres (por exemplo, espaços) que não são permitidos em nomes de campo de tabela.  
  
 DE [*DatabaseName*!] *Tabela* [*Local_Alias*] [, [*DatabaseName*!] *Tabela* [*Local_Alias*]...]  
 Lista as tabelas que contêm os dados que a consulta recupera. Se nenhuma tabela estiver aberta, Visual FoxPro exibe a **abrir** caixa de diálogo para que você possa especificar o local do arquivo. Depois que ele tiver sido aberto, a tabela permanece aberta depois que a consulta for concluída.  
  
 *DatabaseName*! Especifica o nome de um banco de dados diferente daquele especificado com a fonte de dados. Você deve incluir o nome do banco de dados que contém a tabela se o banco de dados não for especificado com a fonte de dados. Inclua o delimitador de ponto de exclamação (!) após o nome do banco de dados e antes do nome da tabela.  
  
 *Local_Alias* Especifica um nome temporário para a tabela nomeada na *tabela*. Se você especificar um alias de local, você deve usar o alias do local em vez do nome de tabela em toda a instrução SELECT. O alias de local não afeta o ambiente do Visual FoxPro.  
  
 Em que *JoinCondition* [AND *JoinCondition* ...]    [AND &#124; ou *FilterCondition* [AND &#124; ou *FilterCondition* ...]]  
 Informa ao Visual FoxPro para incluir apenas determinados registros nos resultados da consulta. ONDE é necessário para recuperar dados de várias tabelas.  
  
 *JoinCondition* Especifica os campos que vinculam as tabelas na cláusula FROM. Se você incluir mais de uma tabela em uma consulta, você deve especificar uma condição de junção para cada tabela após a primeira.  
  
> [!IMPORTANT]  
>  Quando você cria condições de junção, considere as seguintes informações:  
  
-   Se você incluir duas tabelas em uma consulta e não especificar uma condição de junção, todos os registros na primeira tabela é Unido a todos os registros na segunda tabela desde que as condições de filtro forem atendidas. Uma consulta pode produzir os resultados longos.  
  
-   Tenha cuidado ao serem unidas a tabelas com campos vazios porque do Visual FoxPro corresponde aos campos vazios. Por exemplo, se você ingressar no cliente. ZIP e a nota fiscal. COMPACTE e se o cliente contém 100 CEPs vazios e FATURA contém 400 CEPs vazios, a saída da consulta contém 40.000 registros extras resultante de campos vazios. Use o **(vazio)** função para eliminar registros vazios da saída da consulta.  
  
-   Você deve usar o operador AND para se conectar a várias condições de junção. Cada condição de junção tem a seguinte forma:  
  
     *Comparação de FieldName1 FieldName2*  
  
     *FieldName1* é o nome de um campo de uma tabela, *FieldName2* é o nome de um campo de outra tabela, e *comparação* é um dos operadores descritos na tabela a seguir.  
  
|Operador|Comparação|  
|--------------|----------------|  
|=|Igual|  
|==|Exatamente iguais|  
|LIKE|SQL COMO|  
|<>, !=, #|Não é igual a|  
|>|Mais de|  
|>=|Maior ou igual a|  
|<|Menor que|  
|<=|Menor que ou igual a|  
  
 Quando você usa o operador = com cadeias de caracteres, ele atua de forma diferente, dependendo da configuração de SET ANSI. Quando SET ANSI é definida como OFF, Visual FoxPro trata as comparações de cadeia de caracteres de uma maneira familiar aos usuários do Xbase. Quando SET ANSI é definida como ON, Visual FoxPro segue os padrões ANSI para comparações de cadeia de caracteres. Ver [SET ANSI](../../odbc/microsoft/set-ansi-command.md) e [SET EXACT](../../odbc/microsoft/set-exact-command.md) para obter mais informações sobre como o Visual FoxPro executa comparações de cadeia de caracteres.  
  
 *FilterCondition* Especifica os critérios que os registros devem atender para serem incluídos nos resultados da consulta. Você pode incluir quantos condições em uma consulta de filtragem, como você deseja conectar-se com o operador e ou operador OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **(vazio)** para verificar se há um campo vazio. *FilterCondition* pode usar qualquer um dos formulários nos exemplos a seguir:  
  
 **Exemplo 1** *FieldName1 FieldName2 de comparação*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Exemplo 2** *expressão de comparação FieldName*  
  
 `payments.amount >= 1000`  
  
 **Exemplo 3** *comparação FieldName* todos os (*subconsulta*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando a condição de filtro inclui tudo, o campo deve atender a condição de comparação para todos os valores gerados pela subconsulta, antes de seu registro é incluído nos resultados da consulta.  
  
 **Exemplo 4** *comparação FieldName* ANY &#124; SOME (*subconsulta*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando a condição de filtro inclui qualquer um ou alguns, o campo deve atender a condição de comparação para pelo menos um dos valores gerados pela subconsulta.  
  
 O exemplo a seguir verifica se os valores no campo estão dentro do intervalo especificado de valores:  
  
 **Exemplo 5** *FieldName* [NOT] BETWEEN *Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 O exemplo a seguir verifica se pelo menos uma linha atende aos critérios na subconsulta. Quando a condição de filtro inclui EXISTS, a condição de filtro é avaliada como True (. T.), a menos que a subconsulta é avaliada para o conjunto vazio.  
  
 **Exemplo 6** [não] existe (*subconsulta*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Exemplo 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Quando a condição de filtro inclui IN, o campo deve conter um dos valores antes de seu registro é incluído nos resultados da consulta.  
  
 **Exemplo 8** *FieldName* [NOT] IN (*subconsulta*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 Aqui o campo deve conter um dos valores retornados pela subconsulta, antes de seu registro é incluído nos resultados da consulta.  
  
 **Exemplo 9** *FieldName* [NOT] como *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Esta condição de filtro de pesquisa para cada campo que corresponde ao *cExpression*. Você pode usar o sinal de porcentagem (%) e caracteres curinga de sublinhado (_) como parte da *cExpression*. O sublinhado representa um único caractere desconhecido na cadeia de caracteres.  
  
 GROUP BY *GroupColumn* [, *GroupColumn* ...]  
 Agrupa linhas na consulta com base nos valores em uma ou mais colunas. *GroupColumn* pode ser uma das seguintes opções:  
  
-   O nome de um campo de tabela comum.  
  
-   Um campo que inclui uma função de campo SQL.  
  
-   Uma expressão numérica que indica o local da coluna na tabela de resultados. (O número da coluna mais à esquerda é 1.)  
  
 TENDO *FilterCondition*  
 Especifica uma condição de filtro que grupos precisam cumprir para serem incluídas nos resultados da consulta. HAVING deve ser usado com GROUP BY e podem incluir muitas condições de filtragem desejar, conectados por AND ou operador OR. Você também pode usar não para reverter o valor de uma expressão lógica.  
  
 *FilterCondition* não pode conter uma subconsulta.  
  
 Uma cláusula HAVING sem uma cláusula GROUP BY se comporta como uma cláusula WHERE. Você pode usar aliases de locais e funções de campos na cláusula HAVING. Use uma cláusula WHERE para melhorar o desempenho se a cláusula HAVING não contiver funções nenhum campo.  
  
 [[ALL] de união *SELECTCommand*]  
 Combina os resultados finais de uma SELECT com os resultados finais do outro "SELECT". Por padrão, a união verifica os resultados combinados e elimina linhas duplicadas. Use parênteses para combinar várias cláusulas UNION.  
  
 Todos os impede que união eliminar linhas duplicadas dos resultados combinados.  
  
 As cláusulas UNION seguem estas regras:  
  
-   Você não pode usar UNION para combinar subconsultas.  
  
-   Ambos os comandos SELECT devem ter o mesmo número de colunas em sua saída de consulta.  
  
-   Cada coluna nos resultados da consulta de uma SELECT deve ter o mesmo tipo de dados e largura da coluna correspondente no outro, selecione.  
  
-   Somente SELECT final pode ter uma cláusula ORDER BY, que deve se referir a colunas de saída por número. Se uma cláusula ORDER BY for incluída, ele afeta o resultado completo.  
  
 Você também pode usar a cláusula UNION para simular uma junção externa.  
  
 Quando você une duas tabelas em uma consulta, somente os registros com valores correspondentes nos campos de junção são incluídos na saída. Se um registro na tabela pai não tiver um registro correspondente na tabela filho, o registro na tabela pai não está incluído na saída. Uma junção externa permite incluir todos os registros na tabela pai na saída, juntamente com os registros correspondentes na tabela filho. Para criar uma junção externa no Visual FoxPro, você deve usar um comando SELECT aninhado, como no exemplo a seguir:  
  
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
>  Certifique-se de que você inclua o espaço que precede cada ponto e vírgula. Caso contrário, você receberá um erro.  
  
 A seção do comando antes que a cláusula UNION seleciona os registros de ambas as tabelas que têm valores correspondentes. As empresas de cliente que não tem faturas associadas não são incluídas. A seção do comando após a cláusula UNION seleciona os registros na tabela de clientes que não tem registros na tabela de pedidos correspondentes.  
  
 Sobre a segunda seção do comando, observe o seguinte:  
  
-   A instrução SELECT entre parênteses é processada primeiro. Essa instrução cria uma seleção de todos os números de cliente na tabela orders.  
  
-   A cláusula WHERE localiza todos os números de cliente na tabela de clientes que não estão na tabela orders. Porque a primeira seção do comando fornecido todas as empresas que tinha um número de cliente na tabela orders, todas as empresas na tabela customer agora estão incluídas nos resultados da consulta.  
  
-   Como as estruturas das tabelas incluídas em uma união devem ser idênticas, há dois espaços reservados na segunda instrução SELECT para representar *orders.order_id* e *orders.emp_id* no primeiro, selecione instrução.  
  
    > [!NOTE]  
    >  Os espaços reservados devem ser do mesmo tipo que os campos que eles representam. Se o campo for um tipo de data, o espaço reservado deve ser {/ /}. Se o campo é um campo de caractere, o espaço reservado deve ser a cadeia de caracteres vazia ("").  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC]...]  
 Classifica os resultados da consulta com base nos dados de uma ou mais colunas. Cada *Order_Item* deve corresponder a uma coluna nos resultados da consulta e pode ser um dos seguintes:  
  
-   Um campo em uma tabela FROM também é um item select na cláusula SELECT principal (não em uma subconsulta).  
  
-   Uma expressão numérica que indica o local da coluna na tabela de resultados. (A coluna mais à esquerda é o número 1.)  
  
 ASC especifica uma ordem crescente de acordo com o item do pedido ou itens, resultados de consulta e é o padrão para ORDER BY.  
  
 DESC Especifica uma ordem decrescente dos resultados da consulta.  
  
 Os resultados da consulta aparecem fora de ordem, se você não especificar uma ordem com ORDER BY.  
  
## <a name="remarks"></a>Comentários  
 Selecione é um comando SQL que está incorporado ao Visual FoxPro como qualquer outro comando do Visual FoxPro. Quando você usa o selecione para representar uma consulta, do Visual FoxPro interpreta a consulta e recupera os dados especificados das tabelas. Você pode criar uma consulta SELECT de dentro da janela de Prompt de comando ou um programa do Visual FoxPro (assim como acontece com qualquer outro comando do Visual FoxPro).  
  
> [!NOTE]  
>  Selecione não respeita a condição de filtro atual especificada com o filtro definido.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando seu aplicativo envia a instrução ODBC SQL SELECT para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando do Visual FoxPro selecionar sem conversão, a menos que o comando contém uma sequência de escape ODBC. Itens colocados em uma sequência de escape ODBC são convertidos em sintaxe do Visual FoxPro. Para obter mais informações sobre como usar o ODBC sequências de escape, consulte [funções de data e hora](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) e, nas *referência do programador de ODBC do Microsoft*, consulte [sequências de Escape no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) .  
  
## <a name="see-also"></a>Consulte também  
 [CRIAR TABELA - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERIR - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [CONJUNTO EXATO](../../odbc/microsoft/set-exact-command.md)
