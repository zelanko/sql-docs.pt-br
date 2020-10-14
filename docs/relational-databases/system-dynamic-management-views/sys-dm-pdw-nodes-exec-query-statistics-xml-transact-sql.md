---
title: sys.dm_pdw_nodes_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
description: Exibição de gerenciamento dinâmico que retorna o plano de execução de consulta para solicitações em andamento. Use essa DMV para recuperar o Showplan XML com estatísticas transitórias.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f03d7b8c8b840c86cd462381d24ada70ded15147
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059465"
---
# <a name="dm_pdw_nodes_exec_query_statistics_xml-transact-sql"></a>dm_pdw_nodes_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Retorna o plano de execução de consulta para solicitações em andamento. Use essa DMV para recuperar o Showplan XML com estatísticas transitórias.

## <a name="table-returned"></a>Tabela retornada

|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|
|node_id|**int**|ID numérica exclusiva associada ao nó.|
|session_id|**smallint**|ID da sessão. Não permite valor nulo.|
|request_id|**int**|ID da solicitação. Não permite valor nulo.|
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte. Anulável.|
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote em execução no momento. Anulável.|
|query_plan|**xml**|Contém a representação Showplan do tempo de execução do plano de execução de consulta especificado com *plan_handle* que contém estatísticas parciais. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário. Anulável.|

## <a name="remarks"></a>Comentários
Os mesmos comentários em [Sys.dm_exec_query_statistics_xml](./sys-dm-exec-query-statistics-xml-transact-sql.md?view=sql-server-ver15) se aplicam.   

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="see-also"></a>Veja também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>Próximas etapas
 Para obter mais dicas de desenvolvimento, consulte [visão geral de desenvolvimento do Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).