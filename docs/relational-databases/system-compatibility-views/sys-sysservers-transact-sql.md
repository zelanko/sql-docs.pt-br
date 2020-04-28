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
ms.openlocfilehash: 333be9cb6c86c1db3801ac50159610c6d19d1611
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68941108"
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
|**ProviderName**|**nvarchar(128)**|Nome do provedor OLE DB para acesso a este servidor.|  
|**fonte**|**nvarchar(4000)**|Valor de fonte de dados OLE DB.|  
|**local**|**nvarchar(4000)**|Valor local de OLE DB.|  
|**providerstring**|**nvarchar(4000)**|Valor de cadeia de caracteres do provedor OLE DB.|  
|**schemadate**|**datetime**|Data da última atualização da linha.|  
|**topologyx**|**int**|Não usado.|  
|**topologyy**|**int**|Não usado.|  
|**Catalog**|**sysname**|Catálogo que é usado quando uma conexão é feita a um provedor OLE DB.|  
|**srvcollation**|**sysname**|A ordenação do servidor.|  
|**connecttimeout**|**int**|Configuração de tempo limite para a conexão de servidor.|  
|**QueryTimeout**|**int**|Configuração de tempo limite para a consultas no servidor.|  
|**srvnetname**|**char(30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = Servidor é um servidor remoto.<br /><br /> 0 = Servidor é um servidor vinculado.|  
|**rpc**|**bit**|1 = **sp_serveroption\@RPC** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@RPC** definido como **false** ou **off**.|  
|**pub**|**bit**|1 = **sp_serveroption\@pub** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@pub** definido como **false** ou **off**.|  
|**projeto**|**bit**|1 = **sp_serveroption\@sub** definida como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@sub** definida como **false** ou **off**.|  
|**dist**|**bit**|1 = **sp_serveroption\@dist** definida como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@dist** definida como **false** ou **off**.|  
|**dpub**|**bit**|1 = **sp_serveroption\@dpub** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@dpub** definido como **false** ou **off**.|  
|**rpcout**|**bit**|1 = **sp_serveroption\@RPC out** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@RPC out** definido como **false** ou **off**.|  
|**dataaccess**|**bit**|1 = **sp_serveroption\@acesso a dados** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@acesso a dados** definido como **falso** ou **desativado**.|  
|**collationcompatible**|**bit**|1 = **sp_serveroption\@compatível com agrupamento** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@compatível com agrupamento** definido como **false** ou **off**.|  
|**sistema**|**bit**|1 = **sistema\@sp_serveroption** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@sistema** definido como **false** ou **off**.|  
|**useremotecollation**|**bit**|1 = **sp_serveroption\@agrupamento remoto** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@agrupamento remoto** definido como **falso** ou **desativado**.|  
|**lazyschemavalidation**|**bit**|1 = **sp_serveroption\@validação de esquema lenta** definida como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@validação de esquema lenta** definida como **false** ou **off**.|  
|**Agrupamento**|**sysname**|Agrupamento de servidor conforme definido **por\@sp_serveroption nome do agrupamento**.|  
|**nonsqlsub**|bit|0 = server é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = server não é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
