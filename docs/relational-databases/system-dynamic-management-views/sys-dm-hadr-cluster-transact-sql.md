---
description: sys.dm_hadr_cluster (Transact-SQL)
title: sys. dm_hadr_cluster (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8bc19f3e73c00c2148cba2fb0381d73a36d6eb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89532920"
---
# <a name="sysdm_hadr_cluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Se o nó WSFC (Windows Server failover clustering) que hospeda uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o tiver quorum do WSFC, **Sys. dm_hadr_cluster** retornará uma linha que expõe o nome do cluster e as informações sobre o quorum. Se o nó WSFC não tiver quorum, nenhuma linha será retornada.  
 > [!TIP]
 > A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , essa exibição de gerenciamento dinâmico dá suporte a Always on instâncias de cluster de failover, além de Always on grupos de disponibilidade.

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|Nome do cluster do WSFC que hospeda as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão habilitadas para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**quorum_type**|**tinyint**|Tipo de quorum usado por este cluster do WSFC, um dos seguintes:<br /><br /> 0 = Maioria de nós. Esta configuração de quorum pode sustentar falhas da metade dos nós (arredondamento) menos um. Por exemplo, em um cluster de sete nós, esta configuração de quorum pode sustentar três falhas de nó.<br /><br /> 1 = Maioria de nós e discos. Se a testemunha de disco permanecer online, essa configuração de quorum poderá sustentar falhas da metade dos nós (arredondamento). Por exemplo, um cluster de seis nós no qual a testemunha de disco está online pode sustentar três falhas de nó. Se a testemunha de disco ficar offline ou falhar, essa configuração de quorum poderá sustentar falhas da metade dos nós (arredondamento). Por exemplo, um cluster de seis nós com uma testemunha de disco com falha pode sustentar duas (3-1=2) falhas de nó.<br /><br /> 2 = Maioria de compartilhamentos de nós e arquivos. Essa configuração de quorum funciona de maneira semelhante à Maioria de Nós e Discos, mas usa uma testemunha de compartilhamento de arquivo em vez de uma testemunha de disco.<br /><br /> 3 = Nenhuma maioria: somente disco. Se o disco de quorum estiver online, essa configuração de quorum poderá sustentar falhas de todos os nós, exceto um.<br /><br /> 4 = quorum desconhecido. Quorum desconhecido para o cluster.<br /><br /> 5 = testemunha em nuvem. O cluster utiliza Microsoft Azure para arbitragem de quorum. Se a testemunha de nuvem estiver disponível, o cluster poderá sustentar a falha da metade dos nós (arredondando para cima).|  
|**quorum_type_desc**|**varchar(50)**|Descrição de **quorum_type**, uma das:<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY <br /><br /> UNKNOWN_QUORUM <br /><br /> CLOUD_WITNESS|  
|**quorum_state**|**tinyint**|Estado do quorum do WSFC, um dos seguintes:<br /><br /> 0 = Estado de quorum desconhecido<br /><br /> 1 = Quorum normal<br /><br /> 2 = Quorum forçado|  
|**quorum_state_desc**|**varchar(50)**|Descrição de **quorum_state**, uma das:<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Always On funções e exibições de gerenciamento dinâmico de grupos de disponibilidade &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
