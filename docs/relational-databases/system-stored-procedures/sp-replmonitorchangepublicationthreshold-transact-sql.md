---
title: sp_replmonitorchangepublicationthreshold (T-SQL)
description: Descreve o sp_replmonitorchangepublicationthreshold procedimento armazenado que altera a métrica de limite de monitoramento para uma publicação.
ms.custom: seo-lt-2019
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6114d52b0db23d04c3b8cf001b0881dbc38844a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543146"
---
# <a name="sp_replmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera a métrica de limite de monitoramento de uma publicação. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'` É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação para a qual os atributos de limite de monitoramento estão sendo alterados. a *publicação* é **sysname**, sem padrão.  
  
`[ @publication_type = ] publication_type` Se o tipo de publicação. *publication_type* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|A replicação tenta determinar o tipo de publicação.|  
  
`[ @metric_id = ] metric_id` É a ID da métrica de limite de publicação que está sendo alterada. *metric_id* é **int**, com um valor padrão de NULL e pode ser um desses valores.  
  
|Valor|Nome da métrica|  
|-----------|-----------------|  
|**1**|**expiration** - monitora a expiração iminente de assinaturas para publicações transacionais.|  
|**2**|**latency** - monitora o desempenho de assinaturas para publicações transacionais.|  
|**4**|**mergeexpiration** - monitora a expiração iminente de assinaturas para publicações de mesclagem.|  
|**5**|**mergeslowrunduration** -monitora a duração de sincronizações de mesclagem em conexões de baixa largura de banda (discada).|  
|**6**|**mergefastrunduration** -monitora a duração das sincronizações de mesclagem em conexões de rede local (LAN) de alta largura de banda.|  
|**7**|**mergefastrunspeed** - monitora a taxa de sincronizações de mesclagem em conexões de alta largura da banda (LAN).|  
|**8**|**mergeslowrunspeed** -monitora a taxa de sincronização de sincronizações de mesclagem em conexões de baixa largura de banda (dial-up).|  
  
 Você deve especificar *metric_id* ou *thresholdmetricname*. Se *thresholdmetricname* for especificado, *METRIC_ID* deverá ser nulo.  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'` É o nome da métrica de limite de publicação que está sendo alterada. *thresholdmetricname* é **sysname**, com um valor padrão de NULL. Você deve especificar *thresholdmetricname* ou *metric_id*. Se *metric_id* for especificado, *THRESHOLDMETRICNAME* deverá ser nulo.  
  
`[ @value = ] value` É o novo valor da métrica de limite de publicação. o *valor* é **int**, com um valor padrão de NULL. Se for **NULL**, o valor da métrica não será atualizado.  
  
`[ @shouldalert = ] shouldalert` É se um alerta for gerado quando uma métrica de limite de publicação for atingida. *ShouldAlert* é **bit**, com um padrão de NULL. Um valor de **1** significa que um alerta é gerado e um valor de **0** significa que um alerta não é gerado.  
  
`[ @mode = ] mode` É se a métrica de limite de publicação estiver habilitada. o *modo* é **tinyint**, com um padrão de **1**. Um valor de **1** significa que o monitoramento dessa métrica está habilitado e um valor de **2** significa que o monitoramento dessa métrica está desabilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorchangepublicationthreshold** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **db_owner** ou **replmonitor** no banco de dados de distribuição podem executar **sp_replmonitorchangepublicationthreshold**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
