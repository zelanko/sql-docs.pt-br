---
title: Criar uma assinatura atualizável para uma publicação transacional (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updateable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f9c04c03c08f118314dc96c8b491e61be317f40c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62691590"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-management-studio"></a>Como criar uma assinatura atualizável para uma publicação transacional (Management Studio)

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
A replicação transacional permite que mudanças sejam realizadas em um Assinante para serem propagadas de volta para o Publicador usando assinaturas de atualizações imediatas ou colocadas em fila. Você pode criar uma assinatura de atualização de forma programada, usando os procedimentos de replicação armazenados.

Configurar assinaturas atualizáveis no página **Assinaturas Atualizáveis** do **Assistente para Nova Assinatura**. Esta página só estará disponível quando uma publicação transacional tiver sido ativada para assinaturas atualizáveis. Para obter mais informações sobre como habilitar assinaturas atualizáveis, consulte [Habilitar atualização de assinaturas para publicações transacionais](enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="configure-an-updatable-subscription-from-the-publisher"></a>Configurar uma assinatura atualizável do Editor  

1. Conecte-se ao Publicador no Microsoft SQL Server Management Studio e, em seguida, expanda o nó de servidor.
2. Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .
3. Clique com o botão direito do mouse em uma publicação transacional habilitada para atualizar assinaturas e, em seguida, clique em **Novas Assinaturas**.
4. Percorra as páginas no assistente para especificar opções para a assinatura, como onde o Distribution Agent deverá ser executado.
5. Na página **Assinaturas Atualizáveis** do **Assistente para Nova Assinatura**, verifique se **Replicar** está selecionado.
6. Selecione uma opção na lista suspensa **Confirmar no Publicador**:

    *  Para usar a atualização imediata de assinaturas, selecione **Confirmar alterações simultaneamente**. Se você selecionar essa opção e a publicação permitir atualização de assinatura na fila (o padrão para publicações criadas com o Assistente para Nova Publicação), a propriedade de assinatura **update_mode** será definida como **failover**. Esse modo permite a troca posterior para atualização em fila, se necessário.
    *  Para usar atualização de assinaturas em fila, selecione **Enfileirar alterações e confirmar quando possível**. Se você selecionar essa opção e a publicação permitir atualização imediata de assinaturas (o padrão para publicações criadas com o Assistente para Nova Publicação) e o Assinante estiver executando o SQL Server 2005 ou uma versão posterior, a propriedade de assinatura **update_mode** será definida como failover em fila. Esse modo permite troca imediata para atualização posterior, se necessária.

    Para obter informações sobre como alternar os modos de atualização, consulte [Switch Between Update Modes for an Updatable Transactional Subscription](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md) (Alternar entre modos de atualização para uma assinatura transacional atualizável).

7. A página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis) é exibida para assinaturas que usam a atualização imediata ou têm **update_mode** definido para **failover em fila**. Na página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis), especifique um servidor vinculado por meio do qual as conexões com o Publicador serão feitas para atualizações imediatas de assinaturas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Selecione uma das seguintes opções:

    * **Criar um servidor vinculado que se conecta usando a Autenticação do SQL Server.** Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação cria um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.
    * **Usar servidor vinculado ou remoto já definido.** Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o Assinante e o Publicador usando [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), o SQL Server Management Studio ou outro método.

    Para obter informações sobre as permissões exigidas pela conta de servidor vinculado, consulte o **Assinaturas de atualização em fila** de [inserir descrição do link aqui](../security/secure-the-subscriber.md).

8. Conclua o assistente.

## <a name="configure-an-updatable-subscription-from-the-subscriber"></a>Configurar uma assinatura atualizável do Assinante


1. Conecte-se ao Assinante no SQL Server Management Studio e, em seguida, expanda o nó de servidor.
2. Expanda a pasta **Replicação** .
3. Clique com o botão direito do mouse na pasta **Assinaturas Locais** e depois clique em **Novas Assinaturas**.
4. Na página **Publicação** do **Assistente para Nova Assinatura**, selecione **Encontrar Publicador do SQL Server** na lista suspensa **Publicador**.
5. Conecte-se ao Publicador na caixa de diálogo **Conectar ao Servidor** .
6. Selecione uma publicação transacional habilitada para atualizar assinaturas na página **Publicação**.
7. Percorra as páginas no assistente para especificar opções para a assinatura, como onde o Distribution Agent deverá ser executado.
8. Na página **assinaturas atualizáveis** do assistente para nova assinatura, verifique se **replicar** está selecionado.
9. Selecione uma opção na lista suspensa **Confirmar no Publicador**:

    * Para usar a atualização imediata de assinaturas, selecione **Confirmar alterações simultaneamente**. Se você selecionar essa opção e a publicação permitir atualização de assinatura na fila (o padrão para publicações criadas com o Assistente para Nova Publicação), a propriedade de assinatura **update_mode** será definida como **failover**. Esse modo permite a troca posterior para atualização em fila, se necessário.
    * Para usar atualização de assinaturas em fila, selecione **Enfileirar alterações e confirmar quando possível**. Se você selecionar essa opção e a publicação permitir assinaturas de atualização imediata (o padrão para publicações criadas com o assistente para nova publicação) e o Assinante estiver executando SQL Server 2005 ou uma versão posterior, a propriedade de assinatura **update_mode** será definida como **failover**em fila. Esse modo permite troca imediata para atualização posterior, se necessária.

    Para obter informações sobre como alternar os modos de atualização, consulte [Switch Between Update Modes for an Updatable Transactional Subscription](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md) (Alternar entre modos de atualização para uma assinatura transacional atualizável).

10. A página **logon para assinaturas atualizáveis** é exibida para assinaturas que usam atualização imediata ou têm **update_mode** definido para **failover**em fila. Na página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis), especifique um servidor vinculado por meio do qual as conexões com o Publicador serão feitas para atualizações imediatas de assinaturas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Selecione uma das seguintes opções:

    * **Criar um servidor vinculado que se conecta usando a Autenticação do SQL Server.** Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação cria um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.
    * **Usar servidor vinculado ou remoto já definido.** Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o Assinante e o Publicador usando [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), o SQL Server Management Studio ou outro método.

    Para obter informações sobre as permissões exigidas pela conta de servidor vinculado, consulte o **Assinaturas de atualização em fila** de [inserir descrição do link aqui](../security/secure-the-subscriber.md).

11. Conclua o assistente.

## <a name="create-an-immediate-updating-pull-subscription"></a>Criar uma assinatura pull de atualização imediata

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização imediata executando o [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_sync_tran` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas de atualização imediata.
    * Se o valor de `allow_sync_tran` no conjunto de resultados for `0`, a publicação deverá ser recriada com as assinaturas de atualização imediata habilitadas.

2. No Publicador, verifique se a publicação tem suporte para assinaturas pull executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_pull` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas pull.
    * Se o valor de `allow_pull` for `0`, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)especificando `allow_pull` para `@property` e `true` para `@value`. 

3. No Assinante, execute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique `@publisher` e `@publication`, e um dos valores a seguir para `@update_mode`:

    * `sync tran` – habilita a assinatura para atualização imediata.
    * `failover` – habilita a assinatura para atualização imediata com atualização enfileirada como uma opção de failover.

    > [!NOTE]  
>  `failover` requer que a publicação também esteja habilitada para assinaturas de atualização em fila. 
 
4. No Assinante, execute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique o seguinte:

    * Os parâmetros `@publisher`, `@publisher_db`e `@publication` . 
    * As credenciais do Microsoft Windows sob as quais o Distribution Agent do Assinante é executado para `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local ao Assinante usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Distribuidor usando a Autenticação Integrada do Windows. 
 
    * (Opcional) Um valor de `0` para `@distributor_security_mode` e as informações de logon do Microsoft SQL Server para `@distributor_login` e `@distributor_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Distribuidor. 
    * Agenda para o trabalho do Distribution Agent para essa assinatura. 

5. No Assinante, no banco de dados de assinatura, execute [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql). Especifique `@publisher`, `@publication`, o nome do banco de dados da publicação para `@publisher_db`e um dos seguintes valores para `@security_mode`: 

    * `0` – Use a Autenticação do SQL Server ao fazer atualizações no Publicador. Essa opção requer a especificação de um logon válido no Publicador para `@login` e `@password`.
    * `1` – Use o contexto de segurança do usuário que faz alterações no Assinante quando se conecta ao Publicador. Consulte [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) quanto às restrições relacionadas a esse modo de segurança.
    * `2` – Use um logon de servidor vinculado, existente, definido pelo usuário criado usando [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).

6. No Publicador, execute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) especificando `@publication`, `@subscriber`, `@destination_db`, um valor de pull para `@subscription_type`, e o mesmo valor especificado na etapa 3 para `@update_mode`.

Isto registra a assinatura pull no Publicador. 


## <a name="create-an-immediate-updating-push-subscription"></a>Criar uma assinatura push de atualização imediata 

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização imediata executando o [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_sync_tran` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas de atualização imediata.
    * Se o valor de `allow_sync_tran` no conjunto de resultados for `0`, a publicação deverá ser recriada com as assinaturas de atualização imediata habilitadas.

2. No Publicador, verifique se a publicação tem suporte para assinaturas push executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_push` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas push.
    * Se o valor de `allow_push` for `0`, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)especificando `allow_push` para `@property` e `true` para `@value`. 

3. No Publicador, execute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique `@publication`, `@subscriber`, `@destination_db`e um dos valores a seguir para `@update_mode`:

    * `sync tran` – habilita o suporte para a atualização imediata.
    * `failover` – habilita o suporte para atualização imediata com a atualização em fila como opção do failover.

    > [!NOTE]  
>  `failover` requer que a publicação também esteja habilitada para assinaturas de atualização em fila. 
 
4. No Publicador, execute [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Especifique os seguintes parâmetros:

    * `@subscriber`, `@subscriber_db`e `@publication`. 
    * As credenciais do Windows sob as quais o Distribution Agent no Distribuidor é executado pata `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows. 

    * (Opcional) Um valor de `0` para `@subscriber_security_mode` e as informações de logon do SQL Server para `@subscriber_login` e `@subscriber_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Assinante. 
    * Agenda para o trabalho do Distribution Agent para essa assinatura.

5. No Assinante, no banco de dados de assinatura, execute [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql). Especifique `@publisher`, `@publication`, o nome do banco de dados da publicação para `@publisher_db`e um dos seguintes valores para `@security_mode`: 

     * `0` – Use a Autenticação do SQL Server ao fazer atualizações no Publicador. Essa opção requer a especificação de um logon válido no Publicador para `@login` e `@password`.
     * `1` – Use o contexto de segurança do usuário que faz alterações no Assinante quando se conecta ao Publicador. Consulte [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) quanto às restrições relacionadas a esse modo de segurança.
     * `2` – Use um logon de servidor vinculado, existente, definido pelo usuário criado usando [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).


## <a name="create-a-queued-updating-pull-subscription"></a>Criar uma assinatura pull de atualização em fila ##

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização em fila executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_queued_tran` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas de atualização imediata.
    * Se o valor de `allow_queued_tran` no conjunto de resultados for `0`, a publicação deverá ser recriada com as assinaturas de atualização em fila habilitadas.

2. No Publicador, verifique se a publicação tem suporte para assinaturas pull executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_pull` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas pull.
    * Se o valor de `allow_pull` for `0`, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)especificando `allow_pull` para `@property` e `true` para `@value`. 

3. No Assinante, execute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique `@publisher` e `@publication`, e um dos valores a seguir para `@update_mode`:

    * `queued tran` – habilita a assinatura de atualização enfileirada.
    * `queued failover` – habilita o suporte para atualização em fila com a atualização imediata como opção do failover.

    > [!NOTE]  
>  `queued failover` requer que a publicação também esteja habilitada para assinaturas de atualização imediata. Para failover de atualização imediata, você deve usar [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) para definir as credenciais sob as quais as alterações no Assinante são replicadas no Publicador.
 
4. No Assinante, execute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique os seguintes parâmetros:

    * @publisher, `@publisher_db`e `@publication`. 
    * As credenciais do Windows sob as quais o Distribution Agent do Assinante é executado para `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local ao Assinante usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Distribuidor usando a Autenticação Integrada do Windows. 
 
    * (Opcional) Um valor de `0` para `@distributor_security_mode` e as informações de logon do SQL Server para `@distributor_login` e `@distributor_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Distribuidor. 
    * Agenda para o trabalho do Distribution Agent para essa assinatura.

5. No Publicador, execute [sp_addsubscriber](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql) para registrar o Assinante no Publicador, `@publication`especificando `@subscriber`, `@destination_db`,, um valor de pull `@subscription_type`para, e o mesmo valor especificado na etapa 3 `@update_mode`para.

Isto registra a assinatura pull no Publicador. 


## <a name="to-create-a-queued-updating-push-subscription"></a>Para criar uma assinatura push de atualização em fila ##

1. No Publicador, verifique se a publicação tem suporte para assinaturas de atualização em fila executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de allow_queued_tran no conjunto de resultados for 1, a publicação tem suporte para assinaturas de atualização imediata.
    * Se o valor de allow_queued_tran no conjunto de resultados for 0, a publicação deverá ser recriada com as assinaturas de atualização em fila habilitadas. Para obter mais informações, consulte Como habilitar a atualização de assinaturas para publicações transacionais (Programação Transact-SQL de replicação).

2. No Publicador, verifique se a publicação tem suporte para assinaturas push executando [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql). 

    * Se o valor de `allow_push` no conjunto de resultados for `1`, a publicação tem suporte para assinaturas push.
    * Se o valor de `allow_push` for `0`, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)especificando allow_push para `@property` e `true` para `@value`. 

3. No Publicador, execute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique `@publication`, `@subscriber`, `@destination_db`e um dos valores a seguir para `@update_mode`:

    * `queued tran` – habilita a assinatura de atualização enfileirada.
    * `queued failover` – habilita o suporte para atualização em fila com a atualização imediata como opção do failover.

    > [!NOTE]  
>  A opção failover em fila requer que a publicação também esteja habilitada para assinaturas de atualização imediata. Para failover de atualização imediata, você deve usar [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) para definir as credenciais sob as quais as alterações no Assinante são replicadas no Publicador.

4. No Publicador, execute [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Especifique os seguintes parâmetros:

    * `@subscriber`, `@subscriber_db`e `@publication`. 
    * As credenciais do Windows sob as quais o Distribution Agent no Distribuidor é executado pata `@job_login` e `@job_password`. 

    > [!NOTE]  
>  As conexões realizadas com o uso da Autenticação Integrada do Windows sempre são feitas com as credenciais do Windows especificadas por `@job_login` e `@job_password`. O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta com o Assinante usando a Autenticação Integrada do Windows. 
 
    * (Opcional) Um valor de `0` para `@subscriber_security_mode` e as informações de logon do SQL Server para `@subscriber_login` e `@subscriber_password`, se você precisar usar a Autenticação do SQL Server ao se conectar ao Assinante. 
    * Agenda para o trabalho do Distribution Agent para essa assinatura.


## <a name="example"></a>Exemplo ##

Este exemplo cria uma assinatura pull de atualização imediata a uma publicação que tem suporte para assinaturas de atualização imediata. Os valores para o logon e senha são fornecidos no runtime usando as variáveis sqlcmd scripting.

> [!NOTE]  
>  Este script usa as variáveis de script do sqlcmd. Elas estão no formato `$(MyVariable)`. Para obter informações sobre como usar variáveis de script na linha de comando e no SQL Server Management Studio, consulte a seção **Executando scripts de replicação** no tópico [Conceitos dos procedimentos armazenados do sistema de replicação](../concepts/replication-system-stored-procedures-concepts.md).

```sql
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

## <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>Definir opções de resolução de conflito de atualização na fila (SQL Server Management Studio)
  Defina as opções de resolução de conflitos para publicações que dão suporte a assinaturas de atualização na fila na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>Para definir opções de resolução de conflito de atualização na fila  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione um dos seguintes valores para a opção **Política de resolução de conflitos**:    
    -   **Mantenha a alteração do Publicador.**    
    -   **Mantenha a alteração do Assinante.**    
    -   **Reinicialize a assinatura.**    
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="see-also"></a>Consulte Também ##
 [Create a Publication](create-a-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Usar sqlcmd com variáveis de script](../../scripting/sqlcmd-use-with-scripting-variables.md)   

  
