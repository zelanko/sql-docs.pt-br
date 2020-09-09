---
description: sys.dm_exec_query_plan (Transact-SQL)
title: sys. dm_exec_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 741cfebb7eb50e37512a5778691ab61700f9d98e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548522"
---
# <a name="sysdm_exec_query_plan-transact-sql"></a>sys.dm_exec_query_plan (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna o plano de execução em formato XML para o lote especificado pelo identificador de plano. O plano especificado pelo identificador do plano pode estar em cache ou estar sendo executado.  
  
O esquema XML para o SHOWPLAN é publicado e está disponível neste [site da Microsoft](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409). Ele fica disponível também no diretório em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_exec_query_plan(plan_handle)  
```  
  
## <a name="arguments"></a>Argumentos  
*plan_handle*  
É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de planos ou está em execução no momento. *plan_handle* é **varbinary (64)**.   

Os *plan_handle* podem ser obtidos nos seguintes objetos de gerenciamento dinâmico:
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys. dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys. dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DBID**|**smallint**|A ID do banco de dados de contexto em vigor quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente a esse plano foi compilada. Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.<br /><br /> A coluna é anulável.|  
|**objectid**|**int**|A identificação do objeto (por exemplo, procedimento armazenado ou função definida pelo usuário) para este plano de consulta. Para lotes ad hoc e preparados, essa coluna é **null**.<br /><br /> A coluna é anulável.|  
|**number**|**smallint**|Inteiro de procedimento armazenado numerado. Por exemplo, um grupo de procedimentos para o aplicativo de ** pedidos** pode ser nomeado **orderproc;1**, **orderproc;2** e assim por diante. Para lotes ad hoc e preparados, essa coluna é **null**.<br /><br /> A coluna é anulável.|  
|**criptografados**|**bit**|Indica se o procedimento armazenado correspondente está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = criptografado<br /><br /> A coluna não é anulável.|  
|**query_plan**|**xml**|Contém a representação de SHOWPLAN de tempo de compilação do plano de execução de consulta especificado com *plan_handle*. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário.<br /><br /> A coluna é anulável.|  
  
## <a name="remarks"></a>Comentários  
 Sob as seguintes condições, nenhuma saída Showplan é retornada na coluna **query_plan** da tabela retornada para ** sys.dm_exec_query_plan**:  
  
-   Se o plano de consulta especificado usando *plan_handle* tiver sido removido do cache de plano, a coluna **query_plan** da tabela retornada será nula. Por exemplo, essa condição pode ocorrer se houver um atraso de tempo entre o momento de captura e de utilização do identificador de plano com ** sys.dm_exec_query_plan**.  
  
-   Algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] não são colocadas em cache, como instruções de operação em massa ou instruções que contêm literais de cadeia de caracteres maiores que 8 KB. Showplans XML para tais instruções não podem ser recuperados usando **sys.dm_exec_text_query_plan** a menos que o lote esteja em execução, atualmente, porque eles não existem no cache.  
  
-   Se um [!INCLUDE[tsql](../../includes/tsql-md.md)] lote ou procedimento armazenado contiver uma chamada para uma função definida pelo usuário ou uma chamada para SQL dinâmico, por exemplo, usando exec (*String*), o Showplan XML compilado para a função definida pelo usuário não será incluído na tabela retornada por **Sys. dm_exec_query_plan** para o lote ou procedimento armazenado. Em vez disso, você deve fazer uma chamada separada para **Sys. dm_exec_query_plan** para o identificador de plano que corresponde à função definida pelo usuário.  
  
 Quando uma consulta ad hoc usa parametrização simples ou forçada, a coluna **query_plan** conterá somente o texto de instrução e não o plano de consulta real. Para retornar ao plano de consulta, chame ** sys.dm_exec_query_plan** para o identificador do plano da consulta parametrizada preparada. Você pode determinar se a consulta foi parametrizada referenciando a coluna **sql** da exibição [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) ou a coluna de texto da exibição de gerenciamento dinâmico [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
> [!NOTE] 
> Devido a uma limitação no número de níveis aninhados permitido no tipo de dados **XML** , **Sys. dm_exec_query_plan** não pode retornar planos de consulta que atendam ou ultrapassem 128 níveis de elementos aninhados. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta condição evitava que o plano de consulta retornasse e gerasse um erro 6335. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versões posteriores, a coluna **QUERY_PLAN** retorna NULL.   
> Você pode usar a função de gerenciamento dinâmico de [&#41;de dm_exec_text_query_plan &#40;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md) para retornar a saída do plano de consulta no formato de texto.  
  
## <a name="permissions"></a>Permissões  
 Para executar **Sys. dm_exec_query_plan**, um usuário deve ser membro da função de servidor fixa **sysadmin** ou ter a `VIEW SERVER STATE` permissão no servidor.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar a exibição de gerenciamento dinâmico **sys.dm_exec_query_plan**.  
  
 Para visualizar os Showplans XML, execute as consultas a seguir no Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e clique em **ShowPlanXML** na coluna **query_plan** da tabela retornada por **sys.dm_exec_query_plan**. O plano de execução XML é exibido no painel de resumo do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para salvar o Showplan XML em um arquivo, clique com o botão direito do mouse em **ShowplanXml** na coluna **query_plan** , clique em **salvar resultados como**, nomeie o arquivo no formato \<*file_name*> . sqlplan; por exemplo, MyXMLShowplan. sqlplan.  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>a. Recuperar o plano de consulta em cache para uma consulta ou lote Transact-SQL de execução lenta  
 Planos de Consulta para vários tipos de lotes [!INCLUDE[tsql](../../includes/tsql-md.md)], como lotes ad hoc, procedimentos armazenados e funções definidas pelo usuário, são colocados em cache em uma área da memória denominada cache de plano. Cada plano de consulta em cache é identificado por um identificador exclusivo chamado de identificador de plano. Você pode especificar esse identificador de plano com a exibição de gerenciamento dinâmico **sys.dm_exec_query_plan** para recuperar o plano de execução para uma consulta ou lote [!INCLUDE[tsql](../../includes/tsql-md.md)] em particular.  
  
 Se uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] ou lote for executado por muito tempo em uma determinada conexão com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recupere o plano de execução para essa consulta ou lote para descobrir o que está causando o retardo. O exemplo a seguir mostra como recuperar o plano de execução XML para uma consulta ou lote de execução lenta.  
  
> [!NOTE]  
>  Para executar este exemplo, substitua os valores de *session_id* e *plan_handle* com valores específicos do seu servidor.  
  
 Primeiramente, recupere a identificação de processo do servidor (SPID) para o processo que está executando a consulta ou lote usando o procedimento armazenado `sp_who`:  
  
```sql  
USE master;  
GO  
exec sp_who;  
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
  
 A tabela retornada por **Sys. dm_exec_requests** indica que o identificador de plano para a consulta em execução lenta ou o lote é `0x06000100A27E7C1FA821B10600` , que você pode especificar como o argumento de *plan_handle* com `sys.dm_exec_query_plan` para recuperar o plano de execução em formato XML da seguinte maneira. O plano de execução em formato XML para a consulta ou lote em execução lenta é contido na coluna **query_plan** da tabela retornada por `sys.dm_exec_query_plan`.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. Recuperar todo o plano de consulta do cache de plano  
 Para recuperar um instantâneo de todos os planos de consulta residindo no cache de plano, recupere os identificadores de plano de todas as consultas no cachê, consultando a exibição de gerenciamento dinâmico `sys.dm_exec_cached_plans`. Os identificadores de plano são armazenados na coluna `plan_handle` de `sys.dm_exec_cached_plans`. Em seguida, use o operador CROSS APPLY para transmitir o identificador de plano a `sys.dm_exec_query_plan`, como se segue. A saída de plano de execução XML de cada plano atualmente no cache de plano está na coluna `query_plan` da tabela retornada.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_cached_plans AS cp 
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Recuperar todo plano de consulta para o qual o servidor reuniu estatísticas de consulta do cache de plano  
 Para recuperar um instantâneo de todos os planos de consulta para os quais o servidor reuniu estatísticas que residem atualmente no cache de plano, recupere os identificadores desses planos no cache consultando a exibição de gerenciamento dinâmico `sys.dm_exec_query_stats`. Os identificadores de plano são armazenados na coluna `plan_handle` de `sys.dm_exec_query_stats`. Em seguida, use o operador CROSS APPLY para transmitir o identificador de plano a `sys.dm_exec_query_plan`, como se segue. O plano de execução XML produzido para cada plano para o qual o servidor reuniu estatísticas atualmente no cache de plano está na coluna `query_plan` da tabela retornada.  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_stats AS qs 
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Recuperar as informações sobre as cinco principais consultas por tempo médio de CPU  
 O exemplo a seguir retorna os planos e o tempo médio de CPU das cinco principais consultas.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
   plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys. dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [sys. dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  
