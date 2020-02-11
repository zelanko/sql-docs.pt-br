---
title: syssubscriptions (exibição do sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 517d9359085f7cb4bc4c94eb941981a09ca06eef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304782"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (Exibição de sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A exibição **syssubscriptions** expõe informações de assinatura. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A ID exclusiva de um artigo assinado.|  
|**srvid**|**smallint**|A ID de servidor do Assinante.|  
|**dest_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo.<br /><br /> **1** = assinado.<br /><br /> **2** = ativo.|  
|**sync_type**|**tinyint**|O tipo de sincronização inicial:<br /><br /> **1** = automático.<br /><br /> **2** = nenhum.|  
|**login_name**|**sysname**|O nome de logon usado ao conectar ao Publicador para adicionar a assinatura.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push-o Distribution Agent é executado no distribuidor.<br /><br /> **1** = pull-o Distribution Agent é executado no Assinante.|  
|**distribution_jobid**|**Binary (16)**|Identifica o trabalho do Distribution Agent usado para sincronizar a assinatura.|  
|**timestmap**|**timestamp**|A data e hora em que a assinatura foi criada.|  
|**update_mode**|**tinyint**|O modo de atualização:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **0** = envia de volta.<br /><br /> **1** = não envia de volta.|  
|**queued_reinit**|**bit**|Especifica se o artigo é marcado para inicialização ou reinicialização. Um valor de **1** especifica que o artigo assinado está marcado para inicialização ou reinicialização.|  
|**nosync_type**|**tinyint**|O tipo de inicialização de assinatura :<br /><br /> **0** = automático (instantâneo)<br /><br /> **1** = suporte somente à replicação<br /><br /> **2** = inicializar com backup<br /><br /> **3** = inicializar do número de sequência de log (LSN)<br /><br /> Para obter mais informações, consulte ** \@** o parâmetro sync_type de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **Beta** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|O nome do Assinante.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;syssubscriptions &#40;Transact-SQL](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
