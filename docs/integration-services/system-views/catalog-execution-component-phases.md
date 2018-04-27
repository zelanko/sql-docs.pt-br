---
title: catalog.execution_component_phases | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0d2adcbca51ab471f3c9b488adea2e4d82aa1dc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe o tempo gasto por um componente de fluxo de dados em cada fase de execução.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|A ID (identificador exclusivo) da fase.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|package_name|**nvarchar(260)**|O nome do primeiro pacote que foi iniciado durante a execução.|  
|task_name|**nvarchar(4000)**|O nome da tarefa de fluxo de dados.|  
|subcomponent_name|**nvarchar(4000)**|Nome do componente de fluxo de dados.|  
|fase|**nvarchar(128)**|O nome da fase de execução.|  
|start_time|**datetimeoffset(7)**|A hora de início da fase.|  
|end_time|**datetimeoffset(7)**|A hora de término da fase.|  
|execution_path|**nvarchar(max)**|O caminho da execução da tarefa de fluxo de dados.|  
  
## <a name="remarks"></a>Remarks  
 Essa exibição exibe uma linha para cada fase de execução de um componente de fluxo de dados, como Validate, Pre-Execute, Post-Execute, PrimeOutput e ProcessInput. Cada linha exibe a hora de início e de término de uma fase de execução específica.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a exibição catalog.execution_component_phases para localizar o tempo total que um pacote específico gastou na execução em todas as fases (**active_time**) e o tempo total decorrido para o pacote (**total_time**).  
  
> [!WARNING]  
>  A exibição catalog.execution_component_phases oferece essas informações quando o nível de log da execução do pacote está definido como desempenho ou detalhado. Para saber mais, veja [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
