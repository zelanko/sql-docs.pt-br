---
title: sys.dm_os_server_diagnostics_log_configurations | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations_TSQL
- dm_os_server_diagnostics_log_configurations
- dm_os_server_diagnostics_log_configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations
ms.assetid: c09ea433-d283-4f83-af69-d458aad59217
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f73f0e2c1fc3223801bdd95d96d5bba8c19351f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosserverdiagnosticslogconfigurations"></a>sys.dm_os_server_diagnostics_log_configurations
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Retorna uma linha com a configuração atual do log de diagnóstico do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas configurações de propriedade determinam se o log de diagnóstico está ativado ou desativado e o local, o número e o tamanho dos arquivos de log.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|is_enabled|**bit**|Indica se o log está ativado ou desativado.<br /><br /> 1 = O log de diagnóstico está ativado<br /><br /> 0 = O log de diagnóstico está desativado|  
|max_size|**Int**|Tamanho máximo em megabytes que cada log de diagnóstico pode atingir. O padrão é 100 MB.|  
|max_files|**Int**|Número máximo de arquivos de log de diagnóstico que podem ser armazenados no computador antes de serem reciclados para novos logs de diagnóstico.|  
|path|**nvarchar(260)**|Caminho que indica o local dos logs de diagnóstico. O local padrão é \<\mssql\log. > dentro da pasta de instalação da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de cluster de failover.|  
  
## <a name="permissions"></a>Permissões  
 Exige permissões de VIEW SERVER STATE na instância do cluster de failover do SQL Server.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa sys.dm_os_server_diagnostics_log_configurations para retornar as configurações de propriedades dos logs de diagnóstico de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT <list of columns>  
FROM sys.dm_os_server_diagnostics_log_configurations;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|IS_ENABLED|PATH|MAX_SIZE|MAX_FILES|  
|-----------------|----------|---------------|----------------|  
|1|\<C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\Log >|10|10|  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e ler o log de diagnóstico da instância do cluster de failover](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
