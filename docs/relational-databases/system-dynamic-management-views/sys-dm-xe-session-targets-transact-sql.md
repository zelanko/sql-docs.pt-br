---
title: xe_session_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 330e5669b9b2e80f7995b12e4bca090e8d0604e9
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmxesessiontargets-transact-sql"></a>sys.dm_xe_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os destinos de sessão.  
  
  |Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|O endereço da memória da sessão de evento. Tem uma relação muitos para um com sys.dm_xe_sessions.address. Não permite valor nulo.|  
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
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

