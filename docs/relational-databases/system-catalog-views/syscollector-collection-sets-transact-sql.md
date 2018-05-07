---
title: syscollector_collection_sets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_collection_sets_TSQL
- syscollector_collection_sets
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collection_sets view
ms.assetid: db0def92-f25b-45da-9709-eab972b33800
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7407828836e4831e313e982111df7f61bd110e8e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="syscollectorcollectionsets-transact-sql"></a>syscollector_collection_sets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre um conjunto de coleta, inclusive agendamento, modo de coleta e seu estado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|collection_set_id|**Int**|É o identificador local do conjunto de coleções. Não permite valor nulo.|  
|collection_set_uid|**uniqueidentifier**|O identificador global exclusivo do conjunto de coleta. Não permite valor nulo.|  
|nome|**nvarchar(4000)**|Nome do conjunto de coleta. Permite valor nulo.|  
|target|**nvarchar(max)**|Identifica o destino do conjunto de coleta. Permite valor nulo.|  
|is_system|**bit**|Ativado (1) ou desativado (0) para indicar se o conjunto de coleta foi incluído no coletor de dados ou se foi adicionado depois pelo dc_admin. Pode ser um conjunto de coleta personalizado desenvolvido internamente ou por um terceiro. Não permite valor nulo.|  
|is_running|**bit**|Indica se o conjunto de coleta está sendo executado ou não. Não permite valor nulo.|  
|collection_mode|**smallint**|Especifica o modo de coleta do conjunto de coleta. Não permite valor nulo.<br /><br /> O modo de coleta pode ser um dos itens a seguir:<br /><br /> 0 - Modo de cache. A coleta e o carregamento de dados estão em agendas separadas.<br /><br /> 1 - Modo não armazenado em cache. A coleta e o carregamento dos dados estão na mesma agenda.|  
|proxy_id|**Int**|Identifica o proxy usado para executar a etapa do trabalho do conjunto de coleta. Permite valor nulo.|  
|schedule_uid|**uniqueidentifier**|Fornece um ponteiro à agenda de conjunto de coleta. Permite valor nulo.|  
|collection_job_id|**uniqueidentifier**|Identifica o trabalho de coleta. Permite valor nulo.|  
|upload_job_id|**uniqueidentifier**|Identifica o trabalho de carregamento de coleta. Permite valor nulo.|  
|logging_level|**smallint**|Especifica o nível de log (0, 1 ou 2). Não permite valor nulo.|  
|days_until_expiration|**smallint**|O número de dias durante os quais os dados coletados são salvos no data warehouse de gerenciamento. Não permite valor nulo.|  
|descrição|**nvarchar(4000)**|Descreve o conjunto de coleta. Permite valor nulo.|  
|dump_on_any_error|**bit**|Ativado (1) ou desativado (0) para indicar se deseja criar um [!INCLUDE[ssIS](../../includes/ssis-md.md)] arquivo de despejo de qualquer erro. Não permite valor nulo.|  
|dump_on_codes|**nvarchar(max)**|Contém a lista de [!INCLUDE[ssIS](../../includes/ssis-md.md)] códigos de erro que são usados para disparar o arquivo de despejo. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer SELECT para dc_operator, dc_proxy.  
  
## <a name="remarks"></a>Remarks  
 A API do coletor de dados só permite que você altere ou exclua os conjuntos de coleta que você criar. Os conjuntos de coleta fornecidos com o sistema não podem ser modificados ou excluídos. Porém, você pode habilitar ou desabilitar um conjunto de coleta do sistema e alterar a sua configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Exibições do Coletor de Dados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
