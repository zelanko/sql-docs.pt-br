---
title: catalog.execution_data_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 90872764fd09ab78d9a98a0c9edc2c6e71479d26
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272943"
---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream para determinada execução do pacote. As informações desta exibição podem ser usadas para computar a taxa de transferência de dados para um componente.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|A ID (identificador exclusivo) dos dados.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|package_name|**nvarchar(260)**|O nome do primeiro pacote que foi iniciado durante a execução.|  
|task_name|**nvarchar(4000)**|O nome da tarefa de fluxo de dados.|  
|dataflow_path_id_string|**nvarchar(4000)**|A cadeia de caracteres de identificação do caminho de fluxo de dados.|  
|dataflow_path_name|**nvarchar(4000)**|Nome do caminho de fluxo de dados.|  
|source_component_name|**nvarchar(4000)**|O nome do componente do fluxo de dados que enviou os dados.|  
|destination_component_name|**nvarchar(4000)**|O nome do componente do fluxo de dados que recebeu os dados.|  
|rows_sent|**bigint**|O número de linhas enviadas ao componentes de origem.|  
|created_time|**datatimeoffset(7)**|A hora em que os valores foram obtidos.|  
|execution_path|**nvarchar(max)**|O caminho de execução do componente.|  
  
## <a name="remarks"></a>Remarks  
  
-   Quando houver várias saídas do componente, uma linha será adicionada para cada uma das saídas.  
  
-   Por padrão, quando uma execução é iniciada, as informações sobre o número de linhas que são enviadas não são registradas em log.  
  
-   Para exibir esses dados para uma execução específica de pacote, defina o nível de log como **Detalhado**. Para saber mais, veja [Habilitar o log para a execução do pacote no servidor SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
