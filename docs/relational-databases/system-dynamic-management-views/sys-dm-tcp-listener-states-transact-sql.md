---
title: sys.dm_tcp_listener_states (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ec759f668da3ce03d084469efad795eb55140d5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha que contém informações de estado dinâmico para cada ouvinte de TCP.  
  
> [!NOTE]
> O ouvinte de grupo de disponibilidade pode escutar na mesma porta que o ouvinte da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Neste caso, os ouvintes são listados separadamente, o mesmo que para um ouvinte do Service Broker.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**Int**|A ID interna do ouvinte. Não permite valor nulo.<br /><br /> Chave primária.|  
|**ip_address**|**nvarchar48**|O endereço IP do ouvinte que está online e está sendo escutando no momento. IPv4 ou IPv6 é permitido. Se um ouvinte possuir os dois tipos de endereços, eles serão listados separadamente. Um curinga de IPv4, exibido como "0.0.0.0". Um curinga de IPv6, exibido como “::”.<br /><br /> Não permite valor nulo.|  
|**is_ipv4**|**bit**|Tipo de endereço IP<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**Int**|O número da porta na qual o ouvinte está escutando. Não permite valor nulo.|  
|**type**|**tinyint**|Tipo de ouvinte, um dos seguintes:<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = Espelhamento do banco de dados<br /><br /> Não permite valor nulo.|  
|**type_desc**|**nvarchar(20)**|Descrição do **tipo**, um de:<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> Não permite valor nulo.|  
|**state**|**tinyint**|O estado do ouvinte do grupo de disponibilidade, um dos seguintes:<br /><br /> 1 = Online. O ouvinte está escutando e processando solicitações.<br /><br /> 2 = Reinício pendente. o ouvinte está offline, pendente de uma reinicialização.<br /><br /> Se o ouvinte do grupo de disponibilidade estiver escutando na mesma porta que a instância do servidor, esses dois ouvintes sempre terão o mesmo estado.<br /><br /> Não permite valor nulo.<br /><br /> Observação: Os valores nesta coluna são provenientes do objeto TSD_listener. A coluna não dá suporte a um estado offline porque quando o TDS_listener estiver offline, ele não pode ser consultado para o estado.|  
|**state_desc**|**nvarchar(16)**|Descrição do **estado**, um de:<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> Não permite valor nulo.|  
|**start_time**|**datetime**|Carimbo de data/hora que indica quando o ouvinte foi iniciado. Não permite valor nulo.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Grupos de disponibilidade AlwaysOn, funções e exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
