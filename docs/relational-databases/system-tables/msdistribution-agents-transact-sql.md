---
title: MSdistribution_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 357d0cf774d3e95d700c840f88bb0165bdb9a12f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817124"
---
# <a name="msdistributionagents-transact-sql"></a>MSdistribution_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdistribution_agents** tabela contém uma linha para cada agente de distribuição em execução no distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do Distribution Agent.|  
|**name**|**nvarchar(100)**|O nome do Distribution Agent.|  
|**publisher_database_id**|**int**|A ID do banco de dados Publicador.|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publication**|**sysname**|O nome da publicação.|  
|**subscriber_id**|**smallint**|A ID do Assinante, só usada por agentes conhecidos. Para agentes anônimos, essa coluna é reservada.|  
|**subscriber_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push.<br /><br /> **1** = Pull.<br /><br /> **2** = anônimo.|  
|**local_job**|**bit**|Indica se há um trabalho do SQL Server Agent no distribuidor local.|  
|**job_id**|**binary(16)**|O número de identificação do trabalho.|  
|**subscription_guid**|**binary(16)**|A ID de assinaturas desse agente.|  
|**profile_id**|**int**|A ID de configuração a partir de [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabela.|  
|**anonymous_subid**|**uniqueidentifier**|A ID de um agente anônimo.|  
|**subscriber_name**|**sysname**|O nome do Assinante, só usada por agentes anônimos.|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|A data e hora de criação do Distribution ou Merge Agent.|  
|**queue_id**|**sysname**|O identificador para localizar a fila de assinaturas de atualização enfileiradas. Para assinaturas que não estão em fila, o valor é NULL. Para publicações com base no serviço de enfileiramento de mensagens da [!INCLUDE[msCoName](../../includes/msconame-md.md)], o valor é um GUID que identifica com exclusividade a fila a ser usada na assinatura. Para publicações de fila com base no SQL Server, a coluna contém o valor **SQL**.<br /><br /> Observação: Usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens foi preterido e não é mais suportado.|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|Indica se o agente pode ser ativado remotamente.<br /><br /> **0** Especifica que o agente não pode ser ativado remotamente.<br /><br /> **1** Especifica que o agente será ativado remotamente e no computador remoto especificado em de *offload_server* propriedade.|  
|**offload_server**|**sysname**|O nome da rede de servidor a ser usado para ativação de agente remota.|  
|**dts_package_name**|**sysname**|O nome do pacote DTS. Por exemplo, para um pacote denominado **DTSPub_Package**, especifique `@dts_package_name = N'DTSPub_Package'`.|  
|**dts_package_password**|**nvarchar(524)**|A senha no pacote.|  
|**dts_package_location**|**int**|O local do pacote. O local do pacote pode ser **distribuidor** ou **assinante**.|  
|**sid**|**varbinary(85)**|O SID (número de identificação de segurança) para o Distribution Agent ou Merge Agent durante sua primeira execução.|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Assinante que pode ser um dos seguintes:<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server Authentication<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
|**subscriber_login**|**sysname**|O logon usado na conexão com o Assinante.|  
|**subscriber_password**|**nvarchar(524)**|É o valor criptografado da senha usada na conexão com o Assinante.|  
|**reset_partial_snapshot_progress**|**bit**|Se um instantâneo parcialmente baixado for cancelado, todo o processo de instantâneo poderá começar novamente.|  
|**job_step_uid**|**uniqueidentifier**|A ID exclusiva do trabalho do SQL Server Agent etapa na qual o agente é iniciado.|  
|**subscriptionstreams**|**tinyint**|Define o número de conexões permitido por Distribution Agent para aplicar lotes de alterações em paralelo a um Assinante. Há suporte para um intervalo de valores de 1 a 64.|  
|**memory_optimized**|**bit**|1 indica que o assinante pode ser usado para tabelas com otimização de memória.|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar(524)**||  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
