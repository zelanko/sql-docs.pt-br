---
description: syscollector_execution_log_full (Transact-SQL)
title: syscollector_execution_log_full (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_log_full
- syscollector_execution_log_full_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log_full view
ms.assetid: 6c8db22d-2e4c-4b7c-ac5a-8762ef1b175b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b60d6f7efb33398789795753f8921ad9d5c55d1f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546704"
---
# <a name="syscollector_execution_log_full-transact-sql"></a>syscollector_execution_log_full (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações sobre o conjunto de coleta ou pacote quando o log de execução está cheio.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|Identifica cada execução do conjunto de coleta. Usado para unir essa exibição a outros logs detalhados. Permite valor nulo.|  
|parent_log_id|**bigint**|Identifica o pacote pai ou o conjunto de coleta. Não permite valor nulo. As IDs são encadeadas na relação pai-filho, o que permite determinar qual pacote foi iniciado por qual conjunto de coleta. Essa exibição agrupa as entradas de log pela vinculação pai-filho e recua os nomes dos pacotes de forma que o encadeamento de chamadas esteja claramente visível.|  
|name|**nvarchar(4000)**|O nome do conjunto de coleta ou pacote que essa entrada de log representa. Permite valor nulo.|  
|status|**smallint**|Indica o status atual do conjunto de coleta ou do pacote. Permite valor nulo.<br /><br /> Os valores são:<br /><br /> 0 = em execução<br /><br /> 1 = concluído<br /><br /> 2 = com falha|  
|runtime_execution_mode|**smallint**|Indica se a atividade do conjunto de coleta estava coletando ou carregando dados. Permite valor nulo.|  
|start_time|**datetime**|A hora em que o conjunto de coleta ou o pacote foi iniciado. Permite valor nulo.|  
|last_iteration_time|**datetime**|Para pacotes de execução contínua, a última vez que o pacote capturou um instantâneo. Permite valor nulo.|  
|finish_time|**datetime**|A hora em que a execução de pacotes e de conjuntos de coletas foi concluída. Permite valor nulo.|  
|duration|**int**|O tempo, em segundos, de execução do pacote ou do conjunto de coleta. Permite valor nulo.|  
|failure_message|**nvarchar(2048)**|Se houve falha no conjunto de coleta ou no pacote, a mais recente mensagem de erro para aquele componente. Permite valor nulo. Para obter informações de erro mais detalhadas, use o [fn_syscollector_get_execution_details &#40;função&#41;Transact-SQL ](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) .|  
|operador|**nvarchar(128)**|Identifica quem iniciou o conjunto de coleta ou o pacote. Permite valor nulo.|  
|package_execution_id|**uniqueidentifier**|Fornece um link para a tabela de logs [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Permite valor nulo.|  
|collection_set_id|**int**|Fornece um link para a tabela de configuração de coleta de dados no msdb. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
