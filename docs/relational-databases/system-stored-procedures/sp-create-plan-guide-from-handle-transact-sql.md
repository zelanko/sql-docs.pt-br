---
title: sp_create_plan_guide_from_handle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide_from_handle_TSQL
- sp_create_plan_guide_from_handle
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide_from_handle
ms.assetid: 02cfb76f-a0f9-4b42-a880-1c3e7d64fe41
author: stevestein
ms.author: sstein
ms.openlocfilehash: a5e4ad5d6f3d0b2e35633694d65e58dd782cc3ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75688251"
---
# <a name="sp_create_plan_guide_from_handle-transact-sql"></a>sp_create_plan_guide_from_handle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma ou mais guias de plano de um plano de consulta no cache de plano. É possível usar esse procedimento armazenado para garantir que o otimizador de consulta use sempre um plano de consulta específico para uma consulta específica. Para obter mais informações sobre guias de plano, consulte [Plan Guides](../../relational-databases/performance/plan-guides.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_create_plan_guide_from_handle [ @name = ] N'plan_guide_name'  
    , [ @plan_handle = ] plan_handle  
    , [ [ @statement_start_offset = ] { statement_start_offset | NULL } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name = ] N '*plan_guide_name*'  
 É o nome da guia de plano. Os nomes de guia de plano têm escopo no banco de dados atual. *plan_guide_name* deve estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md) e não pode começar com o sinal numérico (#). O comprimento máximo de *plan_guide_name* é de 124 caracteres.  
  
 [ @plan_handle = ] *plan_handle*  
 Identifica um lote no cache de plano. *plan_handle* é **varbinary (64)**. *plan_handle* pode ser obtida na exibição de gerenciamento dinâmico [Sys. dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) .  
  
 [ @statement_start_offset = ] { *statement_start_offset* | NULL}]  
 Identifica a posição inicial da instrução dentro do lote do *plan_handle*especificado. *statement_start_offset* é **int**, com um padrão de NULL.  
  
 O deslocamento da instrução corresponde à coluna statement_start_offset na exibição de gerenciamento dinâmico [Sys. dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) .  
  
 Quando NULL é especificado ou um deslocamento de instrução não é especificado, um guia de plano é criado para cada instrução no lote usando o plano de consulta do identificador de plano especificado. Os guias de plano resultantes são equivalentes aos que usam a dica de consulta USE PLAN para forçar o uso de um determinado plano.  
  
## <a name="remarks"></a>Comentários  
 Um guia de plano não pode ser criado para todos os tipos de instrução. Se um guia de plano não puder ser criado para uma instrução no lote, o procedimento armazenado ignorará a instrução e avançará para a próxima instrução do lote. Caso uma instrução ocorra várias vezes no mesmo lote, o plano da última ocorrência será habilitado, e os planos anteriores da instrução serão desabilitados. Se nenhuma instrução do lote puder ser usada em um guia de plano, o erro 10532 será gerado e a instrução falhará. Recomendamos sempre que você obtenha o identificador de plano na exibição de gerenciamento dinâmico sys.dm_exec_query_stats para ajudar a evitar a possibilidade de ocorrência desse erro.  
  
> [!IMPORTANT]  
>  sp_create_plan_guide_from_handle cria guias de plano com base em planos à medida que eles vão aparecendo no cache do plano. Isso significa que o texto do lote, as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e o Plano de execução XML são obtidos caractere por caractere (incluindo qualquer valor literal enviado à consulta) do cache do plano no guia de plano resultante. Essas cadeias de caracteres de texto podem conter informações confidenciais armazenadas nos metadados do banco de dados. Os usuários com permissões apropriadas podem exibir essas informações usando a exibição de catálogo sys. plan_guides e a caixa de diálogo Propriedades do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]guia de **plano** no. Para garantir que as informações confidenciais não sejam divulgadas em um guia de plano, recomendamos revisar os guias criados no cache do plano.  
  
## <a name="creating-plan-guides-for-multiple-statements-within-a-query-plan"></a>Criando guias de plano para várias instruções em um plano de consulta  
 Assim como sp_create_plan_guide, sp_create_plan_guide_from_handle remove o plano de consulta do lote ou módulo de destino do cache do plano. Isso é feito para assegurar que todos os usuários comecem a usar o novo guia de plano. Ao criar um guia de plano para várias instruções em um único plano de consulta, você pode adiar a remoção do plano do cache criando todos os guias de plano em uma transação explícita. Esse método permite que o plano permaneça no cache até que a transação seja concluída e um guia de plano para cada instrução especificada seja criado. Consulte o Exemplo B.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE`. Além disso, são solicitadas permissões individuais para cada guia de plano criado, usando sp_create_plan_guide_from_handle. Para criar um guia de plano do tipo OBJECT `ALTER` , é necessária a permissão no objeto referenciado. Para criar um guia de plano do tipo SQL ou TEMPLATE `ALTER` requer permissão no banco de dados atual. Para determinar o tipo de guia de plano que será criado, execute a seguinte consulta:  
  
```sql  
SELECT cp.plan_handle, sql_handle, st.text, objtype   
FROM sys.dm_exec_cached_plans AS cp  
JOIN sys.dm_exec_query_stats AS qs ON cp.plan_handle = qs.plan_handle  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st;  
```  
  
 Na linha que contém a instrução para a qual está sendo criado o guia de plano, examine a coluna `objtype` no conjunto de resultados. Um valor de `Proc` indica que o guia de plano é do tipo OBJECT. Outros valores, como `AdHoc` ou `Prepared`, indicam que o guia de plano é do tipo SQL.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-plan-guide-from-a-query-plan-in-the-plan-cache"></a>a. Criando um guia de plano de um plano de consulta no cache de plano  
 O exemplo a seguir cria um guia de plano para uma instrução SELECT única especificando um plano de consulta no cache do plano. O exemplo começa pela execução de uma instrução `SELECT` única para a qual o guia de plano será criado. O plano para esta consulta é examinado usando as exibições de gerenciamento dinâmico `sys.dm_exec_sql_text` e `sys.dm_exec_text_query_plan`. Em seguida, o guia de plano é criado para a consulta por meio da especificação do plano de consulta no cache do plano associado à consulta. A instrução final no exemplo verifica se o guia de plano existe.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT WorkOrderID, p.Name, OrderQty, DueDate  
FROM Production.WorkOrder AS w   
JOIN Production.Product AS p ON w.ProductID = p.ProductID  
WHERE p.ProductSubcategoryID > 4  
ORDER BY p.Name, DueDate;  
GO  
-- Inspect the query plan by using dynamic management views.  
SELECT * FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle)  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
-- Create a plan guide for the query by specifying the query plan in the plan cache.  
DECLARE @plan_handle varbinary(64);  
DECLARE @offset int;  
SELECT @plan_handle = plan_handle, @offset = qs.statement_start_offset  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
  
EXECUTE sp_create_plan_guide_from_handle   
    @name =  N'Guide1',  
    @plan_handle = @plan_handle,  
    @statement_start_offset = @offset;  
GO  
-- Verify that the plan guide is created.  
SELECT * FROM sys.plan_guides  
WHERE scope_batch LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
```  
  
### <a name="b-creating-multiple-plan-guides-for-a-multistatement-batch"></a>B. Criando vários guias de plano para um lote com várias instruções  
 O exemplo a seguir cria um guia de plano para duas instruções de um lote com várias instruções. Os guias de plano são criados em uma transação explícita de modo que o plano de consulta do lote não seja removido do cache do plano após a criação do primeiro guia de plano. O exemplo começa pela execução de um lote com várias instruções. O plano do lote é examinado com o uso de exibições de gerenciamento dinâmico. Observe que uma linha para cada instrução no lote é retornada. Um guia de plano é criado para a primeira e a terceira instruções no lote por meio da especificação do parâmetro `@statement_start_offset`. A instrução final no exemplo verifica se os guias de plano existem.  
  
 [!code-sql[PlanGuides#Create_From_Handle2](../../relational-databases/system-stored-procedures/codesnippet/tsql/sp-create-plan-guide-fro_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys. dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [Guias de plano](../../relational-databases/performance/plan-guides.md)   
 [&#41;&#40;Transact-SQL de sp_create_plan_guide](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys. dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys. dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
  
  
