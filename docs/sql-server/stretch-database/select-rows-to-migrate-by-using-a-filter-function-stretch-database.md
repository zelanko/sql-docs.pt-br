---
title: Selecionar linhas para migrar usando uma função de filtro (Stretch Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/27/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, predicates
- predicates for Stretch Database
- Stretch Database, inline table-valued functions
- inline table-valued functions for Stretch Database
ms.assetid: 090890ee-7620-4a08-8e15-d2fbc71dd12f
caps.latest.revision: 43
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c4834b888400b8155be979c42cd5d22a9bb03b54
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773202"
---
# <a name="select-rows-to-migrate-by-using-a-filter-function-stretch-database"></a>Selecionar linhas para migrar usando uma função de filtro (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Se você armazenar dados inertes em uma tabela separada, será possível configurar o Stretch Database para migrar a tabela inteira. Por outro lado, se sua tabela contiver dados dinâmicos e inertes, você poderá especificar um predicado de filtro para selecionar as linhas a serem migradas. O predicado de filtro é uma função com valor de tabela embutida. Este artigo descreve como escrever uma função com valor de tabela embutida para selecionar linhas a serem migradas.  
  
> [!IMPORTANT]
> Se você fornecer uma função de filtro precária, a migração de dados também será precária. O Stretch Database aplica a função de filtro à tabela usando o operador CROSS APPLY.  
  
 Se você não especificar uma função de filtro, a tabela inteira será migrada.  
  
 Ao executar o Assistente para habilitar o banco de dados para Stretch, você pode migrar uma tabela inteira ou especificar uma função de filtro simples no assistente. Se você desejar usar um tipo diferente de função de filtro para selecionar as linhas a serem migradas, siga um destes procedimentos.  
  
-   Saia do assistente e execute a instrução ALTER TABLE para habilitar o Stretch para a tabela e especificar uma função de filtro.  
  
-   Execute a instrução ALTER TABLE para especificar uma função de filtro depois que você sair do assistente.  
  
 A sintaxe ALTER TABLE para adicionar uma função é descrita posteriormente neste artigo.  
  
## <a name="basic-requirements-for-the-filter-function"></a>Requisitos básicos para a função de filtro  
 A função com valor de tabela embutida, necessária para um predicado de filtro Stretch Database é parecida com o exemplo a seguir.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datatype1, @column2 datatype2 [, ...n])  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE <predicate>  
```  
  
 Os parâmetros da função precisam ser identificadores para colunas da tabela.  
  
 A associação do esquema é necessária para impedir que as colunas usadas pela função de filtro sejam descartadas ou alteradas.  
  
### <a name="return-value"></a>Valor de retorno  
 Se a função retornar um resultado não vazio, a linha será qualificada para ser migrada. Caso contrário, isto é, se a função não retornar um resultado, a linha não será qualificada para ser migrada.  
  
### <a name="conditions"></a>Condições  
 O &lt;*predicado*&gt; pode consistir em uma condição ou em várias condições associadas ao operador lógico AND.  
  
```  
<predicate> ::= <condition> [ AND <condition> ] [ ...n ]  
```  
  
 Por sua vez, cada condição pode consistir em uma condição primitiva ou em várias condições primitivas associadas ao operador lógico OR.  
  
```  
<condition> ::= <primitive_condition> [ OR <primitive_condition> ] [ ...n ]  
```  
  
### <a name="primitive-conditions"></a>Condições primitivas  
 Uma condição primitiva pode fazer uma das comparações a seguir.  
  
```  
<primitive_condition> ::=   
{  
<function_parameter> <comparison_operator> constant  
| <function_parameter> { IS NULL | IS NOT NULL }  
| <function_parameter> IN ( constant [ ,...n ] )  
}  
  
```  
  
-   Compare um parâmetro de função a uma expressão constante. Por exemplo, `@column1 < 1000`.  
  
     Veja um exemplo que verifica se o valor de uma coluna *data* é &lt; 1/1/2016.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
    GO  
  
    ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   Aplique o operador IS NULL ou IS NOT NULL a um parâmetro de função.  
  
-   Use o operador IN para comparar um parâmetro de função com uma lista de valores constantes.  
  
     Veja um exemplo que verifica se o valor de uma coluna *shipment_status*  é `IN (N'Completed', N'Returned', N'Cancelled')`.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate(@column1 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
### <a name="comparison-operators"></a>Operadores de comparação  
 Os operadores de comparação a seguir são compatíveis.  
  
 `<, <=, >, >=, =, <>, !=, !<, !>`  
  
```  
<comparison_operator> ::= { < | <= | > | >= | = | <> | != | !< | !> }  
```  
  
### <a name="constant-expressions"></a>Expressões de constante  
 As constantes que você usa em uma função de filtro podem ser qualquer expressão determinística que pode ser avaliada ao definir a função. As expressões de constante podem conter os itens a seguir.  
  
-   Literais Por exemplo, `N’abc’, 123`.  
  
-   Expressões algébricas. Por exemplo, `123 + 456`.  
  
-   Funções determinísticas. Por exemplo, `SQRT(900)`.  
  
-   Conversões determinísticas que usam CAST ou CONVERT. Por exemplo, `CONVERT(datetime, '1/1/2016', 101)`.  
  
### <a name="other-expressions"></a>Outras expressões  
 Você pode usar os operadores BETWEEN e NOT BETWEEN se a função resultante estiver em conformidade com as regras descritas aqui depois de substituir os operadores BETWEEN e NOT BETWEEN pelas expressões equivalentes AND e OR.  
  
 Você não pode usar subconsultas nem funções não determinísticas como RAND() ou GETDATE().  
  
## <a name="add-a-filter-function-to-a-table"></a>Adicionar uma função de filtro a uma tabela  
 Adicione uma função de filtro a uma tabela executando a instrução **ALTER TABLE** e especificando uma função com valor de tabela embutida existente como o valor do parâmetro **FILTER_PREDICATE** . Por exemplo:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 Depois de associar a função à tabela como um predicado, os itens a seguir serão verdadeiros.  
  
-   Na próxima vez que a migração de dados ocorrer, somente as linhas para as quais a função retorna uma valor não vazio serão migradas.  
  
-   As colunas usadas pela função são associadas ao esquema. Não é possível alterar essas colunas, pois uma tabela está usando a função como seu predicado de filtro.  
  
 Não é possível descartar a função com valor de tabela embutida, pois uma tabela está usando a função como seu predicado de filtro. 

> [!TIP]
> Para melhorar o desempenho da função de filtro, crie um índice em colunas usadas pela função.

 ### <a name="passing-column-names-to-the-filter-function"></a>Passando nomes de coluna para a função de filtro
 
 Ao atribuir uma função de filtro a uma tabela, especifique os nomes de coluna passados para a função de filtro com um nome de parte única. Se você especificar um nome de três partes ao passar os nomes de coluna, as consultas subsequentes com base em tabelas habilitada para Stretch falharão.

Por exemplo, se você especificar um nome de coluna de três partes, conforme mostrado no exemplo a seguir, a instrução será executada com êxito, mas as consultas subsequentes com base na tabela falharão.

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(dbo.SensorTelemetry.ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```

Em vez disso, especifique a função de filtro com um nome de coluna de parte única, conforme mostrado no exemplo a seguir.

```sql
ALTER TABLE SensorTelemetry 
  SET ( REMOTE_DATA_ARCHIVE = ON  (
    FILTER_PREDICATE=dbo.fn_stretchpredicate(ScanDate),
    MIGRATION_STATE = OUTBOUND )
  )
```
  
## <a name="addafterwiz"></a>Adicionar uma função de filtro após a execução do Assistente  
  
Se você quiser usar uma função que não pode criar o Assistente **Habilitar o banco de dados para Stretch** , você pode executar a instrução **ALTER TABLE** para especificar uma função depois que sair do assistente. Antes de aplicar uma função, no entanto, você precisa interromper a migração de dados que já está em andamento e trazer os dados migrados de volta. (Para obter mais informações sobre por que isso é necessário, consulte [Substituir uma função de filtro existente](#replacePredicate).)
  
1. Reverta a direção da migração e restaure os dados já migrados. Não é possível cancelar esta operação após ela ser iniciada. Você também incorre em custos no Azure para transferências de dados de saída (saída). Para obter mais informações, consulte [Como os preços do Azure funciona](https://azure.microsoft.com/pricing/details/data-transfers/).  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;   
    ```  
  
2. Aguarde a migração ser concluída. Você pode verificar o status no **Monitor de Stretch Database** do SQL Server Management Studio ou você pode consultar a exibição **sys.dm_db_rda_migration_status** . Para obter mais informações, veja [Monitorar e solucionar problemas de migração de dados](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) ou [sys.dm_db_rda_migration_status](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
3. Crie a função de filtro que você deseja aplicar à tabela.  
  
4. Adicione a função à tabela e reinicie a migração de dados no Azure.  
  
    ```sql  
    ALTER TABLE <table name>  
        SET ( REMOTE_DATA_ARCHIVE  
            (           
                FILTER_PREDICATE = <predicate>,  
                MIGRATION_STATE = OUTBOUND  
            )  
            );   
    ```  
  
## <a name="filter-rows-by-date"></a>Filtrar linhas por data  
 O exemplo a seguir migra linhas onde a coluna **data** contém um valor anterior a 1º de janeiro de 2016.  
  
```sql  
-- Filter by date  
--  
CREATE FUNCTION dbo.fn_stretch_by_date(@date datetime2)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @date < CONVERT(datetime2, '1/1/2016', 101)  
GO  
  
```  
  
## <a name="filter-rows-by-the-value-in-a-status-column"></a>Filtrar linhas pelo valor em uma coluna de status  
 O exemplo a seguir migra linhas onde a coluna **status** contém um dos valores especificados.  
  
```sql  
-- Filter by status column  
--  
CREATE FUNCTION dbo.fn_stretch_by_status(@status nvarchar(128))  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
       RETURN SELECT 1 AS is_eligible WHERE @status IN (N'Completed', N'Returned', N'Cancelled')  
GO  
  
```  
  
## <a name="filter-rows-by-using-a-sliding-window"></a>Filtrar linhas usando uma janela deslizante  
 Para filtrar linhas usando uma janela deslizante, lembre-se dos requisitos a seguir para a função de filtro.  
  
-   A função deve ser determinística. Portanto, você não pode criar uma função que recalcule automaticamente a janela deslizante com o passar do tempo.  
  
-   A função usa associação do esquema. Portanto, não é possível simplesmente atualizar a função "in-loco" todos os dias chamando **ALTER FUNCTION** para mover a janela deslizante.  
  
 Comece com uma função de filtro como o exemplo a seguir, que migra linhas onde a coluna **systemEndTime** contém um valor anterior a 1º de janeiro de 2016.  
  
```sql  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2016-01-01T00:00:00', 101) ;  
  
```  
  
 Aplique a função de filtro à tabela.  
  
```sql  
ALTER TABLE <table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160101(SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
  
```  
  
 Quando você quiser atualizar a janela deslizante, siga estas etapas.  
  
1.  Crie uma nova função que especifique a nova janela deslizante. O exemplo a seguir seleciona datas anteriores a 2 de janeiro de 2016, em vez de 1º de janeiro de 2016.  
  
2.  Substitua a função do filtro anterior pelo novo chamando **ALTER TABLE**, conforme mostrado no exemplo a seguir.  
  
3.  Se preferir, descarte a função de filtro anterior que você não está mais usando chamando **DROP FUNCTION**. (Essa etapa não é mostrada no exemplo.)  
  
```sql  
BEGIN TRAN  
GO  
        /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20160102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2016-01-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as the filter predicate */  
        ALTER TABLE <table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20160102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
  
```  
  
## <a name="more-examples-of-valid-filter-functions"></a>Mais exemplos de funções de filtro válidas  
  
-   O exemplo a seguir combina duas condições primitivas usando o operador lógico AND.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate((@column1 datetime, @column2 nvarchar(15))  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
      WHERE @column1 < N'20150101' AND @column2 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ALTER TABLE table1 SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(date, shipment_status),  
        MIGRATION_STATE = OUTBOUND  
    ) )  
  
    ```  
  
-   O exemplo a seguir usa várias condições e uma conversão determinística com CONVERT.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example1(@column1 datetime, @column2 int, @column3 nvarchar)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101) AND (@column2 < -100 OR @column2 > 100 OR @column2 IS NULL) AND @column3 IN (N'Completed', N'Returned', N'Cancelled')  
    GO  
  
    ```  
  
-   O exemplo a seguir usa funções e operadores matemáticos.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example2(@column1 float)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < SQRT(400) + 10  
    GO  
  
    ```  
  
-   O exemplo a seguir usa os operadores BETWEEN e NOT BETWEEN. Esse uso é válido porque a função resultante está em conformidade com as regras descritas aqui depois que você substitui os operadores BETWEEN e NOT BETWEEN pelas expressões equivalentes AND e OR.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example3(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 BETWEEN 0 AND 100  
                AND (@column2 NOT BETWEEN 200 AND 300 OR @column1 = 50)  
    GO  
  
    ```  
  
     A função anterior é equivalente à função a seguir depois que você substitui os operadores BETWEEN e NOT BETWEEN pelas expressões equivalentes AND e OR.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_stretchpredicate_example4(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 >= 0 AND @column1 <= 100 AND (@column2 < 200 OR @column2 > 300 OR @column1 = 50)  
    GO  
  
    ```  
  
## <a name="examples-of-filter-functions-that-arent-valid"></a>Exemplos de função de filtro que não são válidas  
  
-   A função a seguir não é válida porque contém uma conversão não determinística.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example5(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < CONVERT(datetime, '1/1/2016')  
    GO  
  
    ```  
  
-   A função a seguir não é válida porque ela contém uma chamada de função não determinística.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example6(@column1 datetime)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 < DATEADD(day, -60, GETDATE())  
    GO  
  
    ```  
  
-   A função a seguir não é válida porque contém uma subconsulta.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example7(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 IN (SELECT SupplierID FROM Supplier WHERE Status = 'Defunct')  
    GO  
  
    ```  
  
-   As funções a seguir não são válidas porque expressões que usam operadores algébricos ou funções internas devem ser avaliadas para uma constante quando você define a função. Não é possível incluir referências de coluna em expressões algébricas ou chamadas de função.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example8(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE @column1 % 2 =  0  
    GO  
  
    CREATE FUNCTION dbo.fn_example9(@column1 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE SQRT(@column1) = 30  
    GO  
  
    ```  
  
-   A função a seguir não é válida porque viola as regras descritas aqui depois que você substitui o operador BETWEEN pela expressão AND equivalente.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example10(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
    AS  
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 BETWEEN 1 AND 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
     A função anterior é equivalente à função a seguir depois que você substitui o operador BETWEEN pela expressão AND equivalente. Essa função não é válida porque as condições primitivas podem usar apenas o operador lógico OR.  
  
    ```sql  
    CREATE FUNCTION dbo.fn_example11(@column1 int, @column2 int)  
    RETURNS TABLE  
    WITH SCHEMABINDING   
    AS   
    RETURN  SELECT 1 AS is_eligible  
            WHERE (@column1 >= 1 AND @column1 <= 200 OR @column1 = 300) AND @column2 > 1000  
    GO  
  
    ```  
  
## <a name="how-stretch-database-applies-the-filter-function"></a>Como o Stretch Database aplica a função de filtro  
 O Stretch Database aplica a função de filtro à tabela e determina linhas qualificadas usando o operador CROSS APPLY. Por exemplo:  
  
```sql  
SELECT * FROM stretch_table_name CROSS APPLY fn_stretchpredicate(column1, column2)  
```  
  
 Se a função retornar um resultado não vazio para a linha, a linha será qualificada para ser migrada.  
  
## <a name="replacePredicate"></a>Substituir uma função de filtro existente  
 Você pode substituir uma função de filtro especificado anteriormente executando a instrução **ALTER TABLE** novamente e especificando um novo valor para o parâmetro **FILTER_PREDICATE** . Por exemplo:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = dbo.fn_stretchpredicate2(column1, column2),  
    MIGRATION_STATE = <desired_migration_state>  
  
```  
  
 A nova função com valor de tabela embutida tem os requisitos a seguir.  
  
-   A nova função deve ser menos restritiva do que a função anterior.  
  
-   Todos os operadores que existiam na função antiga devem existir na nova função.  
  
-   A nova função não pode conter operadores que não existam na função antiga.  
  
-   A ordem dos argumentos do operador não pode mudar.  
  
-   Somente valores constantes que fazem parte de uma comparação `<, <=, >, >=`  podem ser alterados de uma maneira que torne a função menos restritiva.  
  
### <a name="example-of-a-valid-replacement"></a>Exemplo de uma substituição válida  
 Suponha que a função a seguir seja a função de filtro atual.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_old(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 A função a seguir é uma substituição válida porque a nova constante de data (que especifica uma data de fechamento posterior) torna a função menos restritiva.  
  
```sql  
CREATE FUNCTION dbo.fn_stretchpredicate_new(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '2/1/2016', 101)  
            AND (@column2 < -50 OR @column2 > 50)  
GO  
  
```  
  
### <a name="examples-of-replacements-that-arent-valid"></a>Exemplos de substituições que não são válidas  
 A função a seguir não é uma substituição válida porque a nova constante de data (que especifica uma data de fechamento anterior) não torna a função menos restritiva.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_1(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2015', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
GO  
  
```  
  
 A função a seguir não é uma substituição válida porque um dos operadores de comparação foi removido.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_2(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -50)  
GO  
  
```  
  
 A função a seguir não é uma substituição válida porque uma nova condição foi adicionada com o operador lógico AND.  
  
```sql  
CREATE FUNCTION dbo.fn_notvalidreplacement_3(@column1 datetime, @column2 int)  
RETURNS TABLE  
WITH SCHEMABINDING   
AS   
RETURN  SELECT 1 AS is_eligible  
        WHERE @column1 < CONVERT(datetime, '1/1/2016', 101)  
            AND (@column2 < -100 OR @column2 > 100)  
            AND (@column2 <> 0)  
GO  
  
```  
  
## <a name="remove-a-filter-function-from-a-table"></a>Remover uma função de filtro de uma tabela  
 Para migrar a tabela inteira em vez de linhas selecionadas, remova a função existente definindo **FILTER_PREDICATE**  como nulo. Por exemplo:  
  
```sql  
ALTER TABLE stretch_table_name SET ( REMOTE_DATA_ARCHIVE = ON (  
    FILTER_PREDICATE = NULL,  
    MIGRATION_STATE = <desired_migration_state>  
) )  
  
```  
  
 Depois de remover a função de filtro, todas as linhas na tabela serão qualificadas para migração. Como resultado, não será possível especificar uma função de filtro para a mesma tabela posteriormente, a menos que você traga de volta todos os dados remotos para a tabela do primeiro Azure. Essa restrição existe para evitar a situação em que as linhas não são qualificadas para migração quando você fornece uma nova função de filtro que já foi migrada para o Azure.  
  
## <a name="check-the-filter-function-applied-to-a-table"></a>Verificar a função de filtro aplicada a uma tabela  
 Para verificar a função de filtro aplicada a uma tabela, abra a exibição de catálogo **sys.remote_data_archive_tables** e verifique o valor da coluna **filter_predicate** . Se o valor for nulo, a tabela inteira será qualificada para arquivamento. Para obter mais informações, veja [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md).  
  
## <a name="security-notes-for-filter-functions"></a>Observações de segurança para funções de filtro  
Uma conta com privilégios de db_owner comprometida pode fazer o seguinte.  
  
-   Criar e aplicar uma função com valor de tabela que consome uma grande quantidade de recursos do servidor ou espera por um longo período, resultando em uma negação de serviço.  
  
-   Criar e aplicar uma função com valor de tabela que torna possível inferir o conteúdo de uma tabela para a qual o usuário negou explicitamente o acesso de leitura.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
