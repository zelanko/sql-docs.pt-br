---
title: Criar assinatura atualizável para publicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updateable transactional subscriptions, T-SQL
ms.assetid: a6e80857-0a69-4867-b6b7-f3629d00c312
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8150c81a52efb13a26b8fa0706d58fc0b6ee289
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713794"
---
# <a name="create-updatable-subscription-to-transactional-publication"></a>Criar assinatura atualizável para publicação transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  Este recurso permanecerá com suporte em versões do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] de 2012 até 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
A replicação transacional permite que mudanças sejam realizadas em um Assinante para serem propagadas de volta para o Publicador usando assinaturas de atualizações imediatas ou colocadas em fila. Você pode criar uma assinatura de atualização de forma programada, usando os procedimentos de replicação armazenados. (Além disso, consulte [Como criar uma assinatura atualizável para uma publicação transacional (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md).) 

## <a name="to-create-an-immediate-updating-pull-subscription"></a>Para criar uma assinatura pull de atualização imediata ##

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização imediata executando o [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_sync_tran` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas de atualização imediata.

    * Se o valor de `allow_sync_tran` no conjunto de resultados for `0`, a publicação deverá ser recriada com as assinaturas de atualização imediata habilitadas.

2. No Publicador, verifique se a publicação tem suporte para assinaturas pull executando [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_pull` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas pull.

    * Se o valor de `allow_pull` for `0`, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)especificando `allow_pull` para `@property` e `true` para `@value`. 

3. No Assinante, execute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique `@publisher` e `@publication`, e um dos valores a seguir para `@update_mode`:

    * `sync tran` – habilita a assinatura para atualização imediata.

    * `failover` – habilita a assinatura para atualização imediata com atualização enfileirada como uma opção de failover.

    > [!NOTE]  
>  `failover` requer que a publicação também esteja habilitada para assinaturas de atualização em fila. 
 
4. No Assinante, execute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique o seguinte:

    * Os parâmetros `@publisher`, `@publisher_db`e `@publication` . 

    * As credenciais do Microsoft Windows sob as quais o Distribution Agent do Assinante é executado para `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local ao Assinante usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Distribuidor usando a Autenticação Integrada do Windows. 
 
    * (Opcional) Um valor de `0` para `@distributor_security_mode` e as informações de logon do Microsoft SQL Server para `@distributor_login` e `@distributor_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Distribuidor. 

    * Agenda para o trabalho do Distribution Agent para essa assinatura. 

5. No Assinante, no banco de dados de assinatura, execute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique `@publisher`, `@publication`, o nome do banco de dados da publicação para `@publisher_db`e um dos seguintes valores para `@security_mode`: 

    * `0` – Use a Autenticação do SQL Server ao fazer atualizações no Publicador. Essa opção requer a especificação de um logon válido no Publicador para `@login` e `@password`.

    * `1` – Use o contexto de segurança do usuário que faz alterações no Assinante quando se conecta ao Publicador. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) quanto às restrições relacionadas a esse modo de segurança.

    * `2` – Use um logon de servidor vinculado, existente, definido pelo usuário criado usando [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).

6. No Publicador, execute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) especificando `@publication`, `@subscriber`, `@destination_db`, um valor de pull para `@subscription_type`e o mesmo valor especificado na etapa 3 para `@update_mode`.

Isto registra a assinatura pull no Publicador. 


## <a name="to-create-an-immediate-updating-push-subscription"></a>Para criar uma assinatura push de atualização imediata ##

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização imediata executando o [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_sync_tran` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas de atualização imediata.

    * Se o valor de `allow_sync_tran` no conjunto de resultados for `0`, a publicação deverá ser recriada com as assinaturas de atualização imediata habilitadas.

2. No Publicador, verifique se a publicação tem suporte para assinaturas push executando [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_push` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas push.

    * Se o valor de `allow_push` for `0`, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)especificando `allow_push` para `@property` e `true` para `@value`. 

3. No Publicador, execute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique `@publication`, `@subscriber`, `@destination_db`e um dos valores a seguir para `@update_mode`:

    * `sync tran` – habilita o suporte para a atualização imediata.

    * `failover` – habilita o suporte para atualização imediata com a atualização em fila como opção do failover.

    > [!NOTE]  
>  `failover` requer que a publicação também esteja habilitada para assinaturas de atualização em fila. 
 
4. No Publicador, execute [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique os seguintes parâmetros:

    * `@subscriber`, `@subscriber_db`e `@publication`. 

    * As credenciais do Windows sob as quais o Distribution Agent no Distribuidor é executado pata `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows. 

    * (Opcional) Um valor de `0` para `@subscriber_security_mode` e as informações de logon do SQL Server para `@subscriber_login` e `@subscriber_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Assinante. 

    * Agenda para o trabalho do Distribution Agent para essa assinatura.

5. No Assinante, no banco de dados de assinatura, execute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique `@publisher`, `@publication`, o nome do banco de dados da publicação para `@publisher_db`e um dos seguintes valores para `@security_mode`: 

     * `0` – Use a Autenticação do SQL Server ao fazer atualizações no Publicador. Essa opção requer a especificação de um logon válido no Publicador para `@login` e `@password`.

     * `1` – Use o contexto de segurança do usuário que faz alterações no Assinante quando se conecta ao Publicador. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) quanto às restrições relacionadas a esse modo de segurança.

     * `2` – Use um logon de servidor vinculado, existente, definido pelo usuário criado usando [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).


## <a name="to-create-a-queued-updating-pull-subscription"></a>Para criar uma assinatura pull de atualização em fila ##

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização em fila executando [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_queued_tran` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas de atualização imediata.

    * Se o valor de `allow_queued_tran` no conjunto de resultados for `0`, a publicação deverá ser recriada com as assinaturas de atualização em fila habilitadas.

2. No Publicador, verifique se a publicação tem suporte para assinaturas pull executando [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_pull` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas pull.

    * Se o valor de `allow_pull` for `0`, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)especificando `allow_pull` para `@property` e `true` para `@value`. 

3. No Assinante, execute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique `@publisher` e `@publication`, e um dos valores a seguir para `@update_mode`:

    * `queued tran` – habilita a assinatura de atualização enfileirada.

    * `queued failover` – habilita o suporte para atualização em fila com a atualização imediata como opção do failover.

    > [!NOTE]  
>  `queued failover` requer que a publicação também esteja habilitada para assinaturas de atualização imediata. Para failover de atualização imediata, você deve usar [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para definir as credenciais sob as quais as alterações no Assinante são replicadas no Publicador.
 
4. No Assinante, execute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique os seguintes parâmetros:

    * @publisher, `@publisher_db`e `@publication`. 

    * As credenciais do Windows sob as quais o Distribution Agent do Assinante é executado para `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local ao Assinante usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Distribuidor usando a Autenticação Integrada do Windows. 
 
    * (Opcional) Um valor de `0` para `@distributor_security_mode` e as informações de logon do SQL Server para `@distributor_login` e `@distributor_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Distribuidor. 

    * Agenda para o trabalho do Distribution Agent para essa assinatura.

5. No Publicador, execute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md) para registrar o Assinante no Publicador, especificando `@publication`, `@subscriber`, `@destination_db`, um valor de pull para `@subscription_type`e o mesmo valor especificado na etapa 3 para `@update_mode`.

Isto registra a assinatura pull no Publicador. 


## <a name="to-create-a-queued-updating-push-subscription"></a>Para criar uma assinatura push de atualização em fila ##

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização em fila executando [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de allow_queued_tran no conjunto de resultados for 1, a publicação tem suporte para assinaturas de atualização imediata.

    * Se o valor de allow_queued_tran no conjunto de resultados for 0, a publicação deverá ser recriada com as assinaturas de atualização em fila habilitadas. Para obter mais informações, consulte Como habilitar a atualização de assinaturas para publicações transacionais (Programação Transact-SQL de replicação).

2. No Publicador, verifique se a publicação tem suporte para assinaturas push executando [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). 

    * Se o valor de `allow_push` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas push.

    * Se o valor de `allow_push` for `0`, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)especificando allow_push para `@property` e `true` para `@value`. 

3. No Publicador, execute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique `@publication`, `@subscriber`, `@destination_db`e um dos valores a seguir para `@update_mode`:

    * `queued tran` – habilita a assinatura de atualização enfileirada.

    * `queued failover` – habilita o suporte para atualização em fila com a atualização imediata como opção do failover.

    > [!NOTE]  
>  A opção failover em fila requer que a publicação também esteja habilitada para assinaturas de atualização imediata. Para failover de atualização imediata, você deve usar [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para definir as credenciais sob as quais as alterações no Assinante são replicadas no Publicador.

4. No Publicador, execute [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique os seguintes parâmetros:

    * `@subscriber`, `@subscriber_db`e `@publication`. 

    * As credenciais do Windows sob as quais o Distribution Agent no Distribuidor é executado pata `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta com o Assinante usando a Autenticação Integrada do Windows. 
 
    * (Opcional) Um valor de `0` para `@subscriber_security_mode` e as informações de logon do SQL Server para `@subscriber_login` e `@subscriber_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Assinante. 

    * Agenda para o trabalho do Distribution Agent para essa assinatura.


## <a name="example"></a>Exemplo ##

Este exemplo cria uma assinatura pull de atualização imediata a uma publicação que tem suporte para assinaturas de atualização imediata. Os valores para o logon e senha são fornecidos no tempo de execução usando as variáveis sqlcmd scripting.

> [!NOTE]  
>  Este script usa as variáveis de script do sqlcmd. Elas estão no formato `$(MyVariable)`. Para obter informações sobre como usar variáveis de script na linha de comando e no SQL Server Management Studio, consulte a seção **Executando scripts de replicação** no tópico [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).

```
-- Execute this batch at the Subscriber.
DECLARE @publication AS sysname;
DECLARE @publicationDB AS sysname;
DECLARE @publisher AS sysname;
DECLARE @login AS sysname;
DECLARE @password AS nvarchar(512);
SET @publication = N'AdvWorksProductTran';
SET @publicationDB = N'AdventureWorks2008R2';
SET @publisher = $(PubServer);
SET @login = $(Login);
SET @password = $(Password);

-- At the subscription database, create a pull subscription to a transactional 
-- publication using immediate updating with queued updating as a failover.
EXEC sp_addpullsubscription 
    @publisher = @publisher, 
    @publication = @publication, 
    @publisher_db = @publicationDB, 
    @update_mode = N'failover', 
    @subscription_type = N'pull';

-- Add an agent job to synchronize the pull subscription, 
-- which uses Windows Authentication when connecting to the Distributor.
EXEC sp_addpullsubscription_agent 
    @publisher = @publisher, 
    @publisher_db = @publicationDB, 
    @publication = @publication,
    @job_login = @login,
    @job_password = @password; 

-- Add a Windows Authentication-based linked server that enables the 
-- Subscriber-side triggers to make updates at the Publisher. 
EXEC sp_link_publication 
    @publisher = @publisher, 
    @publication = @publication,
    @publisher_db = @publicationDB, 
    @security_mode = 0,
    @login = @login,
    @password = @password;
GO

USE AdventureWorks2008R2;
GO

-- Execute this batch at the Publisher.
DECLARE @publication AS sysname;
DECLARE @subscriptionDB AS sysname;
DECLARE @subscriber AS sysname;
SET @publication = N'AdvWorksProductTran'; 
SET @subscriptionDB = N'AdventureWorks2008R2Replica'; 
SET @subscriber = $(SubServer);

-- At the Publisher, register the subscription, using the defaults.
USE [AdventureWorks2008R2]
EXEC sp_addsubscription 
    @publication = @publication, 
    @subscriber = @subscriber, 
    @destination_db = @subscriptionDB, 
    @subscription_type = N'pull', 
    @update_mode = N'failover';
GO
```

## <a name="see-also"></a>Consulte Também ##

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Usar sqlcmd com variáveis de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)

[Como criar uma assinatura atualizável para uma publicação transacional (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)

