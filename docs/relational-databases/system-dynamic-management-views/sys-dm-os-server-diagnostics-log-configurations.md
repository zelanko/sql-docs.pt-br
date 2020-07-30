---
title: sys. dm_os_server_diagnostics_log_configurations | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 797cdece07651499a9b770ba59972792805828a5
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395217"
---
# <a name="sysdm_os_server_diagnostics_log_configurations"></a>sys.dm_os_server_diagnostics_log_configurations
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha com a configuração atual do log de diagnóstico do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas configurações de propriedade determinam se o log de diagnóstico está ativado ou desativado e o local, o número e o tamanho dos arquivos de log.  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|is_enabled|**bit**|Indica se o log está ativado ou desativado.<br /><br /> 1 = O log de diagnóstico está ativado<br /><br /> 0 = O log de diagnóstico está desativado|  
|max_size|**int**|Tamanho máximo em megabytes que cada log de diagnóstico pode atingir. O padrão é 100 MB.|  
|max_files|**int**|Número máximo de arquivos de log de diagnóstico que podem ser armazenados no computador antes de serem reciclados para novos logs de diagnóstico.|  
|caminho|**nvarchar(260)**|Caminho que indica o local dos logs de diagnóstico. A localização padrão é \<\MSSQL\Log> dentro da pasta de instalação da instância do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
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
|1|\<C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\Log>|10|10|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler o log de diagnóstico da instância do cluster de failover](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
