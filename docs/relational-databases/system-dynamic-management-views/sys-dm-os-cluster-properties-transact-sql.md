---
title: sys. dm_os_cluster_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3fd3c53f5603567e0f6c2b6ee4f1712f742c1137
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900219"
---
# <a name="sysdm_os_cluster_properties-transact-sql"></a>sys.dm_os_cluster_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha com as configurações atuais para as propriedades de recurso de cluster do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas neste tópico. Nenhum dado será retornado se essa exibição for executada em uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Essas propriedades são usadas para definir os valores que afetam a detecção de falha, o tempo de resposta da falha e o log de monitoração o status de integridade da instância do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  

|Nome da coluna|Propriedade|DESCRIÇÃO|  
|-----------------|--------------|-----------------|  
|VerboseLogging|BIGINT|O nível de log para o cluster de failover do SQL Server. O log detalhado pode ser ativado para fornecer detalhes adicionais nos logs de erros para solução de problemas. Um dos seguintes valores:<br /><br /> 0 – O log está desativado (padrão)<br /><br /> 1 – Apenas erros<br /><br /> 2 – Erros e avisos<br /><br /> Para obter mais informações, consulte [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).|  
|SqlDumperDumpFlags|BIGINT|Sinalizadores de despejo do SQLDumper determinam o tipo de arquivos de despejo gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A configuração padrão é 0.|  
|SqlDumperDumpPath|nvarchar(260)|O local onde o utilitário SQLDumper gera os arquivos de despejo.|  
|SqlDumperDumpTimeOut|BIGINT|O valor de tempo limite em milissegundos para o utilitário SQLDumper gerar um despejo no caso de uma falha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O valor padrão é 0.|  
|FailureConditionLevel|BIGINT|Define as condições sob as quais o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve apresentar uma falha ou reiniciar. O valor padrão é 3. Para obter uma explicação detalhada ou alterar as configurações de propriedade, consulte [definir configurações de propriedade FailureConditionLevel](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).|  
|HealthCheckTimeout|BIGINT|O valor do tempo limite de quanto tempo a DLL de recursos do Mecanismo de Banco de Dados do SQL Server deve aguardar por informações de integridade do servidor antes de considerar a instância do SQL Server como sem resposta. O valor de tempo limite é expresso em milissegundos. O padrão é 60000. Para obter mais informações ou alterar essa configuração de propriedade, consulte [definir configurações de propriedade HealthCheckTimeout](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md).|  
  
## <a name="permissions"></a>Permissões  
 Exige permissões de VIEW SERVER STATE na instância do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa sys. dm_os_cluster_properties para retornar as configurações de propriedades do recurso de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 Este é um exemplo de conjunto de resultados.  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULO|0|3|60000|  
  
  
