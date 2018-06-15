---
title: sp_replmonitorchangepublicationthreshold (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bfc9b3ad0f67fa462db098a44603cc9cb1a4d586
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33001663"
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
 [ **@publisher** =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 É o nome do banco de dados publicado. *publisher_db* é **sysname**, sem padrão.  
  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação para a qual os atributos de limite de monitoramento estão sendo alterados. *publicação* é **sysname**, sem padrão.  
  
 [ **@publication_type** =] *publication_type*  
 Se o tipo de publicação. *publication_type* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|Replicação tenta determinar o tipo de publicação.|  
  
 [ **@metric_id** =] *metric_id*  
 É a ID da métrica de limite da publicação que está sendo alterada. *metric_id* é **int**, com um valor padrão de NULL e pode ser um destes valores.  
  
|Value|Nome da métrica|  
|-----------|-----------------|  
|**1**|**expiration** - monitora a expiração iminente de assinaturas para publicações transacionais.|  
|**2**|**latency** - monitora o desempenho de assinaturas para publicações transacionais.|  
|**4**|**mergeexpiration** - monitora a expiração iminente de assinaturas para publicações de mesclagem.|  
|**5**|**mergeslowrunduration** -monitora a duração de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
|**6**|**mergefastrunduration** -monitora a duração de sincronizações de mesclagem em conexões de rede de área local de alta largura de banda (LAN).|  
|**7**|**mergefastrunspeed** - monitora a taxa de sincronizações de mesclagem em conexões de alta largura da banda (LAN).|  
|**8**|**mergeslowrunspeed** -monitora a taxa de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
  
 Você deve especificar *metric_id* ou *thresholdmetricname*. Se *thresholdmetricname* for especificado, então *metric_id* deve ser NULL.  
  
 [ **@thresholdmetricname** =] **'***thresholdmetricname***'**  
 É o nome da métrica de limite da publicação que está sendo alterada. *thresholdmetricname* é **sysname**, com um valor padrão de NULL. Você deve especificar *thresholdmetricname* ou *metric_id*. Se *metric_id* for especificado, então *thresholdmetricname* deve ser NULL.  
  
 [ **@value** =] *valor*  
 É o novo valor da métrica de limite de publicação. *valor* é **int**, com um valor padrão de NULL. Se **nulo**, em seguida, o valor da métrica não é atualizado.  
  
 [ **@shouldalert** =] *shouldalert*  
 Será se um alerta for gerado quando a métrica de limite de publicação for atingida. *shouldalert* é **bit**, com um padrão NULL. Um valor de **1** significa que um alerta é gerado e um valor de **0** significa que um alerta não é gerado.  
  
 [ **@mode** =] *modo*  
 Será se a métrica de limite de publicação estiver habilitada. *modo* é **tinyint**, com um padrão de **1**. Um valor de **1** significa que o monitoramento dessa métrica está habilitada e um valor de **2** significa que o monitoramento dessa métrica está desabilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorchangepublicationthreshold** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **db_owner** ou **replmonitor** função de banco de dados fixa no banco de dados de distribuição pode executar **sp_replmonitorchangepublicationthreshold**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
