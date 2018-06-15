---
title: sp_replmonitorhelppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1067d01bf7b4d510e81ac85f3e88b121b0f645e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33002793"
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações de status atual para uma ou mais publicações em um Publicador. Esse procedimento armazenado, usado para monitorar a replicação, é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publicador***'**  
 É o nome do Publicador do qual o status está sendo monitorado. *publicador* é **sysname**, com um valor padrão de NULL. Se **nulo**, as informações serão retornadas para todos os publicadores que usam o distribuidor.  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 É o nome do banco de dados publicado. *publisher_db* é **sysname**, com um valor padrão de NULL. Se for NULL, as informações serão retornadas para todos os bancos de dados publicados no Publicador.  
  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação que está sendo monitorada. *publicação* é **sysname**, com um valor padrão de NULL.  
  
 [ **@publication_type** =] *publication_type*  
 Se o tipo de publicação. *publication_type* é **int**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Publicação transacional.|  
|**1**|Publicação de instantâneo.|  
|**2**|Publicação de mesclagem.|  
|NULL (padrão)|Replicação tenta determinar o tipo de publicação.|  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Somente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|É o nome do Publicador.|  
|**Publicação**|**sysname**|É o nome de uma publicação.|  
|**publication_type**|**Int**|É o tipo de publicação, que pode ser um destes valores:<br /><br /> **0** = publicação transacional<br /><br /> **1** = publicação de instantâneo<br /><br /> **2** = publicação de mesclagem|  
|**status**|**Int**|Status máximo de todos os agentes de replicação associados com a publicação, que pode ter um destes valores.<br /><br /> **1** = iniciado<br /><br /> **2** = foi bem-sucedida<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = repetir<br /><br /> **6** = falha|  
|**Aviso**|**Int**|Aviso de limite máximo gerado por uma assinatura pertencente à publicação, que pode ser o resultado de OR lógico de um ou mais desses valores.<br /><br /> **1** = expiration – uma assinatura para uma publicação transacional não foi sincronizada dentro do limite de período de retenção.<br /><br /> **2** = latency – o tempo necessário para replicar dados de um publicador transacional para o assinante excede o limite, em segundos.<br /><br /> **4** = mergeexpiration – uma assinatura para uma publicação de mesclagem não foi sincronizada dentro do limite de período de retenção.<br /><br /> **8** = mergefastrunduration – o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede rápida.<br /><br /> **16** = mergeslowrunduration - o tempo necessário para concluir a sincronização de uma assinatura de mesclagem excede o limite, em segundos, em uma conexão de rede lenta ou discada.<br /><br /> **32** = mergefastrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa limite, em linhas por segundo, em uma conexão de rede rápida.<br /><br /> **64** = mergeslowrunspeed – a taxa de entrega de linhas durante a sincronização de uma assinatura de mesclagem não conseguiu manter a taxa limite, em linhas por segundo, em uma conexão de rede lenta ou discada.|  
|**worst_latency**|**Int**|A latência mais alta, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**best_latency**|**Int**|A latência mais baixa, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**average_latency**|**Int**|A latência média, em segundos, para alterações de dados propagadas pelo Log Reader ou Distribution Agents para uma publicação transacional.|  
|**last_distsync**|**datetime**|A última data e hora de execução do Agente de Distribuição.|  
|**retention**|**Int**|O período de retenção para a publicação.|  
|**latencythreshold**|**Int**|O limite de latência definido para a publicação transacional.|  
|**expirationthreshold**|**Int**|O limite de expiração definido para a publicação, se for uma publicação de mesclagem.|  
|**agentnotrunningthreshold**|**Int**|O limite definido para o período mais longo de não execução de um agente.|  
|**subscriptioncount**|**Int**|O número de assinaturas para uma publicação.|  
|**runningdistagentcount**|**Int**|O número de agentes de distribuição em execução para a publicação|  
|**snapshot_agentname**|**sysname**|Nome do trabalho do Agente de Instantâneo para a publicação.|  
|**logreader_agentname**|**sysname**|Nome de trabalho do Agente de Leitor de Log para a publicação transacional.|  
|**qreader_agentname**|**sysname**|Nome de trabalho do Agente de Leitor de Fila para uma publicação transacional que oferece suporte a atualização enfileirada.|  
|**worst_runspeedPerf**|**Int**|O tempo mais longo de sincronização para a publicação de mesclagem.|  
|**best_runspeedPerf**|**Int**|O tempo mais curto de sincronização para a publicação de mesclagem.|  
|**average_runspeedPerf**|**Int**|O tempo médio de sincronização para a publicação de mesclagem.|  
|**retention_period_unit**|**Int**|É a unidade usada para expressar *retenção*.|  
|**publisher**|**sysname**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está publicando a publicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorhelppublication** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **db_owner** ou **replmonitor** função de banco de dados fixa no banco de dados de distribuição pode executar **sp_replmonitorhelppublication**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
