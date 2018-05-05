---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f6ceea1c7a604b2bfd98a158b383814990644391
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações sobre todas as solicitações ativas no momento ou recentemente em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele lista uma linha por solicitar de consulta.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Chave para este modo de exibição. Id numérico exclusivo associado à solicitação.|Exclusivo entre todas as solicitações no sistema.|  
|session_id|**nvarchar(32)**|Id numérico exclusivo associado à sessão em que essa consulta foi executada. Consulte [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Status atual da solicitação.|'Em execução', 'Suspenso', 'Concluir', 'Cancelado', 'Com falha'.|  
|submit_time|**datetime**|Hora em que a solicitação foi enviada para execução.|Válido **datetime** menores ou iguais à start_time e da hora atual.|  
|start_time|**datetime**|Hora em que a execução da solicitação foi iniciada.|NULL para solicitações em fila; Caso contrário, válido **datetime** menor ou igual à hora atual.|  
|end_compile_time|**datetime**|Hora em que o mecanismo concluiu compilar a solicitação.|NULL para solicitações que não foram compilados ainda; Caso contrário, uma opção válida **datetime** menor do que start_time e menor ou igual a hora atual.|
|end_time|**datetime**|Hora em que a execução da solicitação concluído, falhou ou foi cancelada.|NULL para solicitações em fila ou ativas; Caso contrário, uma opção válida **datetime** menor ou igual à hora atual.|  
|total_elapsed_time|**Int**|Tempo decorrido na execução desde que a solicitação foi iniciada, em milissegundos.|Entre 0 e a diferença entre start_time e end_time.<br /><br /> Se total_elapsed_time excede o valor máximo para um inteiro, total_elapsed_time continuará a ser o valor máximo. Essa condição gerará o aviso "o valor máximo foi excedido."<br /><br /> O valor máximo em milissegundos é equivalente a 24.8 dias.|  
|Rótulo|**nvarchar(255)**|Cadeia de caracteres de rótulo opcional associada algumas instruções de consulta SELECT.|Qualquer cadeia de caracteres que contém 'a-z', 'A-Z','0-9', '_'.|  
|error_id|**nvarchar(36)**|Id exclusiva do erro associado à solicitação, se houver.|Consulte [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); definido como NULL se nenhum erro ocorreu.|  
|database_id|**Int**|Identificador do banco de dados usado pelo contexto explícito (por exemplo, USE DB_X).|Consulte a id de [sys. Databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Contém o texto completo da solicitação como enviado pelo usuário.|Qualquer texto de consulta ou solicitação válido. Consultas que têm mais de 4000 bytes são truncadas.|  
|resource_class|**nvarchar(20)**|A classe de recurso para esta solicitação. Consulte relacionados **concurrency_slots_used** na [sys.dm_pdw_resource_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 Para obter informações sobre o máximo de linhas mantido por esta exibição, consulte "Mínimo e máximo valores" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="security"></a>Segurança  
 sys.dm_pdw_exec_requests não filtra os resultados de consulta de acordo com as permissões específicas do banco de dados. Logons com permissão VIEW SERVER STATE podem obter resultados resultados da consulta para todos os bancos de dados  
  
> [!WARNING]  
>  Um invasor pode usar sys.dm_pdw_exec_requests para recuperar informações sobre objetos de banco de dados específico por simplesmente ter permissão VIEW SERVER STATE e por não ter uma permissão de banco de dados específico.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
