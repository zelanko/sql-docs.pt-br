---
description: MSmerge_conflicts_info (Transact-SQL)
title: MSmerge_conflicts_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2acd79359758c4bc5c14d8d204a5b5ac6b889c48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469041"
---
# <a name="msmerge_conflicts_info-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_conflicts_info** rastreia os conflitos que ocorrem durante a sincronização de uma assinatura para uma publicação de mesclagem. Os dados de linha perdidos para conflitos são armazenados na tabela [MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md) do artigo em que o conflito ocorreu. Essa tabela é armazenada no Publicador, no banco de dados de publicação, e no Assinante, no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|O apelido da tabela publicada.|  
|**ROWGUID**|**uniqueidentifier**|O identificador para a linha de conflito.|  
|**origin_datasource**|**nvarchar(255)**|O nome do banco de dados onde a alteração conflitante teve origem.|  
|**conflict_type**|**int**|O tipo de conflito ocorrido, que pode ser um dos seguintes:<br /><br /> **1** = conflito de atualização: o conflito é detectado no nível de linha.<br /><br /> **2** = conflito de atualização de coluna: o conflito detectado no nível de coluna.<br /><br /> **3** = atualizar conflito de exclusão de WINS: a exclusão vence o conflito.<br /><br /> **4** = atualizar o conflito de exclusão do WINS: o ROWGUID excluído que perde o conflito é registrado nesta tabela.<br /><br /> **5** = falha ao carregar inserção: não foi possível aplicar a inserção do Assinante no Publicador.<br /><br /> **6** = falha ao inserir download: não foi possível aplicar a inserção do Publicador no Assinante.<br /><br /> **7** = falha ao excluir upload: a exclusão no Assinante não pôde ser carregada no Publicador.<br /><br /> **8** = falha ao excluir download: a exclusão no Publicador não pôde ser baixada para o Assinante.<br /><br /> **9** = falha na atualização do carregamento: não foi possível aplicar a atualização no Assinante no Publicador.<br /><br /> **10** = falha na atualização do download: a atualização no Publicador não pôde ser aplicada ao Assinante.<br /><br /> **11** = resolução<br /><br /> **12** = atualização do registro lógico WINS excluir: o registro lógico excluído que perde o conflito é registrado nesta tabela.<br /><br /> **13** = atualização de inserção de conflito de registro lógico: Insert em um registro lógico está em conflito com uma atualização.<br /><br /> **14** = registro lógico excluir conflito de atualização do WINS: o registro lógico atualizado que perde o conflito é registrado nesta tabela.|  
|**reason_code**|**int**|O código de erro que pode ser sensível ao contexto. No caso de conflitos UPDATE-UPDATE e Update-Delete, o valor usado para essa coluna é o mesmo que o **conflict_type**. No entanto, em conflitos de alteração com falha, o código da razão é o erro que impediu o Merge Agent de aplicar a alteração. Por exemplo, se o Agente de Mesclagem não puder aplicar uma inserção no Assinante devido a uma violação de chave primária, ele registrará um **conflict_type** de 6 ("falha no download de inserção") e uma **reason_code** de 2627, que é a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem de erro interna para uma violação de chave primária: "violação da restrição% ls '%. * ls '. Não é possível inserir a chave duplicada no objeto '%. \* ls "."|  
|**reason_text**|**nvarchar (720)**|A descrição do erro que pode ser sensível ao contexto.|  
|**pubid**|**uniqueidentifier**|O identificador para a publicação.|  
|**MSrepl_create_time**|**datetime**|A hora em que o conflito ocorreu.|  
|**origin_datasource_id**|**uniqueidentifier**|O identificador do banco de dados onde a alteração conflitante teve origem.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
