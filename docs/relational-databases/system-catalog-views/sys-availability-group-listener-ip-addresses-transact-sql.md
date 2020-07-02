---
title: sys. availability_group_listener_ip_addresses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listener_ip_addresses
- sys.availability_group_listener_ip_addresses
- availability_group_listener_ip_addresses_TSQL
- sys.availability_group_listener_ip_addresses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.availability_group_listener_ip_addresses catalog view
ms.assetid: e515fa6b-1354-4110-9b70-ab2e6164c992
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e4c3dce812a06b4b42b45d0baa3874f5cfa2ba3b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733544"
---
# <a name="sysavailability_group_listener_ip_addresses-transact-sql"></a>sys.availability_group_listener_ip_addresses (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada endereço IP associado a qualquer ouvinte de grupo de disponibilidade Always On no cluster do WSFC (Windows Server Failover Clustering).  
  
 Chave primária: **listener_id**  +  **ip_address**  +  **ip_sub_mask**  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**listener_id**|**nvarchar (36)**|GUID do recurso do cluster do WSFC (Windows Server Failover Clustering).|  
|**ip_address**|**nvarchar (48)**|Endereço IP virtual configurado do ouvinte do grupo de disponibilidade. Retorna um único endereço IPv4 ou IPv6.|  
|**ip_subnet_mask**|**nvarchar (15)**|Máscara de sub-rede IP configurada para o endereço IPv4, se houver, isso é configurado para o ouvinte do grupo de disponibilidade.<br /><br /> NULL = Sub-rede IPv6|  
|**is_dhcp**|**bit**|Se o endereço IP está configurado pelo DHCP, um dos seguintes:<br /><br /> 0 = Endereço IP não configurado pelo DHCP.<br /><br /> 1 = Endereço IP configurado pelo DHCP.|  
|**network_subnet_ip**|**nvarchar (48)**|Endereço IP de sub-rede de rede que especifica a sub-rede à qual o endereço IP pertence.|  
|**network_subnet_prefix_length**|**int**|Comprimento do prefixo de sub-rede de rede da sub-rede à qual o endereço IP pertence.|  
|**network_subnet_ipv4_mask**|**nvarchar (45)**|Máscara de sub-rede de rede da sub-rede à qual o endereço IP pertence. **network_subnet_ipv4_mask** para especificar o <DHCP network_subnet_option opções de> em uma cláusula WITH DHCP da instrução [Create Availability Group](../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> NULL = Sub-rede IPv6|  
|**state**|**tinyint**|Estado ONLINE/OFFLINE do recurso IP no cluster do WSFC, um dos seguintes:<br /><br /> 1 = Online. O recurso IP está online.<br /><br /> 0 = Offline. O recurso IP está offline.<br /><br /> 2 = Online pendente. O recurso IP está offline, mas está sendo colocado online.<br /><br /> 3 - Com falha. O recurso IP estava sendo colocado online, mas houve uma falha.|  
|**state_desc**|**nvarchar(60)**|Descrição do **estado**, um de:<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> ONLINE_PENDING<br /><br /> FAILED|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
