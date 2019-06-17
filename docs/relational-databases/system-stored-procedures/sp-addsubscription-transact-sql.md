---
title: sp_addsubscription (Transact-SQL) | Microsoft Docs
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscription
- sp_addsubscription_TSQL
helpviewer_keywords:
- sp_addsubscription
ms.assetid: 61ddf287-1fa0-4c1a-8657-ced50cebf0e0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a0064787eee6c3ac267b3ababcd9881e794ff2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998304"
---
# <a name="spaddsubscription-transact-sql"></a>sp_addsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma assinatura a uma publicação e define o status do Assinante. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addsubscription [ @publication = ] 'publication'  
    [ , [ @article = ] 'article']  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
        [ , [ @sync_type = ] 'sync_type' ]  
    [ , [ @status = ] 'status'  
        [ , [ @subscription_type = ] 'subscription_type' ]  
    [ , [ @update_mode = ] 'update_mode' ]  
    [ , [ @loopback_detection = ] 'loopback_detection' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
    [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @backupdevicetype = ] 'backupdevicetype' ]  
    [ , [ @backupdevicename = ] 'backupdevicename' ]  
    [ , [ @mediapassword = ] 'mediapassword' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @fileidhint = ] fileidhint ]  
    [ , [ @unload = ] unload ]  
    [ , [ @subscriptionlsn = ] subscriptionlsn ]  
    [ , [ @subscriptionstreams = ] subscriptionstreams ]  
    [ , [ @subscriber_type = ] subscriber_type ]  
    [ , [ @memory_optimized = ] memory_optimized ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication=] '*publication*'  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [ @article=] '*article*'  
 É o artigo no qual a publicação é assinada. *artigo* está **sysname**, com um padrão de all. Se for todos, uma assinatura será adicionada a todos os artigos naquela publicação. Somente valores de todos ou NULL têm suporte para Publicadores Oracle.  
  
 [ @subscriber=] '*subscriber*'  
 É o nome do Assinante. *assinante* está **sysname**, com um padrão NULL.  
  
 [ @destination_db=] '*destination_db*'  
 É o nome do banco de dados de destino no qual os dados replicados são colocados. *destination_db* está **sysname**, com um padrão NULL. Quando NULL, *destination_db* é definido como o nome do banco de dados de publicação. For Oracle Publishers *destination_db* deve ser especificado. Para um assinante não SQL Server, especifique um valor de (destino padrão) para *destination_db*.  
  
 [ @sync_type=] '*sync_type*'  
 É o tipo de sincronização da assinatura. *sync_type* está **nvarchar (255)** , e pode ser um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|none|O Assinante já tem o esquema e os dados iniciais para as tabelas publicadas.<br /><br /> Observação: Essa opção foi preterida. Use, em vez disso, suporte a replicação.|  
|automatic (padrão)|Esquema e dados iniciais de tabelas publicadas são transferidos ao Assinante primeiro.|  
|suporte de replicação só|Fornece geração automática no Assinante de procedimentos armazenados personalizados de artigo e gatilhos que oferecem suporte a assinaturas de atualização, se apropriado. Presume que o Assinante já tem o esquema e os dados iniciais para as tabelas publicadas. Ao configurar uma topologia de replicação transacional ponto a ponto, verifique se os dados em todos os nós na topologia são idênticos. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).<br /><br /> *Não tem suporte para assinaturas para publicações não SQL Server.*|  
|initialize with backup|Esquema e dados iniciais para tabelas publicadas são obtidos de um backup do banco de dados de publicação. Presume que o Assinante tem acesso a um backup do banco de dados de publicação. O local do tipo de backup e mídia para o backup são especificadas por *backupdevicename* e *backupdevicetype*. Ao usar essa opção, uma topologia de replicação transacional ponto a ponto não precisa ser desativada durante a configuração.<br /><br /> *Não tem suporte para assinaturas para publicações não SQL Server.*|  
|initialize from lsn|Usado quando você está adicionando um nó a uma topologia de replicação transacional ponto a ponto. Usado com @subscriptionlsn para garantir que todas as transações relevantes são replicadas para o novo nó. Presume que o Assinante já tem o esquema e os dados iniciais para as tabelas publicadas. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
> [!NOTE]  
>  Tabelas de sistema e dados sempre são transferidos.  
  
 [ @status=] '*status*'  
 E o status da assinatura. *status* está **sysname**, com um valor padrão de NULL. Quando esse parâmetro não é definido explicitamente, a replicação o define automaticamente para um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|active|A assinatura é inicializada e está pronta para oferecer suporte a alterações. Essa opção é definida quando o valor de *sync_type* é none, inicializar com backup ou suporte para replicação somente.|  
|subscribed|A assinatura precisa ser inicializada. Essa opção é definida quando o valor de *sync_type* é automática.|  
  
 [ @subscription_type=] '*subscription_type*'  
 É o tipo de assinatura. *subscription_type* está **nvarchar(4)** , com um padrão push. Pode ser push ou pull. Os Distribution Agents de assinaturas push residem no distribuidor e os Distribution Agents de assinaturas pull residem no assinante. *subscription_type* pode ser pull para criar uma assinatura pull nomeada conhecida do publicador. Para obter mais informações, consulte [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md) (Assinar publicações).  
  
> [!NOTE]  
>  Assinaturas anônimas não precisam usar esse procedimento armazenado.  
  
 [ @update_mode=] '*update_mode*'  
 É o tipo de atualização. *update_mode* é **nvarchar (30)** , e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|read only (padrão)|A assinatura é somente leitura. Qualquer alteração no Assinante não será mandada ao Publicador.|  
|sync tran|Habilita suporte para assinaturas de atualização imediata. Sem suporte para Publicadores Oracle.|  
|queued tran|Habilita a assinatura de atualização enfileirada. As modificações de dados podem ser feitas no Assinante, armazenadas em uma fila e, depois, propagadas ao Publicador. Sem suporte para Publicadores Oracle.|  
|failover|Habilita a assinatura para atualização imediata com atualização enfileirada como um failover. Modificações de dados podem ser feitas no Assinante e propagadas ao Publicador imediatamente. Se o Publicador e o Assinante não estiverem conectados, o mo do de atualização pode ser alterado para que as modificações de dados feitas no Assinante sejam armazenadas em uma fila até que o Assinante e o Publicador sejam reconectados. Sem suporte para Publicadores Oracle.|  
|queued failover|Habilita a assinatura como uma assinatura de atualização enfileirada com a capacidade de alterar para o modo de atualização imediata. Modificações de dados podem ser feitas no Assinante e armazenadas em uma fila até que a conexão seja estabelecida entre o Assinante e o Publicador. Quando uma conexão contínua é estabelecida, o modo de atualização pode ser alterado para atualização imediata. Sem suporte para Publicadores Oracle.|  
  
 Observe que os valores synctran e queued tran não permitida se a publicação que está sendo assinada permite DTS.  
  
 [ @loopback_detection=] '*loopback_detection*'  
 Especifica se o Agente de Distribuição envia transações originadas no Assinante de volta ao Assinante. *loopback_detection* está **nvarchar (5)** , e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|true|O Distribution Agent não envia transações originadas no Assinante de volta ao Assinante. Usado com replicação transacional bidirecional. Para obter mais informações, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|false|O Distribution Agent envia transações originadas no Assinante de volta ao Assinante.|  
|NULL (padrão)|Automaticamente definido como verdadeiro para um Assinante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e falso para um assinante não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 [ @frequency_type=] *frequency_type*  
 É a frequência de agendamento da tarefa de distribuição. *frequency_type* é int, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|1|Uma vez|  
|2|Sob Demanda|  
|4|Diariamente|  
|8|Semanalmente|  
|16|Mensalmente|  
|32|Relativo ao mês|  
|64 (padrão)|Iniciar automaticamente|  
|128|Recorrente|  
  
 [ @frequency_interval=] *frequency_interval*  
 É o valor a ser aplicado à frequência definida *frequency_type*. *frequency_interval* está **int**, com um padrão NULL.  
  
 [ @frequency_relative_interval=] *frequency_relative_interval*  
 É a data do Distribution Agent. Esse parâmetro é usado quando *frequency_type* é definido como 32 (mensal relativo). *frequency_relative_interval* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|1|First|  
|2|Segundo|  
|4|Terceiro|  
|8|Quarto|  
|16|Last|  
|NULL (padrão)||  
  
 [ @frequency_recurrence_factor=] *frequency_recurrence_factor*  
 É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* está **int**, com um padrão NULL.  
  
 [ @frequency_subday=] *frequency_subday*  
 É a frequência, em minutos, de reagendamento durante o período definido. *frequency_subday* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|1|Uma vez|  
|2|Segundo|  
|4|Minuto|  
|8|Hora|  
|NULL||  
  
 [ @frequency_subday_interval=] *frequency_subday_interval*  
 É o intervalo de *frequency_subday*. *frequency_subday_interval* está **int**, com um padrão NULL.  
  
 [ @active_start_time_of_day=] *active_start_time_of_day*  
 É a hora do dia do primeiro agendamento do Agente de Distribuição, formatada como HHMMSS. *active_start_time_of_day* está **int**, com um padrão NULL.  
  
 [ @active_end_time_of_day=] *active_end_time_of_day*  
 É a hora do dia do último agendamento do Agente de Distribuição, formatada como HHMMSS. *active_end_time_of_day* está **int**, com um padrão NULL.  
  
 [ @active_start_date=] *active_start_date*  
 É a data do primeiro agendamento do Agente de Distribuição, formatada como AAAAMMDD. *active_start_date* está **int**, com um padrão NULL.  
  
 [ @active_end_date=] *active_end_date*  
 É a data do último agendamento do Agente de Distribuição, formatada como AAAAMMDD. *active_end_date* está **int**, com um padrão NULL.  
  
 [ @optional_command_line=] '*optional_command_line*'  
 É o prompt de comando opcional a ser executado. *optional_command_line* está **nvarchar (4000)** , com um padrão NULL.  
  
 [ @reserved=] '*reserved*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @enabled_for_syncmgr=] '*enabled_for_syncmgr*'  
 Se a assinatura pode ser sincronizada pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gerenciador de sincronização do Windows. *enabled_for_syncmgr* está **nvarchar (5)** , com um padrão de FALSE. Se for falso, a assinatura não será registrada com o Gerenciador de Sincronização do Windows. Se for verdadeiro, a assinatura será registrada com o Gerenciador de Sincronização do Windows e será sincronizada sem iniciar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Sem suporte para Publicadores Oracle.  
  
 [ @offloadagent= ] '*remote_agent_activation*'  
 Especifica que o agente pode ser ativado remotamente. *remote_agent_activation* está **bit** com um padrão de 0.  
  
> [!NOTE]  
>  Esse parâmetro foi preterido e só é mantido para compatibilidade com versões anteriores.  
  
 [ @offloadserver= ] '*remote_agent_server_name*'  
 Especifica o nome da rede de servidor a ser usada para ativação remota. *remote_agent_server_name*está **sysname**, com um padrão NULL.  
  
 [ @dts_package_name= ] '*dts_package_name*'  
 Especifica o nome do pacote DTS (Data Transformation Services). *dts_package_name* é um **sysname** com um padrão NULL. Por exemplo, para especificar um nome de pacote DTSPub_Package, o parâmetro seria `@dts_package_name = N'DTSPub_Package'`. Esse parâmetro está disponível para assinaturas push. Para adicionar informações de pacote DTS a uma assinatura pull, use sp_addpullsubscription_agent.  
  
 [ @dts_package_password= ] '*dts_package_password*'  
 Especifica a senha no pacote, se houver um. *dts_package_password* está **sysname** com um padrão NULL.  
  
> [!NOTE]  
>  Você deve especificar uma senha se *dts_package_name* for especificado.  
  
 [ @dts_package_location= ] '*dts_package_location*'  
 Especifica o local do pacote. *dts_package_location* é um **nvarchar(12**, com um padrão de DISTRIBUIDOR. O local do pacote pode ser distribuidor ou assinante.  
  
 [ @distribution_job_name= ] '*distribution_job_name*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @publisher= ] '*publisher*'  
 Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser especificado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
 [ @backupdevicetype=] '*backupdevicetype*'  
 Especifica o tipo do dispositivo de backup a ser usado ao inicializar um Assinante de um backup. *backupdevicetype* está **nvarchar (20)** , e pode ser um destes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|logical (padrão)|O dispositivo de backup é um dispositivo lógico.|  
|disk|O dispositivo de backup é uma unidade de disco.|  
|tape|O dispositivo de backup é uma unidade de fita.|  
  
 *backupdevicetype* é usado apenas quando *sync_method*é definido para initialize_with_backup.  
  
 [ @backupdevicename=] '*backupdevicename*'  
 Especifica o nome do dispositivo usado ao inicializar um Assinante em um backup. *backupdevicename* está **nvarchar (1000)** , com um padrão NULL.  
  
 [ @mediapassword=] '*mediapassword*'  
 Especifica uma senha para o conjunto de mídias se uma senha já tiver sido definida quando a mídia foi formatada. *mediapassword* está **sysname**, com um valor padrão de NULL.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [ @password=] '*senha*'  
 Especifica uma senha para o backup se uma senha já tiver sido definida quando o backup foi criado. *senha*está **sysname**, com um valor padrão de NULL.  
  
 [ @fileidhint= ] *fileidhint*  
 Identifica um valor ordinal do conjunto de backup a ser restaurado. *fileidhint* está **int**, com um valor padrão de NULL.  
  
 [ @unload= ] *unload*  
 Especifica se um dispositivo de backup em fita deve ser descarregado quando a inicialização do backup for concluída. *Descarregar* está **bit**, com um valor padrão de 1. 1 Especifica que a fita deve ser descarregada. *Descarregar* é usado apenas quando *backupdevicetype* é fita.  
  
 [ @subscriptionlsn=] *subscriptionlsn*  
 Especifica o LSN (número de sequência de log) no qual uma assinatura deve começar a entrega de alterações para um nó, em uma topologia de replicação transacional ponto a ponto. Usado com um @sync_type valor de inicialização do lsn para certificar-se de que todas as transações relevantes sejam replicadas para um novo nó. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [ @subscriptionstreams=] *subscriptionstreams*  
 É o número de conexões permitido por Agente de Distribuição para aplicar lotes de alterações em paralelo a um Assinante, mantendo muitas das características transacionais presentes ao usar um thread único. *subscriptionstreams* está **tinyint**, com um valor padrão de NULL. Há suporte para um intervalo de valores de 1 a 64. Não há suporte para esse parâmetro para não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes, Publicadores Oracle ou assinaturas ponto a ponto. Sempre que fluxos de assinatura são usados, linhas adicionais são acrescentadas à tabela msreplication_subscriptions (1 por fluxo) com um agent_id definido como NULL.  
  
> [!NOTE]  
>  Fluxos de assinatura não funcionam em artigos configurados para entrega [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para usar fluxos de assinatura, configure os artigos para entregar chamadas de procedimento armazenado.  
  
 [ @subscriber_type=] *subscriber_type*  
 É o tipo de assinante. *subscriber_type* está **tinyint**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0 (padrão)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante|  
|1|Servidor de fontes de dados ODBC|  
|2|Banco de dados [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet|  
|3|Provedor OLE DB|  
  
 [ @memory_optimized=] *memory_optimized*  
 Indica que a assinatura dá suporte a tabelas com otimização de memória. *memory_optimized* está **bit**, onde 1 é igual a true (a assinatura dá suporte a tabelas com otimização de memória).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_addsubscription é usado em replicação de instantâneo e replicação transacional.  
  
 Quando sp_addsubscription é executado por um membro da função de servidor fixa sysadmin para criar uma assinatura push, o trabalho do Distribution Agent é implicitamente criado e executado na conta de serviço do SQL Server Agent. Recomendamos que você execute [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) e especifique as credenciais da conta diferente, específica de agente do Windows para @job_login e @job_password. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 sp_addsubscription impede que Assinantes ODBC e OLE DB acessem publicações que:  
  
-   Foram criados com o native *sync_method* na chamada para [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
-   Contêm artigos que foram adicionados à publicação com o [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) procedimento armazenado que tinha um *pre_creation_cmd* valor do parâmetro de 3 (truncado).  
  
-   Tentativa de definir *update_mode* como sync tran.  
  
-   Têm um artigo configurado para usar instruções com parâmetros.  
  
 Além disso, se uma publicação com o *allow_queued_tran* opção definido como true (o que permite que o enfileiramento de alterações no assinante até que elas podem ser aplicadas no publicador), a coluna de carimbo de hora em um artigo é criada como **carimbo de hora**, e as alterações nessa coluna são enviadas ao assinante. O Assinante gera e atualiza o valor da coluna de carimbo de hora. Para um assinante ODBC ou OLE DB, sp_addsubscription falhará se uma tentativa for feita para assinar uma publicação que tem *allow_queued_tran* definida como true e artigos com colunas de carimbo de hora.  
  
 Se uma assinatura não usar um pacote DTS, ela não poderá assinar uma publicação que está definida como *allow_transformable_subscriptions*. Se a tabela da publicação precisar ser replicada para uma assinatura DTS e uma assinatura não DTS, deverão ser criadas duas publicações separadas, uma para cada tipo de assinatura.  
  
 Ao selecionar as opções de **sync_type** , *replication support only*, *initialize with backup*, ou *initialize from lsn*, o Agente de Leitor de Log deve ser executado após a execução de **sp_addsubscription**, para que os scripts configurados sejam gravados no banco de dados de distribuição. O Agente de Leitor de Log deve ser executado sob uma conta que seja membro da função de servidor fixa **sysadmin** . Quando a opção **sync_type** estiver definida como *Automatic*, nenhuma ação especial do Agente de Leitor de Log será necessária.  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin ou da função de banco de dados fixa db_owner podem executar sp_addsubscription. Para assinaturas pull, os usuários com logons na lista de acesso à publicação podem executar sp_addsubscription.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addsubscription-trans_1.sql)]  
  
## <a name="see-also"></a>Consulte também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Criar uma assinatura para um assinante não SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
