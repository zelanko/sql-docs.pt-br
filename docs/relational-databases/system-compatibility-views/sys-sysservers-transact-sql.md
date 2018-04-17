---
title: sys.sysservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cd9657b883ff008f8ef174f6be82de7c2118c2f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada servidor que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode acessar como fonte de dados OLE DB.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|Identificação (somente para uso local) do servidor remoto.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|O nome do servidor.|  
|**srvproduct**|**sysname**|Nome de produto do servidor remoto.|  
|**providername**|**nvarchar(128)**|Nome do provedor OLE DB para acesso a este servidor.|  
|**datasource**|**nvarchar(4000)**|Valor de fonte de dados OLE DB.|  
|**local**|**nvarchar(4000)**|Valor local de OLE DB.|  
|**providerstring**|**nvarchar(4000)**|Valor de cadeia de caracteres do provedor OLE DB.|  
|**schemadate**|**datetime**|Data da última atualização da linha.|  
|**topologyx**|**Int**|Não usado.|  
|**topologyy**|**Int**|Não usado.|  
|**catalog**|**sysname**|Catálogo que é usado quando uma conexão é feita a um provedor OLE DB.|  
|**srvcollation**|**sysname**|O agrupamento do servidor.|  
|**connecttimeout**|**Int**|Configuração de tempo limite para a conexão de servidor.|  
|**querytimeout**|**Int**|Configuração de tempo limite para a consultas no servidor.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = Servidor é um servidor remoto.<br /><br /> 0 = Servidor é um servidor vinculado.|  
|**rpc**|**bit**|1 = **sp_serveroption@rpc** definida como **true** ou **em**.<br /><br /> 0 = **sp_serveroption@rpc** definida como **false** ou **off**.|  
|**pub**|**bit**|1 = **sp_serveroption@pub** definida como **true** ou **em**.<br /><br /> 0 = **sp_serveroption@pub** definida como **false** ou **off**.|  
|**sub**|**bit**|1 = **sp_serveroption@sub** definida como **true** ou **em**.<br /><br /> 0 = **sp_serveroption@sub** definida como **false** ou **off**.|  
|**dist**|**bit**|1 = **sp_serveroption@dist** definida como **true** ou **em**.<br /><br /> 0 = **sp_serveroption@dist** definida como **false** ou **off**.|  
|**dpub**|**bit**|1 = **sp_serveroption@dpub** definida como **true** ou **em**.<br /><br /> 0 = **sp_serveroption@dpub** definida como **false** ou **off**.|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc out** definida como **true** ou **em**.<br /><br /> 0 =  **sp_serveroption@rpc out** definida como **false** ou **off**.|  
|**dataaccess**|**bit**|1 =  **sp_serveroption@data acesso** definida como **true** ou **em**.<br /><br /> 0 =  **sp_serveroption@data acesso** definida como **false** ou **off**.|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation compatível** definida como **true** ou **em**.<br /><br /> 0 =  **sp_serveroption@collation compatível** definida como **false** ou **off**.|  
|**system**|**bit**|1 = **sp_serveroption@system** definida como **true** ou **em**.<br /><br /> 0 = **sp_serveroption@system** definida como **false** ou **off**.|  
|**useremotecollation**|**bit**|1 =  **sp_serveroption@remote agrupamento** definida como **true** ou **em**.<br /><br /> 0 =  **sp_serveroption@remote agrupamento** definida como **false** ou **off**.|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy validação de esquema** definida como **true** ou **em**.<br /><br /> 0 =  **sp_serveroption@lazy validação de esquema** definida como **false** ou **off**.|  
|**Agrupamento**|**sysname**|Agrupamento do servidor conforme definido pela  **sp_serveroption@collation nome**.|  
|**nonsqlsub**|bit|0 = server é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = server não é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
