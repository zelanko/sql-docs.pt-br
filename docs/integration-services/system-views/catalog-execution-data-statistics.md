---
title: execution_data_statistics | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fa1d87489ff6d0a10d95bf160ded3d038ca39d81
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream para determinada execução do pacote. As informações desta exibição podem ser usadas para computar a taxa de transferência de dados para um componente.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|A ID (identificador exclusivo) dos dados.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|package_name|**nvarchar (260)**|O nome do primeiro pacote que foi iniciado durante a execução.|  
|task_name|**nvarchar(4000)**|O nome da tarefa de fluxo de dados.|  
|dataflow_path_id_string|**nvarchar(4000)**|A cadeia de caracteres de identificação do caminho de fluxo de dados.|  
|dataflow_path_name|**nvarchar(4000)**|Nome do caminho de fluxo de dados.|  
|source_component_name|**nvarchar(4000)**|O nome do componente do fluxo de dados que enviou os dados.|  
|destination_component_name|**nvarchar(4000)**|O nome do componente do fluxo de dados que recebeu os dados.|  
|rows_sent|**bigint**|O número de linhas enviadas ao componentes de origem.|  
|created_time|**datatimeoffset(7)**|A hora em que os valores foram obtidos.|  
|execution_path|**nvarchar(max)**|O caminho de execução do componente.|  
  
## <a name="remarks"></a>Comentários  
  
-   Quando houver várias saídas do componente, uma linha será adicionada para cada uma das saídas.  
  
-   Por padrão, quando uma execução é iniciada, as informações sobre o número de linhas que são enviadas não são registradas em log.  
  
-   Para exibir esses dados para uma determinada execução do pacote, defina o nível de log como **detalhado**. Para saber mais, veja [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  

