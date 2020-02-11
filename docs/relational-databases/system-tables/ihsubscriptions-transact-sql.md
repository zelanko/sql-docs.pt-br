---
title: IHsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: stevestein
ms.author: sstein
ms.openlocfilehash: b677e0f6c9be058650a46aee3465811b8f3eecc7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990148"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela do sistema **IHsubscriptions** contém uma linha para cada assinatura para uma publicação de um Publicador não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Identifica exclusivamente um artigo publicado.|  
|**srvid**|**smallint**|A ID de servidor do Assinante.|  
|**dest_db**|**sysname**|O nome do banco de dados de destino|  
|**login_name**|**sysname**|O nome de logon usado ao adicionar a assinatura.|  
|**distribution_jobid**|**Binary (16)**|A ID do trabalho da Agente de Distribuição|  
|**timestamp**|**timestamp**|A data e hora em que a assinatura foi criada.|  
|**queued_reinit**|**bit**|Especifica se o artigo é marcado para inicialização ou reinicialização. Um valor de **1** especifica que o artigo assinado está marcado para inicialização ou reinicialização.|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo.<br /><br /> **1** = assinado.<br /><br /> **2** = ativo.|  
|**sync_type**|**tinyint**|O tipo de sincronização inicial:<br /><br /> **1** = automático.<br /><br /> **2** = nenhum.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push-o Distribution Agent é executado no Assinante.<br /><br /> **1** = pull-o Distribution Agent é executado no distribuidor.|  
|**update_mode**|**tinyint**|O modo de atualização:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **0** = envia de volta.<br /><br /> **1** = não envia de volta.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
