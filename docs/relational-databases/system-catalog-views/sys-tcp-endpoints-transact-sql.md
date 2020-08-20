---
description: sys.tcp_endpoints (Transact-SQL)
title: sys. tcp_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e433372f8c1c5748b7ae4cfe1b355517e8b75d77
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455136"
---
# <a name="systcp_endpoints-transact-sql"></a>sys.tcp_endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada ponto de extremidade TCP presente no sistema. Os pontos de extremidade descritos por **Sys. tcp_endpoints** fornecem um objeto para conceder e revogar o privilégio de conexão. As informações que são exibidas em relação a portas e endereços IP não são usadas para configurar os protocolos e podem não corresponder à configuração de protocolo atual. Para exibir e configurar protocolos, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**< colunas herdadas>**||Herda colunas de [pontos sys.](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)end.|  
|**port**|INT|O número da porta que o ponto de extremidade está escutando. Não permite valor nulo.|  
|**is_dynamic_port**|bit|1 = O número da porta foi atribuído dinamicamente.<br /><br /> Não permite valor nulo.|  
|**ip_address**|**nvarchar (45)**|Endereço de IP do ouvinte conforme especificado pela cláusula LISTENER_IP. Permite valor nulo.|  
  
## <a name="remarks"></a>Comentários  
 Execute a consulta a seguir para colher informações sobre os pontos de extremidade e conexões. Pontos de extremidade sem conexões atuais ou sem conexões TCP aparecerão com valores NULL. Adicione a **WHERE** cláusula WHERE `WHERE des.session_id = @@SPID` para retornar informações sobre a conexão atual.  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo de pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
