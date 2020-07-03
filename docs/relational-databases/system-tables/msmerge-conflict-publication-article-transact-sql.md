---
title: MSmerge_conflict_publication_article (T-SQL)
description: Descreve o MSmerge_conflict_publication_article procedimento armazenado que contém informações sobre linhas que foram desfeitas em conflito ou alterações de linha que não foram feitas para obter a convergência de dados.
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fbad328f7b384cc75620a5be04b624331796a51b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889891"
---
# <a name="msmerge_conflict_publication_article-transact-sql"></a>MSmerge_conflict_publication_article (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_conflict_publication_article** contém informações sobre linhas que foram desfeitas em conflito ou alterações de linha que não foram realizadas para obter a convergência de dados. Existe uma tabela de conflitos para cada tabela replicada na publicação, onde o nome da tabela de conflitos é anexada com o nome da publicação e do artigo. Essas tabelas de conflitos específicas do artigo existem no banco de dados usado para registro de conflito, geralmente o banco de dados de publicação, mas pode ser o banco de dados de assinatura se houver log de conflitos descentralizado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**_\_nome da coluna do artigo \__**|**variável**|Representa uma coluna em uma tabela replicada. Essa tabela do sistema contém uma coluna para cada coluna no artigo de tabela.|  
|**rowguid**|**uniqueidentifier**|O identificador de linha para o conflito de exclusão.|  
|**ModifiedDate**|**datetime**|A hora em que o conflito ocorreu.|  
|**\_ID da fonte de origem \_**|**uniqueidentifier**|A assinatura para a qual a alteração de linha foi desfeita ou perdeu o conflito.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
