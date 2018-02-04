---
title: dbo. slo_assignment_history (banco de dados do SQL Azure) | Microsoft Docs
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
- dbo.slo_assignment_history
- slo_assignment_history
- slo_assignment_history_TSQL
- dbo.slo_assignment_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
ms.assetid: 048a6fb5-2fc2-4d12-a436-4c53ecd413f3
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61bab47646d1acff9edcfbf461588b3560916acd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="dbosloassignmenthistory-azure-sql-database"></a>dbo.slo_assignment_history (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **Isso se aplica somente ao [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.**  
>   
>  Esse recurso está em um estado de visualização. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
  
 Retorna o histórico de atribuições de SLO de banco de dados no servidor, inclusive o seguinte:  
  
-   O histórico de atribuições de SLO de banco de dados no servidor.  
  
-   Hora de início e término de cada solicitação de alteração do SLO do banco de dados.  
  
-   Qualquer erro de atribuição de SLO que for registrado nas colunas error_code e error_desc.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|Nome do banco de dados.|  
|database_id|**Int**|ID do banco de dados.|  
|create_date|**datetimeoffset(7)**|Data de criação do banco de dados.|  
|service_objective_name|**sysname**|Nome do SLO (objetivo de nível de serviço).|  
|service_objective_id|**uniqueidentifier**|A ID do SLO.|  
|operation_id|**uniqueidentifier**|Identificador da operação.|  
|operation_start_time|**datetimeoffset(7)**|Hora de início da solicitação de alteração do SLO do banco de dados.|  
|operation_end_time|**datetimeoffset(7)**|Hora de término da solicitação de alteração do SLO do banco de dados.|  
|error_code|**Int**|Código de erro da solicitação de alteração do SLO do banco de dados.|  
|error_desc|**nvarchar**|Descrição do erro na solicitação de alteração do SLO do banco de dados.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o histórico de atribuições de SLO de banco de dados para um banco de dados especificado.  
  
```  
SELECT *  
FROM dbo.slo_assignment_history   
WHERE database_name = '<DB NAME>’   
ORDER BY operation_start_time DESC;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando bancos de dados Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
