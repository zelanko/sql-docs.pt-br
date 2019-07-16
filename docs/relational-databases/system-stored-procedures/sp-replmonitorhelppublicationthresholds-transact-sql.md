---
title: sp_replmonitorhelppublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
ms.openlocfilehash: a80ff5308edee02d24d214a6520a090750600edc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950573"
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a métrica de limite definida para uma publicação monitorada. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do publicador. *Publisher* está **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicado. *publisher_db* está **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @publication_type = ] publication_type` Se o tipo de publicação. *publication_type* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|A replicação tenta determinar o tipo de publicação.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|ID da métrica de desempenho de replicação, que pode ter um destes valores.<br /><br /> **1expiration** -monitora a expiração iminente de assinaturas para publicações transacionais.<br /><br /> **2latency** -monitora o desempenho de assinaturas para publicações transacionais.<br /><br /> **4mergeexpiration** -monitora a expiração iminente de assinaturas para publicações de mesclagem.<br /><br /> **5mergeslowrunduration** -monitora a duração de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).<br /><br /> **6mergefastrunduration** -monitora a duração de sincronizações de mesclagem em conexões de alta largura de banda (LAN).<br /><br /> **7mergefastrunspeed** -monitora a taxa de sincronizações de mesclagem em conexões de alta largura de banda (LAN).<br /><br /> **8mergeslowrunspeed** -monitora a taxa de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
|**title**|**sysname**|Nome da métrica de desempenho da replicação.|  
|**value**|**int**|O valor de limite da métrica de desempenho.|  
|**shouldalert**|**bit**|É se um alerta deve ser gerado quando a métrica excede o limite definido para esta publicação; um valor de **1** indica que um alerta deve ser gerado.|  
|**isenabled**|**bit**|É se o monitoramento está habilitado para esta métrica de desempenho de replicação para esta publicação; um valor de **1** indica que o monitoramento está habilitado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorhelppublicationthresholds** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição podem executar **sp_replmonitorhelppublicationthresholds**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
