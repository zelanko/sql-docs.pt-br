---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 972a5a5f1be1f06f22a520281b1eaa0e1e3a03b1
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973405"
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as solicitações ativas no momento ou recentemente em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele lista uma linha por solicitação/consulta.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|A chave para este modo de exibição. Id numérico exclusivo associado com a solicitação.|Exclusivo entre todas as solicitações no sistema.|  
|session_id|**nvarchar(32)**|Id numérico exclusivo associado à sessão em que essa consulta foi executada. Ver [DM pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Status atual da solicitação.|'Running', 'Suspended', 'Completed', 'Cancelled', 'Failed'.|  
|submit_time|**datetime**|Hora em que a solicitação foi enviada para execução.|Válido **datetime** menor ou igual à hora atual e start_time.|  
|start_time|**datetime**|Hora em que a execução da solicitação foi iniciada.|NULL para solicitações em fila; Caso contrário, válido **datetime** menor ou igual à hora atual.|  
|end_compile_time|**datetime**|Hora em que o mecanismo concluiu a solicitação de compilação.|NULL para solicitações que não foram compilados ainda; Caso contrário, válido **datetime** menor do que start_time e menor ou igual à hora atual.|
|end_time|**datetime**|Hora em que a execução da solicitação concluído, falhou ou foi cancelada.|NULL para solicitações em fila ou do Active Directory; Caso contrário, válido **datetime** menor ou igual à hora atual.|  
|total_elapsed_time|**int**|Tempo decorrido na execução desde que a solicitação foi iniciada, em milissegundos.|Entre 0 e a diferença entre start_time e end_time.</br></br> Se total_elapsed_time exceder o valor máximo para um número inteiro, o total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."</br></br> O valor máximo em milissegundos é equivalente a 24,8 dias.|  
|Rótulo|**nvarchar(255)**|Cadeia de caracteres de rótulo opcional associada com algumas instruções de consulta SELECT.|Qualquer cadeia de caracteres que contém 'a-z', 'A-Z','0-9', '_'.|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado à solicitação, se houver.|Ver [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); definido como NULL se nenhum erro tiver ocorrido.|  
|database_id|**int**|Identificador do banco de dados usado pelo contexto explícito (por exemplo, USE DB_X).|Consulte a id na [sys. Databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Contém o texto completo da solicitação enviado pelo usuário.|Qualquer texto de consulta ou de solicitação válido. Consultas que têm mais de 4000 bytes são truncadas.|  
|resource_class|**nvarchar(20)**|A classe de recurso para esta solicitação. Consulte relacionados **concurrency_slots_used** na [sys.dm_pdw_resource_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).|Classes de recursos estáticos</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>SmallRC de Classes de recursos dinâmicos</br>MediumRC</br>LargeRC</br>XLargeRC|
|importância (versão prévia para o SQL DW Gen2)|**nvarchar(32)**|A importância de definição da solicitação foi enviada com. Solicitações com um menor será de importância permanecem na fila em estado suspenso, se as solicitações de importância mais alta são enviadas.  Solicitações com importância mais alta serão executadas antes de solicitações de prioridade inferiores que foram enviadas anteriormente. |NULL</br>low</br>below_normal</br>normal</br>above_normal</br>high|
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte "Mínimo e máximo valores" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="permissions"></a>Permissões

 Requer a permissão VIEW SERVER STAT.  
  
## <a name="security"></a>Segurança

 DM pdw_exec_requests não filtra os resultados de consulta de acordo com as permissões específicas do banco de dados. Logons com permissão VIEW SERVER STATE podem obter resultados resultados da consulta para todos os bancos de dados  
  
>[!WARNING]  
>Um invasor pode usar DM pdw_exec_requests para recuperar informações sobre objetos de banco de dados específico, basta ter a permissão VIEW SERVER STATE e por não ter uma permissão de banco de dados específico.  
  
## <a name="see-also"></a>Consulte também

 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) </br>[Importância de carga de trabalho do SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-importance)
