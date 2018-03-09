---
title: IHextendedArticleView (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 413a95e5d39b5a335381f25a8214df9a0b3be779
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHextendedArticleView** exibição expõe informações sobre artigos em uma publicação não SQL Server. Essa exibição é armazenada no **distribuição** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|O identificador exclusivo para o Publicador.|  
|**publication_id**|**Int**|O identificador exclusivo para a publicação.|  
|**article**|**sysname**|O nome do artigo.|  
|**destination_object**|**sysname**|O nome do objeto publicado no Assinante.|  
|**source_owner**|**sysname**|O proprietário do objeto publicado no Assinante.|  
|**source_object**|**sysname**|O nome do objeto publicado no Assinante.|  
|**description**|**nvarchar(255)**|A descrição do artigo.|  
|**creation_script**|**nvarchar(255)**|O script de criação de esquema para o artigo.|  
|**del_cmd**|**nvarchar(255)**|O comando que é executado para um DELETE.|  
|**filtro**|**Int**|O identificador de objeto do procedimento armazenado usado para definir a partição horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo usada para filtragem horizontal.|  
|**ins_cmd**|**nvarchar(255)**|O comando que é executado para um INSERT.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCAR.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções com parâmetros.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usar instruções com parâmetros.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor de **17** nesta coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo com base em log.<br /><br /> **3** = artigo com base em log com filtro manual.<br /><br /> **5** = artigo com base em log com exibição manual.<br /><br /> **7** = artigo com base em log com filtro manual e exibição manual.|  
|**upd_cmd**|**nvarchar(255)**|O comando que é executado para um UPDATE.|  
|**schema_option**|**binary**|Indica os scripts a serem feitos. Consulte [sp_addarticle &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para obter uma lista das opções de esquema com suporte.|  
|**dest_owner**|**sysname**|O proprietário do objeto publicado no banco de dados de destino.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
