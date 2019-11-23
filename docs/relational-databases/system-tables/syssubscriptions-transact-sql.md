---
title: syssubscriptions (Transact-SQL) | Microsoft Docs
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
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 251dbb143c1b5aa150cc094ce67943dd0139ee6d
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305017"
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada assinatura no banco de dados. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A ID exclusiva de um artigo.|  
|**srvid**|**smallint**|A ID de servidor do Assinante.|  
|**dest_db**|**sysname**|O nome do banco de dados de destino.|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo.<br /><br /> **1** = assinado.<br /><br /> **2** = ativo.|  
|**sync_type**|**tinyint**|O tipo de sincronização inicial:<br /><br /> **1** = automático.<br /><br /> **2** = nenhum|  
|**login_name**|**sysname**|O nome de logon usado ao adicionar a assinatura.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> 0 = Push - o agente de distribuição é executado no Distribuidor.<br /><br /> 1 = Pull - o agente de distribuição é executado no Assinante.|  
|**distribution_jobid**|**binary(16)**|A ID do trabalho da Agente de Distribuição.|  
|**timestamp**|**timestamp**|O carimbo de data e hora.|  
|**update_mode**|**tinyint**|O modo de atualização:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **0** = envia de volta.<br /><br /> **1** = não envia de volta.|  
|**queued_reinit**|**bit**|Especifica se o artigo é marcado para inicialização ou reinicialização. Um valor de **1** especifica que o artigo assinado está marcado para inicialização ou reinicialização.|  
|**nosync_type**|**tinyint**|O tipo de inicialização de assinatura :<br /><br /> **0** = automático (instantâneo)<br /><br /> **1** = suporte somente à replicação<br /><br /> **2** = inicializar com backup<br /><br /> **3** = inicializar do número de sequência de log (LSN)<br /><br /> Para obter mais informações, consulte o parâmetro **\@sync_type** de [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).|  
|**srvname**|**sysname**|O nome do Assinante.|  
  
## <a name="see-also"></a>Consulte também  
   [de &#40;Transact-SQL&#41; de tabelas de replicação](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
