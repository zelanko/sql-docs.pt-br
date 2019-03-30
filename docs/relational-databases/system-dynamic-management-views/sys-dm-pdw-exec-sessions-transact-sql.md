---
title: sys.dm_pdw_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 331bb44faa2938241de98a6bff08f1e660583c4e
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657820"
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as sessões abertas no momento ou recentemente no dispositivo. Ele lista uma linha por sessão.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|A id da consulta atual ou a última consulta executada (se a sessão é ENCERRADA e a consulta estava em execução no momento do encerramento). A chave para este modo de exibição.|Exclusivo em todas as sessões no sistema.|  
|status|**nvarchar(10)**|Para sessões atuais, identifica se a sessão está atualmente ativo ou ocioso. Para sessões anteriores, a sessão de status poderá mostrar fechado ou eliminado (se a sessão foi fechada à força).|'ACTIVE', 'FECHADO', 'OCIOSA', 'ENCERRADO'|  
|request_id|**nvarchar(32)**|A id da consulta atual ou da última consulta executada.|Exclusivo entre todas as solicitações no sistema. NULL se nenhum tiver sido executada.|  
|security_id|**varbinary(85)**|ID de segurança da entidade de segurança executando a sessão.||  
|login_name|**nvarchar(128)**|O nome de logon da entidade de segurança executando a sessão.|Qualquer cadeia de caracteres de acordo com as convenções de nomenclatura do usuário.|  
|login_time|**datetime**|Data e hora em que o usuário conectado e esta sessão foi criada.|Válido **datetime** antes da hora atual.|  
|query_count|**int**|Captura o número de consultas/requeststhis sessão foi executada desde a criação.|Maior que ou igual a 0.|  
|is_transactional|**bit**|Captura se uma sessão está atualmente em uma transação ou não.|0 para a confirmação automática, 1 para transacional.|  
|client_id|**nvarchar(255)**|Captura informações de cliente para a sessão.|Qualquer cadeia de caracteres válida.|  
|app_name|**nvarchar(255)**|Captura informações de nome de aplicativo, opcionalmente, definidas como parte do processo de conexão.|Qualquer cadeia de caracteres válida.|  
|sql_spid|**int**|O número de identificação de SPID. Use o `session_id` esta sessão. Use o `sql_spid` coluna para ingressar **sys.dm_pdw_nodes_exec_sessions**.<br /><br /> **\*\* Aviso \* \***  esta coluna contém SPIDs fechados.||  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte a seção de metadados na [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) tópico.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
