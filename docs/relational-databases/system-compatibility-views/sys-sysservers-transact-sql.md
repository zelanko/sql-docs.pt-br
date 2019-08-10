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
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/10/2019
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
|**providername**|**nvarchar(128)**|Nome do provedor OLE DB para acesso a este servidor.|  
|**datasource**|**nvarchar(4000)**|Valor de fonte de dados OLE DB.|  
|**local**|**nvarchar(4000)**|Valor local de OLE DB.|  
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
|**rpc**|**bit**|1 = **sp_serveroption\@RPC** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@RPC** definido como **false** ou **off**.|  
|**pub**|**bit**|1 = **sp_serveroption\@pub** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@pub** definido como **false** ou **off**.|  
|**sub**|**bit**|1 = **sp_serveroption\@sub** definida como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@sub** definida como **false** ou **off**.|  
|**dist**|**bit**|1 = **sp_serveroption\@dist** definida como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@dist** definido como **false** ou **off**.|  
|**dpub**|**bit**|1 = **sp_serveroption\@dpub** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@dpub** definido como **false** ou **off**.|  
|**rpcout**|**bit**|1 = **sp_serveroption\@RPC out** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@RPC out** definido como **false** ou **off**.|  
|**dataaccess**|**bit**|1 = **sp_serveroption\@Data Access** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@Data Access** definido como **false** ou **off**.|  
|**collationcompatible**|**bit**|1 = **conjunto\@compatível com agrupamento sp_serveroption** definido como **true** ou **on**.<br /><br /> 0 = **conjunto\@compatível com agrupamento sp_serveroption** definido como **false** ou **off**.|  
|**system**|**bit**|1 = **sistema\@sp_serveroption** definido como **true** ou **on**.<br /><br /> 0 = **sistema\@sp_serveroption** definido como **false** ou **off**.|  
|**useremotecollation**|**bit**|1 = **agrupamento\@remoto sp_serveroption** definido como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@agrupamento remoto** definido como **false** ou **off**.|  
|**lazyschemavalidation**|**bit**|1 = **validação\@de esquema lenta sp_serveroption** definida como **true** ou **on**.<br /><br /> 0 = **sp_serveroption\@validação de esquema lenta** definida como **false** ou **off**.|  
|**Agrupamento**|**sysname**|Agrupamento de servidor conforme definido **pelo\@nome de agrupamento sp_serveroption**.|  
|**nonsqlsub**|bit|0 = server é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = server não é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para &#40;exibições do sistema TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
