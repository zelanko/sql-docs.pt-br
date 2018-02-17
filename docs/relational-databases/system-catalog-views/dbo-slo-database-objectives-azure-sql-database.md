---
title: dbo.slo_database_objectives (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_database_objectives
- dbo.slo_database_objectives_TSQL
- slo_database_objectives_TSQL
- slo_database_objectives
dev_langs:
- TSQL
helpviewer_keywords:
- slo_database_objectives
- dbo.slo_database_objectives
ms.assetid: a522569d-8cfc-4643-a170-1cd291e61eee
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10227990cb6c5928fcc403ee35a978cbf93ad6ca
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2018
---
# <a name="dboslodatabaseobjectives-azure-sql-database"></a>dbo.slo_database_objectives (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **Isso se aplica somente ao [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
>   
>  Para [! INCLUIR[ssSDSfull](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) (no mestre) para a operação ALTER DATABASE.   
  
 Retorna o status da atribuição de um objetivo de nível de serviço (SLO) em um banco de dados SQL.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|Nome do banco de dados.|  
|current_slo|**sysname**|SLO atual do banco de dados.|  
|target_slo|**sysname**|SLO de destino do banco de dados, conforme especificado na solicitação de alteração do SLO.|  
|state_desc|**nvarchar**|Status da solicitação de alteração de SLO: concluído ou pendente.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
```  
SELECT   
database_name=database_name.name   
    , current_slo=current_slo.name   
    , target_slo=target_slo.name   
    , state_desc=database_slo.state_desc   
FROM slo_database_objectives AS database_slo  
INNER JOIN slo_service_objectives AS current_slo ON database_slo.current_objective_id = current_slo.objective_id  
INNER JOIN slo_service_objectives AS target_slo ON database_slo.configured_objective_id = target_slo.objective_id  
INNER JOIN sys.databases AS database_name  ON database_slo.database_id = database_name.database_id;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando bancos de dados Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
[sys.dm_operation_status (Banco de Dados SQL do Azure)](../system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 
