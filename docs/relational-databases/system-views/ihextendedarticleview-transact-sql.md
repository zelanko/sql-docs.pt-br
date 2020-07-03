---
title: IHextendedArticleView (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: e15bb478ba04a95fa3c4d358477fe8073f50d007
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889216"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A exibição **IHextendedArticleView** expõe informações sobre artigos em uma publicação não SQL Server. Essa exibição é armazenada no banco de dados de **distribuição** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|O identificador exclusivo para o Publicador.|  
|**publication_id**|**int**|O identificador exclusivo para a publicação.|  
|**artigo**|**sysname**|O nome do artigo.|  
|**destination_object**|**sysname**|O nome do objeto publicado no Assinante.|  
|**source_owner**|**sysname**|O proprietário do objeto publicado no Assinante.|  
|**source_object**|**sysname**|O nome do objeto publicado no Assinante.|  
|**ndescrição**|**nvarchar (255)**|A descrição do artigo.|  
|**creation_script**|**nvarchar (255)**|O script de criação de esquema para o artigo.|  
|**del_cmd**|**nvarchar (255)**|O comando que é executado para um DELETE.|  
|**sem**|**int**|O identificador de objeto do procedimento armazenado usado para definir a partição horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo usada para filtragem horizontal.|  
|**ins_cmd**|**nvarchar (255)**|O comando que é executado para um INSERT.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = nenhum.<br /><br /> **1** = descartar.<br /><br /> **2** = excluir.<br /><br /> **3** = truncar.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = o artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções parametrizadas.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usam instruções parametrizadas.<br /><br /> Por exemplo, um artigo ativo usando instruções parametrizadas teria um valor de **17** nesta coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional é definida.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo baseado em log.<br /><br /> **3** = artigo baseado em log com filtro manual.<br /><br /> **5** = artigo baseado em log com exibição manual.<br /><br /> **7** = artigo baseado em log com filtro manual e exibição manual.|  
|**upd_cmd**|**nvarchar (255)**|O comando que é executado para um UPDATE.|  
|**schema_option**|**binary**|Indica o que será extraído do script. Consulte [sp_addarticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para obter uma lista de opções de esquema com suporte.|  
|**dest_owner**|**sysname**|O proprietário do objeto publicado no banco de dados de destino.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
