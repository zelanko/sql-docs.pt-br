---
title: "Como criar uma assinatura atualiz&#225;vel para uma publica&#231;&#227;o transacional (Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assinaturas atualizáveis de transacionais"
  - "assinaturas atualizáveis transacionais, SSMS"
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# Como criar uma assinatura atualiz&#225;vel para uma publica&#231;&#227;o transacional (Management Studio)

> [!NOTE]  
>  Este recurso permanecerá com suporte em versões do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] de 2012 até 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Configurar inscrições atualizáveis no **assinaturas atualizáveis** página o **Assistente para nova assinatura**. Esta página só estará disponível quando uma publicação transacional tiver sido ativada para assinaturas atualizáveis. Para obter mais informações sobre como habilitar assinaturas atualizáveis, consulte [Habilitar assinaturas de atualização para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## Para configurar uma assinatura atualizável no Publicador  

1. Conectar-se ao publicador no Microsoft SQL Server Management Studio e, em seguida, expanda o nó do servidor.

2. Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .

3. Clique em uma publicação transacional ativada para assinaturas de atualização e, em seguida, clique em **novas assinaturas**.

4. Percorra as páginas no assistente para especificar opções para a assinatura, como onde o Distribution Agent deverá ser executado.

5. No **assinaturas atualizáveis** página do **Assistente para nova assinatura**, certifique-se de **replicar** está selecionado.

6. Selecione uma opção do **Confirmar no publicador** lista suspensa:

    * Para usar assinaturas de atualização imediata, selecione **Confirmar as alterações simultaneamente**. Se você selecionar essa opção, e a publicação permite inscrições de atualização na fila (o padrão para publicações criadas com o Assistente para nova publicação), a propriedade de assinatura **update_mode** é definido como **failover**. Esse modo permite a troca posterior para atualização em fila, se necessário.

    * Para usar assinaturas de atualização enfileirada, selecione **enfileirar alterações e confirmar quando possível**. Se você selecionar essa opção, a publicação permite assinaturas de atualização imediata (o padrão para publicações criadas com o Assistente para nova publicação) e o assinante estiver executando o SQL Server 2005 ou posterior, a propriedade de assinatura **update_mode** será definida como failover na fila. Esse modo permite troca imediata para atualização posterior, se necessária.

    Para obter informações sobre como alternar os modos de atualização, consulte [Alternar entre atualizar modos para uma assinatura transacional atualizável](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. O **logon para assinaturas atualizáveis** página é exibida para assinaturas que usam a atualização imediata ou tem **update_mode** definida como **failover na fila**. Sobre o **logon para assinaturas atualizáveis** página, especifique um servidor vinculado através do qual são feitas conexões com o publicador para assinaturas de atualização imediata. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Selecione uma das opções a seguir:

    * **Crie um servidor vinculado que conecta-se usando a autenticação do SQL Server.** Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação cria um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.

    * **Usar servidor vinculado ou remoto já definido.** Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o assinante e o publicador usando [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio ou outro método.

    Para obter informações sobre as permissões exigidas pela conta de servidor vinculado, consulte o **assinaturas de atualização enfileirada** de [Inserir link descrição aqui](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Conclua o assistente.

## Para configurar uma assinatura atualizável no Assinante


1. Conectar-se ao assinante no SQL Server Management Studio e, em seguida, expanda o nó do servidor.

2. Expanda a pasta **Replicação** .

3. Clique com botão direito do **assinaturas locais** pasta e clique **novas assinaturas**.

4. No **publicação** página do **Assistente para nova assinatura**, selecione **encontrar publicador SQL Server** do **publicador** lista suspensa.

5. Conecte-se ao Publicador na caixa de diálogo **Conectar ao Servidor** .

6. Selecione uma publicação transacional ativada para assinaturas de atualização de **publicação** página.

7. Percorra as páginas no assistente para especificar opções para a assinatura, como onde o Distribution Agent deverá ser executado.

8. Sobre o **assinaturas atualizáveis** página do Assistente para nova assinatura, certifique-se **replicar** está selecionado.

9. Selecione uma opção do **Confirmar no publicador** lista suspensa:

    * Para usar assinaturas de atualização imediata, selecione **Confirmar as alterações simultaneamente**. Se você selecionar essa opção, e a publicação permite inscrições de atualização na fila (o padrão para publicações criadas com o Assistente para nova publicação), a propriedade de assinatura **update_mode** é definido como **failover**. Esse modo permite a troca posterior para atualização em fila, se necessário.

    * Para usar assinaturas de atualização enfileirada, selecione **enfileirar alterações e confirmar quando possível**. Se você selecionar essa opção, a publicação permite assinaturas de atualização imediata (o padrão para publicações criadas com o Assistente para nova publicação) e o assinante estiver executando o SQL Server 2005 ou posterior, a propriedade de assinatura **update_mode** é definido como em fila **failover**. Esse modo permite troca imediata para atualização posterior, se necessária.

    Para obter informações sobre como alternar os modos de atualização, consulte [Alternar entre atualizar modos para uma assinatura transacional atualizável](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. O **logon para assinaturas atualizáveis** página é exibida para assinaturas que usam a atualização imediata ou tem **update_mode** definidos para **failover**. Sobre o **logon para assinaturas atualizáveis** página, especifique um servidor vinculado através do qual são feitas conexões com o publicador para assinaturas de atualização imediata. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Selecione uma das opções a seguir:

    * **Crie um servidor vinculado que conecta-se usando a autenticação do SQL Server.** Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação cria um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.

    * **Usar servidor vinculado ou remoto já definido.** Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o assinante e o publicador usando [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio ou outro método.

    Para obter informações sobre as permissões exigidas pela conta de servidor vinculado, consulte o **assinaturas de atualização enfileirada** de [Inserir link descrição aqui](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Conclua o assistente.

## Consulte também

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Crie uma publicação](../../../relational-databases/replication/publish/create-a-publication.md)

[Criar uma assinatura atualizável para uma publicação transacional, usando Transact-SQL](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 
