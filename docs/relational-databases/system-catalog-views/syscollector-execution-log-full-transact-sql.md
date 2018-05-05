---
title: syscollector_execution_log_full (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 39d4455e7db545d6fc5716322cc5dd76a79f702e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syscollectorexecutionlogfull-transact-sql"></a>syscollector_execution_log_full (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre o conjunto de coleta ou pacote quando o log de execução está cheio.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|Identifica cada execução do conjunto de coleta. Usado para unir essa exibição a outros logs detalhados. Permite valor nulo.|  
|parent_log_id|**bigint**|Identifica o pacote pai ou o conjunto de coleta. Não permite valor nulo. As IDs são encadeadas na relação pai-filho, o que permite determinar qual pacote foi iniciado por qual conjunto de coleta. Essa exibição agrupa as entradas de log pela vinculação pai-filho e recua os nomes dos pacotes de forma que o encadeamento de chamadas esteja claramente visível.|  
|nome|**nvarchar(4000)**|O nome do conjunto de coleta ou pacote que essa entrada de log representa. Permite valor nulo.|  
|status|**smallint**|Indica o status atual do conjunto de coleta ou do pacote. Permite valor nulo.<br /><br /> Os valores são:<br /><br /> 0 = em execução<br /><br /> 1 = concluído<br /><br /> 2 = Falha|  
|runtime_execution_mode|**smallint**|Indica se a atividade do conjunto de coleta estava coletando ou carregando dados. Permite valor nulo.|  
|start_time|**datetime**|A hora em que o conjunto de coleta ou o pacote foi iniciado. Permite valor nulo.|  
|last_iteration_time|**datetime**|Para pacotes de execução contínua, a última vez que o pacote capturou um instantâneo. Permite valor nulo.|  
|finish_time|**datetime**|A hora em que a execução de pacotes e de conjuntos de coletas foi concluída. Permite valor nulo.|  
|duration|**Int**|O tempo, em segundos, de execução do pacote ou do conjunto de coleta. Permite valor nulo.|  
|failure_message|**nvarchar(2048)**|Se houve falha no conjunto de coleta ou no pacote, a mais recente mensagem de erro para aquele componente. Permite valor nulo. Para obter informações mais detalhadas do erro, use o [fn_syscollector_get_execution_details &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) função.|  
|operador|**nvarchar(128)**|Identifica quem iniciou o conjunto de coleta ou o pacote. Permite valor nulo.|  
|package_execution_id|**uniqueidentifier**|Fornece um link para a tabela de logs [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Permite valor nulo.|  
|collection_set_id|**Int**|Fornece um link para a tabela de configuração de coleta de dados no msdb. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
