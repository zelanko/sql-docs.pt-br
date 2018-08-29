---
title: sp_replmonitorhelpmergesession (Transact-SQL) | Microsoft Docs
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
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 25bacdedf9ed9be6baa5e467cf81b809ff9cab1f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037669"
---
# <a name="spreplmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações de sessões anteriores para um determinado Merge Agent de replicação, com uma linha retornada para cada sessão correspondente aos critérios de filtragem. Esse procedimento armazenado, usado para monitorar replicação de mesclagem, é executado no Distribuidor, no banco de dados de distribuição, e no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@agent_name** =] **'***agent_name***'**  
 É o nome do agente. *agent_name* está **nvarchar(100)** sem nenhum padrão.  
  
 [ **@hours** =] *horas*  
 É o intervalo de tempo, em horas, para o qual as informações da sessão do agente são retornadas. *horas* está **int**, que pode ser um dos intervalos a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|< **0**|Retorna informações sobre execuções de agente anteriores, até um máximo de 100 execuções.|  
|**0** (padrão)|Retorna informações sobre todas as execuções de agente anteriores.|  
|> **0**|Retorna informações sobre o agente de execuções que ocorreram nas últimas *horas* número de horas.|  
  
 [ **@session_type** =] *session_type*  
 Filtra o conjunto de resultados baseado no resultado final da sessão. *session_type* está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (padrão)|Sessões de agente com um resultado de repetição ou êxito.|  
|**0**|Sessões de agente com um resultado de falha.|  
  
 [ **@publisher** =] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, com um padrão NULL. Esse parâmetro é usado ao executar **sp_replmonitorhelpmergesession** no assinante.  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* está **sysname**, com um padrão NULL. Esse parâmetro é usado ao executar **sp_replmonitorhelpmergesession** no assinante.  
  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, com um padrão NULL. Esse parâmetro é usado ao executar **sp_replmonitorhelpmergesession** no assinante.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|ID da sessão de trabalho do agente.|  
|**Status**|**int**|Status de execução do agente:<br /><br /> **1** = início<br /><br /> **2** = êxito<br /><br /> **3** = em andamento<br /><br /> **4** = ocioso<br /><br /> **5** = repetir<br /><br /> **6** = falha|  
|**StartTime**|**datetime**|Começou a sessão de trabalho do agente de tempo.|  
|**EndTime**|**datetime**|Sessão de trabalho do agente de tempo foi concluída.|  
|**Duration**|**int**|Duração acumulada, em segundos, dessa sessão de trabalho.|  
|**UploadedCommands**|**int**|Número de comandos carrgeado durante a sessão do agente.|  
|**DownloadedCommands**|**int**|Número de comandos baixados durante a sessão do agente.|  
|**ErrorMessages**|**int**|Número de mensagens de erro geradas durante a sessão do agente.|  
|**Identificação de erro**|**int**|ID do erro ocorrido.|  
|**PercentageDone**|**decimal**|Porcentagem estimada do total de alterações que já foi entregue em uma sessão ativa.|  
|**TimeRemaining**|**int**|Número estimado de segundos restantes em uma sessão ativa.|  
|**CurrentPhase**|**int**|É a fase atual da sessão de uma sessão ativa, que pode ser uma das seguintes:<br /><br /> **1** = carregamento<br /><br /> **2** = download|  
|**LastMessage**|**nvarchar(500)**|É a última mensagem registrada pelo Merge Agent durante a sessão.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorhelpmergesession** é usado para monitorar a replicação de mesclagem.  
  
 Quando executado no assinante, **sp_replmonitorhelpmergesession** só retorna informações sobre as últimas cinco sessões do Merge Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **db_owner** ou **replmonitor** banco de dados fixa no banco de dados de distribuição no distribuidor ou no banco de dados de assinatura no assinante podem executar **SP _ replmonitorhelpmergesession**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
