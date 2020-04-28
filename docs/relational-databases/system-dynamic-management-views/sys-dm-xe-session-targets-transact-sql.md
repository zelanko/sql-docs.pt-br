---
title: sys. dm_xe_session_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_targets
- dm_xe_session_targets_TSQL
- dm_xe_session_targets
- sys.dm_xe_session_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_targets dynamic management view
- extended events [SQL Server], views
ms.assetid: 76fbc3e1-ad88-4a47-8bf1-471c3bee5ad8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 977a5e0428f59a45a823dd82e30b3f4c63520c0c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68090210"
---
# <a name="sysdm_xe_session_targets-transact-sql"></a>sys.dm_xe_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os destinos da sessão.  
  
  |Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|O endereço da memória da sessão de evento. Tem uma relação muitos para um com sys.dm_xe_sessions.address. Não permite valor nulo.|  
|target_name|**nvarchar(60)**|O nome do destino em uma sessão. Não permite valor nulo.|  
|target_package_guid|**uniqueidentifier**|O GUID do pacote que contém o destino. Não permite valor nulo.|  
|execution_count|**bigint**|O número de horas que o destino foi executado para a sessão. Não permite valor nulo.|  
|execution_duration_ms|**bigint**|O total de tempo, em milissegundos, em que o destino esteve em execução. Não permite valor nulo.|  
|target_data|**nvarchar(max)**|Os dados que o destino mantém, como informações de agregação de evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_xe_session_targets.event_session_address|sys.dm_xe_sessions.address|Muitos para um|  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Corrigido o tipo de dados da coluna target_data.|  
|Corrigida a descrição da coluna target_data para indicar que o valor é anulável.|  
|Corrigida a tabela "Cardinalidades de relações".|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

