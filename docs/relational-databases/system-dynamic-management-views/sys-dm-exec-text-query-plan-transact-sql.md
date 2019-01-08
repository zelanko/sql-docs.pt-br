---
title: sys.dm_exec_text_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 36c5e28d3e669f05ee0f014e949182b13e816685
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211755"
---
# <a name="sysdmexectextqueryplan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o plano de execução em formato de texto para um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] ou para uma instrução específica dentro do lote. O plano de consulta especificado pelo identificador de plano podem estar armazenados em cache ou em execução no momento. Essa função com valor de tabela é semelhante ao [. DM exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md), mas tem as seguintes diferenças:  
  
-   A saída do plano de consulta é retornada em formato de texto.  
  
-   A saída do plano de consulta não é limitada em tamanho.  
  
-   Instruções individuais podem ser especificadas dentro do lote.  
  
**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>Argumentos  
*plan_handle*  
Identifica exclusivamente um plano de consulta para um lote em cache ou sendo executado atualmente. *plan_handle* está **varbinary(64)**.  
  
O identificador de plano pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-  [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_start_offset* | 0 | PADRÃO  
Indica, em bytes, a posição inicial da consulta que a linha descreve dentro do texto de seu lote ou objeto persistente. *statement_start_offset* está **int**. Um valor de 0 indica o começo do lote. O valor padrão é 0.  
  
O deslocamento de início da instrução pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | PADRÃO  
Indica, em bytes, a posição final da consulta que a linha descreve dentro do texto de seu lote ou objeto pesistente.  
  
*statement_start_offset* está **int**.  
  
Um valor de -1 indica o fim do lote. O valor padrão é -1.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparadas, essa coluna é **nulo**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Por exemplo, um grupo de procedimentos para o **pedidos** aplicativo pode ser nomeado **orderproc; 1**, **orderproc; 2**e assim por diante. Para lotes ad hoc e preparadas, essa coluna é **nulo**.<br /><br /> A coluna é anulável.|  
|**Criptografado**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**nvarchar(max)**|Contém a representação de plano de execução de tempo de compilação do plano de execução de consulta que é especificado com *plan_handle*. O Showplan está em formato de texto. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.|  
  
## <a name="remarks"></a>Comentários  
 Sob as seguintes condições, nenhuma saída Showplan é retornada na **plano** coluna da tabela retornada para **DM exec_text_query_plan**:  
  
-   Se o plano de consulta é especificado usando *plan_handle* foi retirado do cache de planos, o **query_plan** coluna da tabela retornada é nula. Por exemplo, essa condição pode ocorrer se houver um atraso entre quando o identificador de plano foi capturado e quando ele foi usado com **DM exec_text_query_plan**.  
  
-   Algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] não são colocadas em cache, como instruções de operação em massa ou instruções que contêm literais de cadeia de caracteres maiores que 8 KB. Showplans para tais instruções não podem ser recuperados usando **DM exec_text_query_plan** porque eles não existem no cache.  
  
-   Se um [!INCLUDE[tsql](../../includes/tsql-md.md)] lote ou procedimento armazenado contém uma chamada para uma função definida pelo usuário ou uma chamada para SQL dinâmico, por exemplo, usando EXEC (*cadeia de caracteres*), o XML Showplan compilado para a função definida pelo usuário não está incluída na tabela retornado por **DM exec_text_query_plan** para o lote ou procedimento armazenado. Em vez disso, você deve fazer uma chamada separada para **DM exec_text_query_plan** para o *plan_handle* que corresponde à função definida pelo usuário.  
  
Quando usa uma consulta ad hoc [simples](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) ou [parametrização forçada](../../relational-databases/query-processing-architecture-guide.md#ForcedParam), o **query_plan** coluna conterá apenas o texto da instrução e não o plano de consulta real. Para retornar o plano de consulta, chame **DM exec_text_query_plan** do identificador do plano de consulta parametrizada preparada. Você pode determinar se a consulta foi parametrizada referenciando a **sql** coluna da [sys. syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) modo de exibição ou a coluna de texto o [DM exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)exibição de gerenciamento dinâmico.  
  
## <a name="permissions"></a>Permissões  
 Para executar **DM exec_text_query_plan**, um usuário deve ser um membro do **sysadmin** função de servidor fixa ou ter a permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. Recuperando o plano de consulta em cache para uma consulta ou lote Transact-SQL de execução lenta  
 Se uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] ou lote for executado por muito tempo em uma determinada conexão com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recupere o plano de execução para essa consulta ou lote para descobrir o que está causando o retardo. O exemplo a seguir mostra como recuperar o Showplan para uma consulta ou lote de execução lenta.  
  
> [!NOTE]  
> Para executar este exemplo, substitua os valores para *session_id* e *plan_handle* com valores específicos ao seu servidor.  
  
 Primeiramente, recupere a identificação de processo do servidor (SPID) para o processo que está executando a consulta ou lote usando o procedimento armazenado `sp_who`:  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 O conjunto de resultados retornado por `sp_who` indica que o SPID é `54`anos. Você pode usar o SPID com a exibição de gerenciamento dinâmico `sys.dm_exec_requests` para recuperar o identificador de plano, por meio da seguinte consulta:  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 A tabela que é retornada por **. DM exec_requests** indica que o identificador de plano para a consulta ou lote em execução lenta é `0x06000100A27E7C1FA821B10600`. O exemplo a seguir retorna o plano de consulta para o identificador de plano especificado e usa os valores padrão 0 e -1 para retornar todas as instruções na consulta ou lote.  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>b. Recuperando todo o plano de consulta do cache de plano  
 Para recuperar um instantâneo de todos os planos de consulta residindo no cache de plano, recupere os identificadores de plano de todas as consultas no cachê, consultando a exibição de gerenciamento dinâmico `sys.dm_exec_cached_plans`. Os identificadores de plano são armazenados na coluna `plan_handle` de `sys.dm_exec_cached_plans`. Em seguida, use o operador CROSS APPLY para transmitir o identificador de plano a `sys.dm_exec_text_query_plan`, como se segue. O plano de execução de saída de cada plano atualmente no cache de plano está na `query_plan` coluna da tabela que é retornada.  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Recuperando todo plano de consulta para o qual o servidor coletou estatísticas de consulta do cache de plano  
 Para recuperar um instantâneo de todos os planos de consulta para os quais o servidor reuniu estatísticas que residem atualmente no cache de plano, recupere os identificadores desses planos no cache consultando a exibição de gerenciamento dinâmico `sys.dm_exec_query_stats`. Os identificadores de plano são armazenados na coluna `plan_handle` de `sys.dm_exec_query_stats`. Em seguida, use o operador CROSS APPLY para transmitir o identificador de plano a `sys.dm_exec_text_query_plan`, como se segue. A saída de plano de execução de cada plano está na coluna `query_plan` da tabela retornada.  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Recuperando informações sobre as cinco principais consultas por tempo médio de CPU  
 O exemplo a seguir retorna os planos de consulta e o tempo médio de CPU das cinco principais consultas. O **DM exec_text_query_plan** função especifica os valores padrão 0 e -1 para retornar todas as instruções no lote no plano de consulta.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
