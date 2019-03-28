---
title: sp_replmonitorchangepublicationthreshold (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 587c66322a7d40f42f81bceb48e1c0d422322d46
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538468"
---
# <a name="spreplmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera a métrica de limite de monitoramento de uma publicação. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do publicador. *Publisher* está **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicado. *publisher_db* está **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação para o qual os atributos de limite de monitoramento estão sendo alterados. *publicação* está **sysname**, sem padrão.  
  
`[ @publication_type = ] publication_type` Se o tipo de publicação. *publication_type* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|A replicação tenta determinar o tipo de publicação.|  
  
`[ @metric_id = ] metric_id` A ID da métrica de limite da publicação está sendo alterada. *metric_id* está **int**, com um valor padrão de NULL e pode ser um destes valores.  
  
|Valor|Nome da métrica|  
|-----------|-----------------|  
|**1**|**expiration** - monitora a expiração iminente de assinaturas para publicações transacionais.|  
|**2**|**latency** - monitora o desempenho de assinaturas para publicações transacionais.|  
|**4**|**mergeexpiration** - monitora a expiração iminente de assinaturas para publicações de mesclagem.|  
|**5**|**mergeslowrunduration** -monitora a duração de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
|**6**|**mergefastrunduration** -monitora a duração de sincronizações de mesclagem em conexões de rede de área local de alta largura de banda (LAN).|  
|**7**|**mergefastrunspeed** - monitora a taxa de sincronizações de mesclagem em conexões de alta largura da banda (LAN).|  
|**8**|**mergeslowrunspeed** -monitora a taxa de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
  
 Você deve especificar *metric_id* ou *thresholdmetricname*. Se *thresholdmetricname* for especificado, então *metric_id* deve ser NULL.  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'` É o nome da métrica de limite da publicação que está sendo alterado. *thresholdmetricname* está **sysname**, com um valor padrão de NULL. Você deve especificar *thresholdmetricname* ou *metric_id*. Se *metric_id* for especificado, então *thresholdmetricname* deve ser NULL.  
  
`[ @value = ] value` É o novo valor da métrica de limite da publicação. *valor* está **int**, com um valor padrão de NULL. Se **nulo**, o valor da métrica não será atualizado.  
  
`[ @shouldalert = ] shouldalert` É se um alerta é gerado quando uma métrica de limite de publicação for atingida. *shouldalert* está **bit**, com um padrão NULL. Um valor de **1** significa que um alerta é gerado e um valor de **0** significa que um alerta não é gerado.  
  
`[ @mode = ] mode` É se a métrica de limite de publicação está habilitada. *modo* está **tinyint**, com um padrão de **1**. Um valor de **1** significa que o monitoramento dessa métrica está habilitada e um valor de **2** significa que o monitoramento dessa métrica está desabilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorchangepublicationthreshold** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição podem executar **sp_replmonitorchangepublicationthreshold**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
