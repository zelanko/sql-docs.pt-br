---
title: CHANGETABLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHANGETABLE_TSQL
- CHANGETABLE
dev_langs: TSQL
helpviewer_keywords:
- CHANGETABLE
- change tracking [SQL Server], CHANGETABLE
ms.assetid: d405fb8d-3b02-4327-8d45-f643df7f501a
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 233a613024b4e216501ea7baaaf9a363325e5998
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="changetable-transact-sql"></a>CHANGETABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna as informações de controle de alterações de uma tabela. Você pode usar essa instrução para retornar todas as alterações de uma tabela ou as informações de controle de alterações de uma linha específica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHANGETABLE (  
    { CHANGES table , last_sync_version  
    | VERSION table , <primary_key_values> } )  
[AS] table_alias [ ( column_alias [ ,...n ] )  
  
<primary_key_values> ::=  
( column_name [ , ...n ] ) , ( value [ , ...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 ALTERAÇÕES *tabela* , *last_sync_version*  
 Retorna informações de controle de todas as alterações em uma tabela que ocorreu desde a versão que é especificada pelo *last_sync_version*.  
  
 *table*  
 É a tabela definida pelo usuário na qual as alterações controladas são obtidas. O controle de alterações deve ser ativado na tabela. Um nome de tabela de uma, duas, três ou quatro partes pode ser usado. O nome da tabela pode ser um sinônimo para a tabela.  
  
 *last_sync_version*  
 Quando obtém alterações, o aplicativo chamador deve especificar o ponto a partir do qual são necessárias alterações. last_sync_version especifica esse ponto. A função retorna informações de todas as linhas que foram alteradas desde essa versão. O aplicativo faz uma consulta para receber alterações com uma versão maior que last_sync_version.  
  
 Normalmente, antes de obter as alterações, o aplicativo chama **change_tracking_current_version ()** para obter a versão que será usada as próximas alterações de tempo são necessárias. Por isso, o aplicativo não precisa interpretar ou entender o valor real.  
  
 Como last_sync_version é obtido pelo aplicativo chamador, o aplicativo tem que manter o valor. Se o aplicativo perder este valor, ele deverá reinicializar os dados.  
  
 *last_sync_version* é **bigint**. O valor deve ser escalar. Uma expressão causará um erro de sintaxe.  
  
 Se o valor for NULL, todas as alterações efetuadas serão retornadas.  
  
 *last_sync_version* devem ser validadas para garantir que ele não é muito antigo, pois algumas ou todas as informações de alteração podem ser apagadas backup de acordo com o período de retenção configurado para o banco de dados. Para obter mais informações, consulte [CHANGE_TRACKING_MIN_VALID_VERSION &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md) e [ALTER definir opções de banco de dados &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 VERSÃO *tabela*, {< primary_key_values >}  
 Retorna as informações de controle de alterações mais recentes de uma linha especificada. Os valores de chave primária devem identificar a linha. <primary_key_values> identifica as colunas de chave primária e especifica os valores. Os nomes de coluna de chave primária podem ser especificados em qualquer ordem.  
  
 *Table*  
 É a tabela definida pelo usuário na qual devem ser obtidas as informações de controle de alterações. O controle de alterações deve ser ativado na tabela. Um nome de tabela de uma, duas, três ou quatro partes pode ser usado. O nome da tabela pode ser um sinônimo para a tabela.  
  
 *column_name*  
 Especifica o nome de coluna/colunas de chave primária. Podem ser especificados vários nomes de coluna em qualquer ordem.  
  
 *Value*  
 É o valor da chave primária. Se houver várias colunas de chave primária, os valores devem ser especificados na mesma ordem que as colunas apareçam no *column_name* lista.  
  
 [COMO] *table_alias* [(*column_alias* [,... *n* ] ) ]  
 Fornece nomes para os resultados que são retornados por CHANGETABLE.  
  
 *table_alias*  
 É o alias da tabela de que é retornada por CHANGETABLE. *table_alias* é obrigatório e deve ser válido [identificador](../../relational-databases/databases/database-identifiers.md).  
  
 *column_alias*  
 É um alias de coluna opcional ou lista de aliases de coluna opcional para as colunas que são retornadas por CHANGETABLE. Isso permite que os nomes de colunas sejam personalizados caso haja nomes duplicados nos resultados.  
  
## <a name="return-types"></a>Tipos de retorno  
 **table**  
  
## <a name="return-values"></a>Valores de retorno  
  
### <a name="changetable-changes"></a>CHANGETABLE CHANGES  
 Quando CHANGES é especificado, são retornadas zero ou mais linhas que têm as colunas a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|Valor de versão associado à última alteração efetuada na linha|  
|SYS_CHANGE_CREATION_VERSION|**bigint**|Valores de versão associados à última operação de inserção.|  
|SYS_CHANGE_OPERATION|**nchar (1)**|Especifica o tipo de alteração:<br /><br /> **U** = atualização<br /><br /> **Eu** = Insert<br /><br /> **D** = excluir|  
|SYS_CHANGE_COLUMNS|**varbinary(4100)**|Lista as colunas alteradas desde a last_sync_version (a linha de base). Observe que as colunas computadas nunca são listadas como alteradas.<br /><br /> O valor será NULL quando qualquer uma das condições a seguir for verdadeira:<br /><br /> O controle de alterações da coluna não está habilitado.<br /><br /> A operação é de inserção ou exclusão.<br /><br /> Todas as colunas de chave não primária foram atualizadas em uma operação. Este valor binário não deve ser interpretado diretamente. Em vez disso, para interpretá-lo, use [change_tracking_is_column_in_mask ()](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md).|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|Alterar as informações de contexto que você pode opcionalmente especificar usando o [WITH](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md) cláusula como parte de uma instrução INSERT, UPDATE ou DELETE.|  
|\<valor da coluna de chave primária >|Igual às colunas de tabela de usuário|Os valores de chave primária da tabela controlada. Esses valores identificam exclusivamente cada linha da tabela do usuário.|  
  
### <a name="changetable-version"></a>CHANGETABLE VERSION  
 Quando VERSION é especificado, uma linha que tem as seguintes colunas é retornada.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|Valor de versão de alteração atual associado à linha.<br /><br /> O valor será NULL se uma alteração não tiver sido efetuada por um período maior que o de retenção do controle de alterações ou se a linha não tiver sido alterada desde que o controle de alterações foi habilitado.|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|Altere as informações de contexto que podem opcionalmente ser especificadas usando a cláusula WITH como parte de uma instrução INSERT, UPDATE ou DELETE.|  
|\<valor da coluna de chave primária >|Igual às colunas de tabela de usuário|Os valores de chave primária da tabela controlada. Esses valores identificam exclusivamente cada linha da tabela do usuário.|  
  
## <a name="remarks"></a>Remarks  
 Em geral, a função CHANGETABLE é usada na cláusula FROM de uma consulta como se fosse uma tabela.  
  
## <a name="changetablechanges"></a>CHANGETABLE(CHANGES...)  
 Para obter dados de linha para linhas novas ou modificadas, una o conjunto de resultados à tabela do usuário utilizando as colunas de chave primária. Somente uma linha é retornada para cada linha na tabela de usuário que tenha sido alterada, mesmo se houver várias alterações na mesma linha desde o *last_sync_version* valor.  
  
 Alterações de coluna de chave primária nunca são marcadas como atualizações. Se um valor de chave primária for alterado, será considerado como excluído do valor antigo e inserido no valor novo.  
  
 Se você excluir uma linha e depois inserir uma linha que tenha a chave primária antiga, a alteração será vista como uma atualização em todas as colunas da linha.  
  
 Os valores retornados para as colunas SYS_CHANGE_OPERATION e SYS_CHANGE_COLUMNS são relativas a linha de base (last_sync_version) especificada. Por exemplo, se uma operação de inserção foi feita na versão 10 e uma operação de atualização na versão 15 e se a linha de base *last_sync_version* é 12, uma atualização será relatada. Se o *last_sync_version* valor é 8, uma inserção será relatada. SYS_CHANGE_COLUMNS nunca informará colunas computadas como tendo sido atualizadas.  
  
 Geralmente, todas as operações que inserem, atualizam ou excluem dados em tabelas de usuário são controladas, inclusive a instrução MERGE.  
  
 As seguintes operações que afetam dados de tabela de usuário não são controladas:  
  
-   Executando a instrução UPDATETEXT  
  
     Esta instrução é preterida e será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, as alterações feitas usando a cláusula .WRITE da instrução UPDATE são controladas.  
  
-   Excluindo linhas usando TRUNCATE TABLE  
  
     Quando uma tabela está truncada, as informações do controle de alterações, associadas à tabela, são redefinidas como se o controle de alterações tivesse acabado de ser habilitado na tabela. Um aplicativo cliente deverá sempre validar sua última versão sincronizada. A validação falhará se a tabela foi truncada.  
  
## <a name="changetableversion"></a>CHANGETABLE(VERSION...)  
 Um conjunto de resultados vazio será retornado se uma chave primária inexistente for especificada.  
  
 O valor de SYS_CHANGE_VERSION pode ser NULL se nenhuma alteração tiver sido efetuada por um período maior que o de retenção (por exemplo, a limpeza removeu a informação de alteração) ou se a linha não tiver sido alterada desde que o controle de alterações foi habilitado para a tabela.  
  
## <a name="permissions"></a>Permissões  
 Requer as seguintes permissões em uma tabela que é especificado pelo *tabela* valor para obter informações de controle de alterações:  
  
-   Permissão SELECT nas colunas de chave primária  
  
-   VIEW CHANGE TRACKING  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-rows-for-an-initial-synchronization-of-data"></a>A. Retornando linhas para uma sincronização inicial de dados  
 O exemplo a seguir mostra como obter dados para uma sincronização inicial dos dados da tabela. A consulta retorna todos os dados de linha e suas versões associadas. Você pode inserir ou adicionar esses dados ao sistema que conterá os dados sincronizados.  
  
```sql  
-- Get all current rows with associated version  
SELECT e.[Emp ID], e.SSN, e.FirstName, e.LastName,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_CONTEXT  
FROM Employees AS e  
CROSS APPLY CHANGETABLE   
    (VERSION Employees, ([Emp ID], SSN), (e.[Emp ID], e.SSN)) AS c;  
```  
  
### <a name="b-listing-all-changes-that-were-made-since-a-specific-version"></a>B. Listando todas as alterações efetuadas desde uma versão específica  
 O exemplo a seguir lista todas as alterações feitas em uma tabela desde a versão especificada (`@last_sync_version)`. [Emp ID] e SSN são colunas em uma chave primária composta.  
  
```sql  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT [Emp ID], SSN,  
    SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION,  
    SYS_CHANGE_COLUMNS, SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS C;  
```  
  
### <a name="c-obtaining-all-changed-data-for-a-synchronization"></a>C. Obtendo todos os dados alterados para uma sincronização  
 O exemplo a seguir mostra como você pode obter todos os dados alterados. Essa consulta une as informações de controle de alterações à tabela de usuário de forma que as informações da tabela de usuário sejam retornadas. Um `LEFT OUTER JOIN` é usado de forma que uma linha seja retornada para as linhas excluídas.  
  
```sql  
-- Get all changes (inserts, updates, deletes)  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT e.FirstName, e.LastName, c.[Emp ID], c.SSN,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_OPERATION,  
    c.SYS_CHANGE_COLUMNS, c.SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS c  
    LEFT OUTER JOIN Employees AS e  
        ON e.[Emp ID] = c.[Emp ID] AND e.SSN = c.SSN;  
```  
  
### <a name="d-detecting-conflicts-by-using-changetableversion"></a>D. Detectando conflitos usando CHANGETABLE (VERSION...)  
 O exemplo a seguir mostra como atualizar uma linha apenas se ela não tiver sido alterada desde a última sincronização. O número de versão da linha específica é obtido usando `CHANGETABLE`. Se a linha tiver sido atualizada, as alterações não serão efetuadas e a consulta retornará informações sobre a alteração mais recente efetuada na linha.  
  
```sql  
-- @last_sync_version must be set to a valid value  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        (SELECT CT.SYS_CHANGE_VERSION FROM   
            CHANGETABLE(VERSION SalesLT.Product,  
            (ProductID), (P.ProductID)) AS CT),  
        0);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções do controle de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [CHANGE_TRACKING_IS_COLUMN_IN_MASK &#40; Transact-SQL &#41;](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40; Transact-SQL &#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)  
  
  
