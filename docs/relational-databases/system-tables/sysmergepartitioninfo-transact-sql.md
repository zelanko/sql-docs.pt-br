---
description: sysmergepartitioninfo (Transact-SQL)
title: sysmergepartitioninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b987adef188e580b38f5f4df5b24b4f6ab22825b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427578"
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações sobre partições para cada artigo. Contém uma linha para cada artigo de mesclagem definido no banco de dados local. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo desta publicação, gerado quando a publicação foi adicionada.|  
|**partition_view_id**|**int**|A ID da exibição de partição desta tabela. A exibição mostra um mapeamento de cada linha no artigo para os diferentes IDs de partição à qual ele pertence.|  
|**repl_view_id**|**int**|A ser adicionado.|  
|**partition_deleted_view_rule**|**nvarchar(4000)**|A instrução SQL usada em um gatilho de replicação de mesclagem para recuperar a ID de partição de cada linha excluída ou atualizada com base em seus valores antigos de coluna.|  
|**partition_inserted_view_rule**|**nvarchar(4000)**|A instrução SQL usada em um gatilho de replicação de mesclagem para recuperar a ID de partição de cada linha inserida ou atualizada com base em seus novos valores de coluna.|  
|**membership_eval_proc_name**|**sysname**|O nome do procedimento que avalia as IDs de partição atuais de linhas no **MSmerge_contents**.|  
|**column_list**|**nvarchar(4000)**|A lista separada por vírgula de colunas replicadas em um artigo.|  
|**column_list_blob**|**nvarchar(4000)**|A lista separada por vírgulas de colunas replicada em um artigo, incluindo colunas de objeto binário grande.|  
|**expand_proc**|**sysname**|O nome do procedimento que reavalia IDs de partição para todas as linhas filho de uma linha pai recém-inserida e para linhas pai que sofreram alterações de partição ou foram excluídas.|  
|**logical_record_parent_nickname**|**int**|O apelido de pai de alto nível de um determinado artigo em um registro lógico.|  
|**logical_record_view**|**int**|Uma exibição que produz o rowguid de artigo pai de alto nível correspondente a cada rowguid filho.|  
|**logical_record_deleted_view_rule**|**nvarchar(4000)**|Semelhante a **logical_record_view**, exceto o que mostra as linhas filhas na tabela "Deleted" nos gatilhos Update e Delete.|  
|**logical_record_level_conflict_detection**|**bit**|Indica se os conflitos devem ser detectados no nível de registro lógico, ou no nível de linha ou coluna.<br /><br /> **0** = a detecção de conflito em nível de linha ou coluna é usada.<br /><br /> **1** = a detecção de conflito de registro lógico é usada, em que uma alteração em uma linha no Publicador e alterada em uma linha separada o mesmo registro lógico no assinante é tratada como um conflito.<br /><br /> Quando esse valor for **1**, somente a resolução de conflitos de nível de registro lógico poderá ser usada.|  
|**logical_record_level_conflict_resolution**|**bit**|Indica se os conflitos devem ser resolvidos no nível de registro lógico, ou no nível de linha ou coluna.<br /><br /> **0** = a resolução em nível de linha ou coluna é usada.<br /><br /> **1** = no caso de um conflito, o registro lógico inteiro do vencedor substitui todo o registro lógico no lado perdido.<br /><br /> Um valor de **1** pode ser usado com a detecção de nível de registro lógico e com detecção em nível de linha ou coluna.|  
|**partition_options**|**tinyint**|Define a forma pela qual os dados no artigo são particionados, o que habilita otimizações de desempenho quando todas as linhas pertencem a apenas uma partição ou assinatura. *partition_options* pode ser um dos valores a seguir.<br /><br /> **0** = a filtragem do artigo é estática ou não produz um subconjunto exclusivo de dados para cada partição, ou seja, uma partição de "sobreposição".<br /><br /> **1** = as partições estão sobrepostas e as atualizações DML feitas no Assinante não podem alterar a partição à qual uma linha pertence.<br /><br /> **2** = a filtragem do artigo produz partições não sobrepostas, mas vários assinantes podem receber a mesma partição.<br /><br /> **3** = a filtragem do artigo gera partições não sobrepostas que são exclusivas para cada assinatura.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
