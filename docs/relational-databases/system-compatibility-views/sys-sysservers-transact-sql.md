---
title: sys.sysservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 03875d828940a2baa5d9f30f7beb58adb77abf07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018110"
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada servidor que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode acessar como fonte de dados OLE DB.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|Identificação (somente para uso local) do servidor remoto.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|O nome do servidor.|  
|**srvproduct**|**sysname**|Nome de produto do servidor remoto.|  
|**providername**|**nvarchar(128)**|Nome do provedor OLE DB para acesso a este servidor.|  
|**datasource**|**nvarchar(4000)**|Valor de fonte de dados OLE DB.|  
|**Local**|**nvarchar(4000)**|Valor local de OLE DB.|  
|**providerstring**|**nvarchar(4000)**|Valor de cadeia de caracteres do provedor OLE DB.|  
|**schemadate**|**datetime**|Data da última atualização da linha.|  
|**topologyx**|**int**|Não usado.|  
|**topologyy**|**int**|Não usado.|  
|**catalog**|**sysname**|Catálogo que é usado quando uma conexão é feita a um provedor OLE DB.|  
|**srvcollation**|**sysname**|A ordenação do servidor.|  
|**connecttimeout**|**int**|Configuração de tempo limite para a conexão de servidor.|  
|**querytimeout**|**int**|Configuração de tempo limite para a consultas no servidor.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = Servidor é um servidor remoto.<br /><br /> 0 = Servidor é um servidor vinculado.|  
|**rpc**|**bit**|1 = **sp_serveroption@rpc** definido como **verdadeira** ou **em**.<br /><br /> 0 = **sp_serveroption@rpc** definido como **falso** ou **off**.|  
|**pub**|**bit**|1 = **sp_serveroption@pub** definido como **verdadeira** ou **em**.<br /><br /> 0 = **sp_serveroption@pub** definido como **falso** ou **off**.|  
|**sub**|**bit**|1 = **sp_serveroption@sub** definido como **verdadeira** ou **em**.<br /><br /> 0 = **sp_serveroption@sub** definido como **falso** ou **off**.|  
|**dist**|**bit**|1 = **sp_serveroption@dist** definido como **verdadeira** ou **em**.<br /><br /> 0 = **sp_serveroption@dist** definido como **falso** ou **off**.|  
|**dpub**|**bit**|1 = **sp_serveroption@dpub** definido como **verdadeira** ou **em**.<br /><br /> 0 = **sp_serveroption@dpub** definido como **falso** ou **off**.|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc out** definido como **verdadeira** ou **em**.<br /><br /> 0 =  **sp_serveroption@rpc out** definido como **falso** ou **off**.|  
|**dataaccess**|**bit**|1 =  **sp_serveroption@data acesso** definido como **verdadeira** ou **em**.<br /><br /> 0 =  **sp_serveroption@data acesso** definido como **falso** ou **off**.|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation compatível** definido como **verdadeira** ou **em**.<br /><br /> 0 =  **sp_serveroption@collation compatível** definido como **falso** ou **off**.|  
|**system**|**bit**|1 = **sp_serveroption@system** definido como **verdadeira** ou **em**.<br /><br /> 0 = **sp_serveroption@system** definido como **falso** ou **off**.|  
|**useremotecollation**|**bit**|1 =  **sp_serveroption@remote agrupamento** definido como **verdadeira** ou **em**.<br /><br /> 0 =  **sp_serveroption@remote agrupamento** definido como **falso** ou **off**.|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy validação de esquema** definido como **verdadeira** ou **em**.<br /><br /> 0 =  **sp_serveroption@lazy validação de esquema** definido como **falso** ou **off**.|  
|**Agrupamento**|**sysname**|Agrupamento do servidor conforme definido pela  **sp_serveroption@collation nome**.|  
|**nonsqlsub**|bit|0 = server é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = server não é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
