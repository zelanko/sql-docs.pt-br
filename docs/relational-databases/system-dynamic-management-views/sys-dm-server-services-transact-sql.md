---
title: sys.dm_server_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8879e4d23c4e74aaa39649b03e59d5303f42e658
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmserverservices-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os serviços do SQL Server, Texto Completo e do SQL Server Agent na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use essa exibição de gerenciamento dinâmico para relatar informações de status sobre esses serviços.  
  
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Nome da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], texto completo ou o serviço SQL Server Agent. Não pode ser nulo.|  
|startup_type|**Int**|Indica o modo inicial do serviço. Estes são os valores possíveis e suas descrições correspondentes.<br /><br /> 0: outros<br />1: outros<br />2: automático<br />3: manual<br />4: desabilitado<br /><br /> Permite valor nulo.|  
|startup_desc|**nvarchar(256)**|Descreve o modo inicial do serviço. Estes são os valores possíveis e suas descrições correspondentes.<br /><br /> Outros: Outros (iniciar reinicialização)<br />Outros: Outros (Iniciar sistema)<br />Automática: Inicialização automática<br />Manual: Início de demanda<br />Desabilitado: desabilitado<br /><br /> Não pode ser nulo.|  
|status|**Int**|Indica o status atual do serviço. Estes são os valores possíveis e suas descrições correspondentes.<br /><br /> 1: interrompido<br />2: outros (início pendente)<br />3: outros (parada pendente)<br />4: em execução<br />5: outros (continuação pendente)<br />6: outros (pausa pendente)<br />7: pausado<br /><br /> Permite valor nulo.|  
|status_desc|**nvarchar(256)**|Descreve o status atual do serviço. Estes são os valores possíveis e suas descrições correspondentes.<br /><br /> Interrompido: O serviço é interrompido.<br />Outros (início de operação pendente): O serviço está iniciando.<br />Outros (parada de operação pendente): O serviço está no processo de parada.<br />Está em execução: O serviço está em execução.<br />Outros (continuar operações pendente): O serviço está em um estado pendente.<br />Outros (pausa pendente): O serviço está no processo de pausa.<br />Em pausa: O serviço está em pausa.<br /><br /> Não pode ser nulo.|  
|process_id|**Int**|A ID do processo do serviço. Não pode ser nulo.|  
|last_startup_time|**datetimeoffset(7)**|A data e a hora em que o serviço foi iniciado pela última vez. Permite valor nulo.|  
|service_account|**nvarchar(256)**|A conta autorizada para controlar o serviço. Essa conta pode iniciar ou parar o serviço, ou modificar as propriedades do serviço. Não pode ser nulo.|  
|filename|**nvarchar(256)**|O caminho e o nome do arquivo do serviço executável. Não pode ser nulo.|  
|is_clustered|**nvarchar(1)**|Indica se o serviço é instalado como um recurso de um servidor clusterizado. Não pode ser nulo.|  
|cluster_nodename|**nvarchar(256)**|O nome do nó de cluster no qual o serviço está instalado. Permite valor nulo.|
|instant_file_initialization_enabled|**nvarchar(1)**|Especifica se a inicialização instantânea de arquivo está habilitada para o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] service.<br /><br />Y = inicialização instantânea de arquivo está habilitada para o serviço.<br /><br />N = inicialização instantânea de arquivo está desabilitada para o serviço.<br /><br /> Permite valor nulo.<br /><br /> **Observação:** não se aplica a outros serviços, como o SQL Server Agent.<br /><br /> **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 por meio de por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|  

## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
