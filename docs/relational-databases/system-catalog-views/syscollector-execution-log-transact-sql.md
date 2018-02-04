---
title: syscollector_execution_log (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_execution_log_TSQL
- syscollector_execution_log
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log view
ms.assetid: 11554d64-0426-42ce-b7ce-5591f67864d2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f5beb35aa769b1c4755481a187c765fa62068ae2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorexecutionlog-transact-sql"></a>syscollector_execution_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações do log de execução para um conjunto de coleta ou pacote.   
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|Identifica cada execução do conjunto de coleta. Usado para unir essa exibição a outros logs detalhados. Não permite valor nulo.|  
|parent_log_id|**bigint**|Identifica o pacote pai ou o conjunto de coleta. Não permite valor nulo. As IDs são encadeadas na relação pai-filho, o que permite determinar qual pacote foi iniciado por qual conjunto de coleta. Essa exibição agrupa as entradas de log pela vinculação pai-filho e recua os nomes dos pacotes de forma que o encadeamento de chamada seja claramente visível.|  
|collection_set_id|**Int**|Identifica o conjunto de coleta ou pacote que essa entrada de log representa. Não permite valor nulo.|  
|collection_item_id|**Int**|Identifica um item de coleção. Permite valor nulo.|  
|start_time|**datetime**|A hora em que o conjunto de coleta ou o pacote foi iniciado. Não permite valor nulo.|  
|last_iteration_time|**datetime**|Para pacotes de execução contínua, a última vez que o pacote capturou um instantâneo. Permite valor nulo.|  
|finish_time|**datetime**|A hora em que a execução de pacotes e de conjuntos de coletas foi concluída. Permite valor nulo.|  
|runtime_execution_mode|**smallint**|Indica se a atividade do conjunto de coleta estava coletando ou carregando dados. Permite valor nulo.<br /><br /> Os valores são:<br /><br /> 0 = Collection<br /><br /> 1 = Carregar|  
|status|**smallint**|Indica o status atual do conjunto de coleta ou do pacote. Não permite valor nulo.<br /><br /> Os valores são:<br /><br /> 0 = em execução<br /><br /> 1 = concluído<br /><br /> 2 = Falha|  
|operador|**nvarchar(128)**|Identifica quem iniciou o conjunto de coleta ou o pacote. Não permite valor nulo.|  
|package_id|**uniqueidentifier**|Identifica o conjunto de coleta ou pacote que gerou esse log. Permite valor nulo.|  
|package_name|**nvarchar(4000)**|O nome do pacote que gerou este log. Permite valor nulo.|  
|package_execution_id|**uniqueidentifier**|Fornece um link para a tabela de logs [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Permite valor nulo.|  
|failure_message|**nvarchar(2048)**|Se houve falha no conjunto de coleta ou no pacote, a mais recente mensagem de erro para aquele componente. Permite valor nulo. Para obter informações mais detalhadas do erro, use o [fn_syscollector_get_execution_details &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) função.|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT para dc_operator.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
