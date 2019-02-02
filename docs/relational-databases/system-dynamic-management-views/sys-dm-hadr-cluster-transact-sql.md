---
title: sys.dm_hadr_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58450f8e43c5f1f736fb4388008f7af3325e430d
ms.sourcegitcommit: 7c052fc969d0f2c99ad574f99076dc1200d118c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570729"
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Se o nó do Windows Server Failover Clustering (WSFC) que hospeda uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tiver quorum de WSFC **DM hadr_cluster** retorna uma linha que expõe o nome do cluster e informações sobre o quorum. Se o nó do WSFC não tem quorum, nenhuma linha será retornada.  
 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], essa exibição de gerenciamento dinâmico oferece suporte a Failover de instâncias de Cluster AlwaysOn além dos grupos de disponibilidade AlwaysOn.

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|Nome do cluster do WSFC que hospeda as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão habilitadas para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**quorum_type**|**tinyint**|Tipo de quorum usado por este cluster do WSFC, um dos seguintes:<br /><br /> 0 = Maioria de nós. Esta configuração de quorum pode sustentar falhas da metade dos nós (arredondamento) menos um. Por exemplo, em um cluster de sete nós, esta configuração de quorum pode sustentar três falhas de nó.<br /><br /> 1 = Maioria de nós e discos. Se a testemunha de disco permanecer online, essa configuração de quorum poderá sustentar falhas da metade dos nós (arredondamento). Por exemplo, um cluster de seis nós no qual a testemunha de disco está online pode sustentar três falhas de nó. Se a testemunha de disco ficar offline ou falhar, essa configuração de quorum poderá sustentar falhas da metade dos nós (arredondamento). Por exemplo, um cluster de seis nós com uma testemunha de disco com falha pode sustentar duas (3-1=2) falhas de nó.<br /><br /> 2 = Maioria de compartilhamentos de nós e arquivos. Essa configuração de quorum funciona de maneira semelhante à Maioria de Nós e Discos, mas usa uma testemunha de compartilhamento de arquivo em vez de uma testemunha de disco.<br /><br /> 3 = nenhuma maioria: Somente Disco. Se o disco de quorum estiver online, essa configuração de quorum poderá sustentar falhas de todos os nós, exceto um.<br /><br /> 4 = Quorum desconhecido. Quorum desconhecido para o cluster.<br /><br /> 5 = testemunha de nuvem. Cluster utiliza o Microsoft Azure para arbitragem de quorum. Se a testemunha de nuvem estiver disponível, o cluster pode sustentar a falha de metade de nós (arredondamento).|  
|**quorum_type_desc**|**varchar(50)**|Descrição da **quorum_type**, um de:<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY <br /><br /> UNKNOWN_QUORUM <br /><br /> CLOUD_WITNESS|  
|**quorum_state**|**tinyint**|Estado do quorum do WSFC, um dos seguintes:<br /><br /> 0 = Estado de quorum desconhecido<br /><br /> 1 = Quorum normal<br /><br /> 2 = Quorum forçado|  
|**quorum_state_desc**|**varchar(50)**|Descrição da **quorum_state**, um de:<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico de Grupos de Disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
