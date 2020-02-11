---
title: sys. dm_fts_semantic_similarity_population (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_semantic_similarity_population_TSQL
- sys.dm_fts_semantic_similarity_population
- dm_fts_semantic_similarity_population
- sys.dm_fts_semantic_similarity_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_semantic_similarity_population dynamic management view
ms.assetid: 33666f28-c370-47e2-a932-190316ed5f69
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 280ab197ef9347c6a209be7ef05e8f1ce2dfd23e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900880"
---
# <a name="sysdm_fts_semantic_similarity_population-transact-sql"></a>sys.dm_fts_semantic_similarity_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha de informações de status sobre a população do índice de similaridade de documento para cada índice de similaridade em cada tabela que tem um índice semântico associado.  
  
 A etapa de população segue a etapa de extração. Para obter informações de status sobre a etapa de extração de similaridade, consulte [Sys. dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md).  
    
||||  
|-|-|-|  
|**Nome da coluna**|**Tipo**|**Descrição**|  
|**database_id**|**int**|ID do banco de dados que contém o índice de texto completo que está sendo populado.|  
|**catalog_id**|**int**|ID do catálogo de texto completo que contém este índice de texto completo.|  
|**table_id**|**int**|ID da tabela para a qual o índice de texto completo está sendo populado.|  
|**document_count**|**int**|Número total de documentos na população.|  
|**document_processed_count**|**int**|Número de documentos processados desde o início deste ciclo de população|  
|**completion_type**|**int**|Status de como esta população foi concluída.|  
|**completion_type_description**|**nvarchar (120)**|Descrição do tipo de conclusão.|  
|**worker_count**|**int**|Número de threads de trabalho associados com a extração de similaridade|  
|**Estado**|**int**|Status desta população. Observação: alguns dos estados são transitórios. Um dos seguintes:<br /><br /> 3 = Iniciando<br /><br /> 5 = Processando normalmente<br /><br /> 7 = Parou de processar<br /><br /> 11 = População anulada|  
|**status_description**|**nvarchar (120)**|Descrição do status da população.|  
|**start_time**|**datetime**|Hora em que a população foi iniciada.|  
|**incremental_timestamp**|**timestamp**|Representa o carimbo de data/hora inicial para uma população completa. Para todos os outros tipos de população, esse valor é o último ponto de verificação confirmado que representa o andamento das populações.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter mais informações sobre o status de Indexação semântica, consulte [Sys. dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como consultar o status das populações de índice de similaridade de documento para todas as tabelas que têm um índice semântico associado:  
  
```  
SELECT * FROM sys.dm_fts_semantic_similarity_population;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
