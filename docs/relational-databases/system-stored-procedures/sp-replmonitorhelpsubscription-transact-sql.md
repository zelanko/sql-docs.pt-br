---
title: sp_replmonitorhelpsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords:
- sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c3eaaeb7715086bf5b411a016239bb24d147fcda
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82817241"
---
# <a name="sp_replmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna informações de status atuais para assinaturas pertencentes a uma ou mais publicações no Publicador e retorna uma linha para cada assinatura retornada. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador cujo status está sendo monitorado. o *Publicador* é **sysname**, com um valor padrão de NULL. Se for **NULL**, as informações serão retornadas para todos os Publicadores que usam o distribuidor.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados publicado. *publisher_db* é **sysname**, com um valor padrão de NULL. Se for NULL, as informações serão retornadas para todos os bancos de dados publicados no Publicador.  
  
`[ @publication = ] 'publication'`É o nome da publicação que está sendo monitorada. a *publicação* é **sysname**, com um valor padrão de NULL.  
  
`[ @publication_type = ] publication_type`Se o tipo de publicação. *publication_type* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|A replicação tenta determinar o tipo de publicação.|  
  
`[ @mode = ] mode`É o modo de filtragem a ser usado ao retornar informações de monitoramento de assinatura. o *modo* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Retorna todas as assinaturas.|  
|**1**|Retorna somente assinaturas com erros.|  
|**2**|Retorna somente assinaturas que geraram avisos de métrica de limite.|  
|**3**|Retorna somente assinaturas que têm erros ou geraram avisos de métrica de limite.|  
|**4**|Retorna as 25 assinaturas com pior desempenho.|  
|**5**|Retorna as 50 assinaturas com os piores desempenhos.|  
|**6**|Retorna somente assinaturas que estão sendo atualmente sincronizadas.|  
|**7**|Retorna somente assinaturas que não estão sendo atualmente sincronizadas.|  
  
`[ @topnum = ] topnum`Restringe o conjunto de resultados para apenas o número especificado de assinaturas na parte superior dos dados retornados. *topnum* é **int**, sem padrão.  
  
`[ @exclude_anonymous = ] exclude_anonymous`Se as assinaturas pull anônimas forem excluídas do conjunto de resultados. *exclude_anonymous* é **bit**, com um padrão de **0**; um valor de **1** significa que as assinaturas anônimas são excluídas e o valor **0** significa que elas estão incluídas.  
  
`[ @refreshpolicy = ] refreshpolicy`Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**status**|**int**|Verifica o status de todos os agentes de replicação associados com a publicação e retorna o status mais alto encontrado na seguinte ordem:<br /><br /> **6** = com falha<br /><br /> **5** = repetindo<br /><br /> **2** = parado<br /><br /> **4** = ocioso<br /><br /> **3** = em andamento<br /><br /> **1** = iniciado|  
|**alerta**|**int**|Aviso de limite máximo gerado por uma assinatura pertencente à publicação, que pode ser o resultado de OR lógico de um ou mais desses valores.<br /><br /> **1** = expiração-uma assinatura para uma publicação transacional não foi sincronizada dentro do limite do período de retenção.<br /><br /> **2** = latência-o tempo necessário para replicar dados de um Publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration-uma assinatura para uma publicação de mesclagem não foi sincronizada dentro do limite do período de retenção.<br /><br /> **8** = mergefastrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration-o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed-a taxa de entrega para linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**farão**|**sysname**|É o nome do Assinante.|  
|**subscriber_db**|**sysname**|É o nome do banco de dados usado para a assinatura.|  
|**publisher_db**|**sysname**|É o nome do banco de dados de publicação.|  
|**documento**|**sysname**|É o nome de uma publicação.|  
|**publication_type**|**int**|É o tipo de publicação, que pode ser um destes valores:<br /><br /> **0** = publicação transacional<br /><br /> **1** = publicação de instantâneo<br /><br /> **2** = publicação de mesclagem|  
|**subtype**|**int**|É o tipo de assinatura, que pode ter um dos seguintes valores:<br /><br /> **0** = enviar por push<br /><br /> **1** = pull<br /><br /> **2** = anônimo|  
|**MOLAP**|**int**|A latência mais alta, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**latencythreshold**|**int**|É a latência máxima para a publicação transacional acima da qual uma advertência será gerada.|  
|**agentnotrunning**|**int**|É a quantidade de tempo, em horas, durante a qual o agente não executou.|  
|**agentnotrunningthreshold**|**int**|É a quantidade de tempo, em horas, em que o agente não executou, antes que um aviso fosse gerado.|  
|**timetoexpiration**|**int**|É a quantidade de tempo, em horas, antes que a assinatura expire, se não estiver sincronizada.|  
|**expirationthreshold**|**int**|É o tempo, em horas, antes que a assinatura expire e um aviso seja gerado.|  
|**last_distsync**|**datetime**|A data e hora da última execução do Distribution Agent.|  
|**distribution_agentname**|**sysname**|É o nome de trabalho do Distribution Agent para a assinatura em uma publicação transacional.|  
|**mergeagentname**|**sysname**|É o nome de trabalho do Merge Agent para a assinatura em uma publicação de mesclagem.|  
|**mergesubscriptionfriendlyname**|**sysname**|É o nome amigável dado à assinatura.|  
|**mergeagentlocation**|**sysname**|É o nome do servidor no qual o Merge Agent é executado.|  
|**mergeconnectiontype**|**int**|Conexão usada ao sincronizar uma assinatura a uma publicação de mesclagem, que pode ser um dos seguintes valores:<br /><br /> **1** = rede local (LAN)<br /><br /> **2** = conexão de rede dial-up<br /><br /> **3** = sincronização da Web.|  
|**mergePerformance**|**int**|Desempenho da última sincronização comparada com todas as sincronizações à assinatura, com base na taxa de entrega da última sincronização dividida pela média de todas as taxas de entrega anteriores.|  
|**mergerunspeed**|**float**|É a taxa de entrega da última sincronização da assinatura.|  
|**mergerunduration**|**int**|É a quantidade de tempo para concluir a última sincronização da assinatura.|  
|**monitorranking**|**int**|É o valor de classificação usado para ordenar as assinaturas no conjunto de resultados, e pode ter um destes valores:<br /><br /> Para uma publicação transacional:<br /><br /> **60** = erro<br /><br /> **56** = aviso: desempenho crítico<br /><br /> **52** = aviso: Expirando em breve ou expirado<br /><br /> **50** = aviso: assinatura não inicializada<br /><br /> **40** = repetindo comando com falha<br /><br /> **30** = não está em execução (êxito)<br /><br /> **20** = em execução (iniciando, em execução ou ocioso)<br /><br /> Para uma publicação de mesclagem:<br /><br /> **60** = erro<br /><br /> **56** = aviso: desempenho crítico<br /><br /> **54** = aviso: mesclagem de execução longa<br /><br /> **52** = aviso: Expirando em breve<br /><br /> **50** = aviso: assinatura não inicializada<br /><br /> **40** = repetindo comando com falha<br /><br /> **30** = em execução (iniciando, em execução ou ocioso)<br /><br /> **20** = não está em execução (êxito)|  
|**distributionagentjobid**|**binary(16)**|ID de trabalho do Distribution Agent para assinaturas em uma publicação transacional.|  
|**mergeagentjobid**|**binary(16)**|ID de trabalho do Merge Agent para assinaturas em uma publicação de mesclagem.|  
|**distributionagentid**|**int**|ID de trabalho do Distribution Agent para a assinatura.|  
|**distributionagentprofileid**|**int**|ID do perfil de agente usado pelo Distribution Agent.|  
|**mergeagentid**|**int**|ID de trabalho do Merge Agent para a assinatura.|  
|**mergeagentprofileid**|**int**|ID do perfil de agente usado pelo Merge Agent.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replmonitorhelpsubscription** é usado com todos os tipos de replicação.  
  
 **sp_replmonitorhelpsubscription** ordena o conjunto de resultados com base na severidade do status da assinatura, que é determinado pelo valor de *monitorranking*. Por exemplo, linhas para todas as assinaturas em estado de erro são ordenadas acima das linhas de assinatura em estado de aviso.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **db_owner** ou **replmonitor** no banco de dados de distribuição podem executar **sp_replmonitorhelpsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar a replicação de forma programática](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
