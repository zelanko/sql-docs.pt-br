---
title: sys.availability_group_listener_ip_addresses (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ca29b9925de2d2c1c80e18372a8abf6e818edd15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814714"
---
# <a name="sysavailabilitygrouplisteneripaddresses-transact-sql"></a>sys.availability_group_listener_ip_addresses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada endereço IP que está associado com qualquer Always On do ouvinte do grupo disponibilidade no cluster do Windows Server Failover Clustering (WSFC).  
  
 Chave primária: **listener_id** + **endereço_IP** + **ip_sub_mask**  
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**nvarchar(36)**|GUID do recurso do cluster do WSFC (Windows Server Failover Clustering).|  
|**ip_address**|**nvarchar(48)**|Endereço IP virtual configurado do ouvinte do grupo de disponibilidade. Retorna um único endereço IPv4 ou IPv6.|  
|**ip_subnet_mask**|**nvarchar(15)**|Máscara de sub-rede IP configurada para o endereço IPv4, se houver, isso é configurado para o ouvinte do grupo de disponibilidade.<br /><br /> NULL = Sub-rede IPv6|  
|**is_dhcp**|**bit**|Se o endereço IP está configurado pelo DHCP, um dos seguintes:<br /><br /> 0 = Endereço IP não configurado pelo DHCP.<br /><br /> 1 = Endereço IP configurado pelo DHCP.|  
|**network_subnet_ip**|**nvarchar(48)**|Endereço IP de sub-rede de rede que especifica a sub-rede à qual o endereço IP pertence.|  
|**network_subnet_prefix_length**|**int**|Comprimento do prefixo de sub-rede de rede da sub-rede à qual o endereço IP pertence.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Máscara de sub-rede de rede da sub-rede à qual o endereço IP pertence. **network_subnet_ipv4_mask** para especificar as opções de DHCP < network_subnet_option > em uma cláusula WITH DHCP dos [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) ou [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.<br /><br /> NULL = Sub-rede IPv6|  
|**state**|**tinyint**|Estado ONLINE/OFFLINE do recurso IP no cluster do WSFC, um dos seguintes:<br /><br /> 1 = Online. O recurso IP está online.<br /><br /> 0 = Offline. O recurso IP está offline.<br /><br /> 2 = Online pendente. O recurso IP está offline, mas está sendo colocado online.<br /><br /> 3 - Com falha. O recurso IP estava sendo colocado online, mas houve uma falha.|  
|**state_desc**|**nvarchar(60)**|Descrição da **estado**, um de:<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> ONLINE_PENDING<br /><br /> FAILED|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
