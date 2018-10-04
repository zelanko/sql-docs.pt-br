---
title: IHextendedArticleView (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 9ed3cb8ca49a22d9358941554cdef2030d584fb2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848954"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHextendedArticleView** exibição expõe informações sobre artigos em uma publicação não SQL Server. Essa exibição é armazenada na **distribuição** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|O identificador exclusivo para o Publicador.|  
|**publication_id**|**int**|O identificador exclusivo para a publicação.|  
|**article**|**sysname**|O nome do artigo.|  
|**destination_object**|**sysname**|O nome do objeto publicado no Assinante.|  
|**source_owner**|**sysname**|O proprietário do objeto publicado no Assinante.|  
|**source_object**|**sysname**|O nome do objeto publicado no Assinante.|  
|**Descrição**|**nvarchar(255)**|A descrição do artigo.|  
|**creation_script**|**nvarchar(255)**|O script de criação de esquema para o artigo.|  
|**del_cmd**|**nvarchar(255)**|O comando que é executado para um DELETE.|  
|**filtro**|**int**|O identificador de objeto do procedimento armazenado usado para definir a partição horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo usada para filtragem horizontal.|  
|**ins_cmd**|**nvarchar(255)**|O comando que é executado para um INSERT.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DESCARTAR.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCAR.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções com parâmetros.<br /><br /> **24** = ambos incluir o nome da coluna em instruções INSERT e usar instruções com parâmetros.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor de **17** nesta coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo com base em log.<br /><br /> **3** = artigo com base em log com filtro manual.<br /><br /> **5** = artigo com base em log com exibição manual.<br /><br /> **7** = artigo com base em log com filtro manual e exibição manual.|  
|**upd_cmd**|**nvarchar(255)**|O comando que é executado para um UPDATE.|  
|**schema_option**|**binary**|Indica os scripts a serem feitos. Ver [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para obter uma lista das opções de esquema com suporte.|  
|**dest_owner**|**sysname**|O proprietário do objeto publicado no banco de dados de destino.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
