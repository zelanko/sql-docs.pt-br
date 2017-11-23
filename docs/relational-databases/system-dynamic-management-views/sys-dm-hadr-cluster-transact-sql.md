---
title: sys.DM hadr_cluster (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea7fef3018ef9e7c88100c1a0c3a7b444bfaeac7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Se o nó de cluster de Failover do Windows Server (WSFC) que hospeda uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tiver quorum de WSFC, **sys.DM hadr_cluster** retorna uma linha que expõe o nome do cluster e informações sobre o quorum. Se o nó WSFC não tem quorum, nenhuma linha será retornada.  
 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], essa exibição de gerenciamento dinâmico oferece suporte a Failover Cluster instâncias AlwaysOn além dos grupos de disponibilidade AlwaysOn.

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar (128)**|Nome do cluster do WSFC que hospeda as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão habilitadas para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**quorum_type**|**tinyint**|Tipo de quorum usado por este cluster do WSFC, um dos seguintes:<br /><br /> 0 = Maioria de nós. Esta configuração de quorum pode sustentar falhas da metade dos nós (arredondamento) menos um. Por exemplo, em um cluster de sete nós, esta configuração de quorum pode sustentar três falhas de nó.<br /><br /> 1 = Maioria de nós e discos. Se a testemunha de disco permanecer online, essa configuração de quorum poderá sustentar falhas da metade dos nós (arredondamento). Por exemplo, um cluster de seis nós no qual a testemunha de disco está online pode sustentar três falhas de nó. Se a testemunha de disco ficar offline ou falhar, essa configuração de quorum poderá sustentar falhas da metade dos nós (arredondamento). Por exemplo, um cluster de seis nós com uma testemunha de disco com falha pode sustentar duas (3-1=2) falhas de nó.<br /><br /> 2 = Maioria de compartilhamentos de nós e arquivos. Essa configuração de quorum funciona de maneira semelhante à Maioria de Nós e Discos, mas usa uma testemunha de compartilhamento de arquivo em vez de uma testemunha de disco.<br /><br /> 3 = Nenhuma maioria: somente disco. Se o disco de quorum estiver online, essa configuração de quorum poderá sustentar falhas de todos os nós, exceto um.|  
|**quorum_type_desc**|**varchar(50)**|Descrição do **quorum_type**, um de:<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY|  
|**quorum_state**|**tinyint**|Estado do quorum do WSFC, um dos seguintes:<br /><br /> 0 = Estado de quorum desconhecido<br /><br /> 1 = Quorum normal<br /><br /> 2 = Quorum forçado|  
|**quorum_state_desc**|**varchar(50)**|Descrição do **quorum_state**, um de:<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
