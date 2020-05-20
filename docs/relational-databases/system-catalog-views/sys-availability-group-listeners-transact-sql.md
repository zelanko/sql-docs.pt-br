---
title: sys. availability_group_listeners (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listeners_TSQL
- sys.availability_group_listeners
- sys.availability_group_listeners_TSQL
- availability_group_listeners
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_group_listeners catalog view
- Availability Groups [SQL Server], listeners
ms.assetid: b5e7d1fb-3ffb-4767-8135-604c575016b1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e4ae93cfcb4df935b3b006413ab8d8c884090ff
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829104"
---
# <a name="sysavailability_group_listeners-transact-sql"></a>sys.availability_group_listeners (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Para cada grupo de disponibilidade Always On, retorna zero linhas indicando que nenhum nome de rede está associado ao grupo de disponibilidade ou retorna uma linha para cada configuração de ouvinte de grupo de disponibilidade no cluster do WSFC (Windows Server Failover Clustering). Essa exibição exibe a configuração em tempo real coletada do cluster.  
  
> [!NOTE]  
>  Essa exibição do catálogo não descreve detalhes de uma configuração de IP, que foi definida no cluster do WSFC.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|ID do grupo de disponibilidade (**group_id**) de [Sys. availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md).|  
|**listener_id**|**nvarchar (36)**|GUID da ID do recurso do cluster.|  
|**dns_name**|**nvarchar (63)**|Nome de rede configurado (nome do host) do ouvinte do grupo de disponibilidade.|  
|**Porto**|**int**|O número da porta TCP configurada para o ouvinte do grupo de disponibilidade.<br /><br /> NULL = O ouvinte foi configurado fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e seu número de porta não foi adicionado ao grupo de disponibilidade. Para adicionar a porta, pleaseuse a opção modificar OUVInte da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**is_conformant**|**bit**|Se esta configuração de IP é compatível, pode ser:<br /><br /> 1 = O ouvinte é compatível. Somente as relações "ou" existem entre seus endereços IP (Internet Protocol). *Compatível* abrange todas as configurações de IP que foram criadas pela instrução [Criar grupo de disponibilidade](../../t-sql/statements/create-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] . Além disso, se uma configuração de IP que foi criada fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por exemplo, usando o Gerenciador de Cluster de Failover do WSFC, mas puder ser modificada pela instrução tsql ALTER AVAILABILITY GROUP, a configuração de IP será qualificada como compatível.<br /><br /> 0 = O ouvinte não é compatível. Normalmente, indica um endereço IP que não pôde ser configurado usando comandos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em vez disso, foi definido diretamente no cluster do WSFC.|  
|**ip_configuration_string_from_cluster**|**nvarchar(max)**|Cadeias de caracteres da configuração de IP do cluster, se houver, para esse ouvinte. NULL = O ouvinte não tem nenhum endereço IP virtual. Por exemplo:<br /><br /> Endereço IPv4: `65.55.39.10`.<br /><br /> Endereço IPv6: `2001::4898:23:1002:20f:1fff:feff:b3a3`|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Always On funções e exibições de gerenciamento dinâmico de grupos de disponibilidade &#40;&#41;de Transact-SQL](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On exibições de catálogo de grupos de disponibilidade &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
