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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ac45c3b25e1a13366ae273b8d21d7e41e768251
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748299"
---
# <a name="spreplmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações de status atuais para assinaturas pertencentes a uma ou mais publicações no Publicador e retorna uma linha para cada assinatura retornada. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publisher** =] **'***publisher***'**  
 É o nome do Publicador do qual o status está sendo monitorado. *Publisher* está **sysname**, com um valor padrão de NULL. Se **nulo**, informações serão retornadas para todos os publicadores que usam o distribuidor.  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 É o nome do banco de dados publicado. *publisher_db* está **sysname**, com um valor padrão de NULL. Se for NULL, as informações serão retornadas para todos os bancos de dados publicados no Publicador.  
  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação que está sendo monitorada. *publicação* está **sysname**, com um valor padrão de NULL.  
  
 [ **@publication_type** =] *publication_type*  
 Se o tipo de publicação. *publication_type* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|A replicação tenta determinar o tipo de publicação.|  
  
 [ **@mode** =] *modo*  
 É o modo de filtragem a ser usado ao retornar informações de monitoramento de assinatura. *modo* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Retorna todas as assinaturas.|  
|**1**|Retorna somente assinaturas com erros.|  
|**2**|Retorna somente assinaturas que geraram avisos de métrica de limite.|  
|**3**|Retorna somente assinaturas que têm erros ou geraram avisos de métrica de limite.|  
|**4**|Retorna as 25 principais assinaturas de pior desempenho.|  
|**5**|Retorna as 50 assinaturas com os piores desempenhos.|  
|**6**|Retorna somente assinaturas que estão sendo atualmente sincronizadas.|  
|**7**|Retorna somente assinaturas que não estão sendo atualmente sincronizadas.|  
  
 [ **@topnum** =] *topnum*  
 Restringe o conjunto de resultados a apenas o número especificado de assinaturas no topo dos dados retornados. *topnum* está **int**, sem padrão.  
  
 [ **@exclude_anonymous** =] *exclude_anonymous*  
 Especifica se assinaturas pull anônimas serão excluídas do conjunto de resultados. *exclude_anonymous* está **bit**, com um padrão de **0**; um valor de **1** significa que as assinaturas anônimas serão excluídas e um valor de **0**  significa que eles são incluídos.  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**status**|**int**|Verifica o status de todos os agentes de replicação associados com a publicação e retorna o status mais alto encontrado na seguinte ordem:<br /><br /> **6** = falha<br /><br /> **5** = tentando novamente<br /><br /> **2** = parado<br /><br /> **4** = ocioso<br /><br /> **3** = em andamento<br /><br /> **1** = iniciado|  
|**Aviso**|**int**|Aviso de limite máximo gerado por uma assinatura pertencente à publicação, que pode ser o resultado de OR lógico de um ou mais desses valores.<br /><br /> **1** = expiration – uma assinatura para uma publicação transacional não foi sincronizada dentro do limite de período de retenção.<br /><br /> **2** = latency – o tempo necessário para replicar dados de um publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration – uma assinatura para uma publicação de mesclagem não foi sincronizada dentro do limite de período de retenção.<br /><br /> **8** = mergefastrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration - o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem falhou em manter a taxa de limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem falhou em manter a taxa de limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**Assinante**|**sysname**|É o nome do Assinante.|  
|**subscriber_db**|**sysname**|É o nome do banco de dados usado para a assinatura.|  
|**publisher_db**|**sysname**|É o nome do banco de dados de publicação.|  
|**publicação**|**sysname**|É o nome de uma publicação.|  
|**publication_type**|**int**|É o tipo de publicação, que pode ser um destes valores:<br /><br /> **0** = publicação transacional<br /><br /> **1** = publicação de instantâneo<br /><br /> **2** = publicação de mesclagem|  
|**subtipo**|**int**|É o tipo de assinatura, que pode ter um dos seguintes valores:<br /><br /> **0** = push<br /><br /> **1** = pull<br /><br /> **2** = anônimo|  
|**latência**|**int**|A latência mais alta, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
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
|**mergeconnectiontype**|**int**|Conexão usada ao sincronizar uma assinatura a uma publicação de mesclagem, que pode ser um dos seguintes valores:<br /><br /> **1** = rede local (LAN)<br /><br /> **2** = conexão de rede dial-up<br /><br /> **3** = sincronização da web.|  
|**mergePerformance**|**int**|Desempenho da última sincronização comparada com todas as sincronizações à assinatura, com base na taxa de entrega da última sincronização dividida pela média de todas as taxas de entrega anteriores.|  
|**mergerunspeed**|**float**|É a taxa de entrega da última sincronização da assinatura.|  
|**mergerunduration**|**int**|É a quantidade de tempo para concluir a última sincronização da assinatura.|  
|**monitorranking**|**int**|É o valor de classificação usado para ordenar as assinaturas no conjunto de resultados, e pode ter um destes valores:<br /><br /> Para uma publicação transacional:<br /><br /> **60** = erro<br /><br /> **56** = Aviso: desempenho crítico<br /><br /> **52** = Aviso: expirando logo ou expirado<br /><br /> **50** = Aviso: assinatura não inicializada<br /><br /> **40** = repetindo comando com falha<br /><br /> **30** = não está em execução (êxito)<br /><br /> **20** = executando (iniciando, executando ou ocioso)<br /><br /> Para uma publicação de mesclagem:<br /><br /> **60** = erro<br /><br /> **56** = Aviso: desempenho crítico<br /><br /> **54** = Aviso: mesclagem de execução longa<br /><br /> **52** = Aviso: expirando em breve<br /><br /> **50** = Aviso: assinatura não inicializada<br /><br /> **40** = repetindo comando com falha<br /><br /> **30** = executando (iniciando, executando ou ocioso)<br /><br /> **20** = não está em execução (êxito)|  
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
  
 **sp_replmonitorhelpsubscription** ordena o conjunto de resultados com base na gravidade do status da assinatura, que é determinado pelo valor da *monitorranking*. Por exemplo, linhas para todas as assinaturas em estado de erro são ordenadas acima das linhas de assinatura em estado de aviso.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição podem executar **sp_replmonitorhelpsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
