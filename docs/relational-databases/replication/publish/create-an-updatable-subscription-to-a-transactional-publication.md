---
title: Criar uma assinatura atualizável em uma publicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 730100ef54e9eb9c9aa3a68a461e0e35d3bb2ab3
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37355668"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>Criar uma assinatura atualizável em uma publicação transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  Este recurso permanecerá com suporte em versões do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] de 2012 até 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Configurar assinaturas atualizáveis no página **Assinaturas Atualizáveis** do **Assistente para Nova Assinatura**. Esta página só estará disponível quando uma publicação transacional tiver sido ativada para assinaturas atualizáveis. Para obter mais informações sobre como habilitar assinaturas atualizáveis, consulte [Habilitar atualização de assinaturas para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>Para configurar uma assinatura atualizável no Publicador  

1. Conecte-se ao Publicador no Microsoft SQL Server Management Studio e, em seguida, expanda o nó de servidor.

2. Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .

3. Clique com o botão direito do mouse em uma publicação transacional habilitada para atualizar assinaturas e, em seguida, clique em **Novas Assinaturas**.

4. Percorra as páginas no assistente para especificar opções para a assinatura, como onde o Distribution Agent deverá ser executado.

5. Na página **Assinaturas Atualizáveis** do **Assistente para Nova Assinatura**, verifique se **Replicar** está selecionado.

6. Selecione uma opção na lista suspensa **Confirmar no Publicador**:

    * Para usar a atualização imediata de assinaturas, selecione **Confirmar alterações simultaneamente**. Se você selecionar essa opção e a publicação permitir atualização de assinatura na fila (o padrão para publicações criadas com o Assistente para Nova Publicação), a propriedade de assinatura **update_mode** será definida como **failover**. Esse modo permite a troca posterior para atualização em fila, se necessário.

    * Para usar atualização de assinaturas em fila, selecione **Enfileirar alterações e confirmar quando possível**. Se você selecionar essa opção e a publicação permitir atualização imediata de assinaturas (o padrão para publicações criadas com o Assistente para Nova Publicação) e o Assinante estiver executando o SQL Server 2005 ou uma versão posterior, a propriedade de assinatura **update_mode** será definida como failover em fila. Esse modo permite troca imediata para atualização posterior, se necessária.

    Para obter informações sobre como alternar os modos de atualização, consulte [Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md) (Alternar entre modos de atualização para uma assinatura transacional atualizável).

7. A página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis) é exibida para assinaturas que usam a atualização imediata ou têm **update_mode** definido para **failover em fila**. Na página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis), especifique um servidor vinculado por meio do qual as conexões com o Publicador serão feitas para atualizações imediatas de assinaturas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Selecione uma das opções a seguir:

    * **Criar um servidor vinculado que se conecta usando a Autenticação do SQL Server.** Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação cria um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.

    * **Usar servidor vinculado ou remoto já definido.** Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o Assinante e o Publicador usando [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), o SQL Server Management Studio ou outro método.

    Para obter informações sobre as permissões exigidas pela conta de servidor vinculado, consulte o **Assinaturas de atualização em fila** de [inserir descrição do link aqui](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Conclua o assistente.

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>Para configurar uma assinatura atualizável no Assinante


1. Conecte-se ao Assinante no SQL Server Management Studio e, em seguida, expanda o nó de servidor.

2. Expanda a pasta **Replicação** .

3. Clique com o botão direito do mouse na pasta **Assinaturas Locais** e depois clique em **Novas Assinaturas**.

4. Na página **Publicação** do **Assistente para Nova Assinatura**, selecione **Encontrar Publicador do SQL Server** na lista suspensa **Publicador**.

5. Conecte-se ao Publicador na caixa de diálogo **Conectar ao Servidor** .

6. Selecione uma publicação transacional habilitada para atualizar assinaturas na página **Publicação**.

7. Percorra as páginas no assistente para especificar opções para a assinatura, como onde o Distribution Agent deverá ser executado.

8. Na página **Assinaturas Atualizáveis** do Assistente para Nova Assinatura, verifique se **Replicar** está selecionado.

9. Selecione uma opção na lista suspensa **Confirmar no Publicador**:

    * Para usar a atualização imediata de assinaturas, selecione **Confirmar alterações simultaneamente**. Se você selecionar essa opção e a publicação permitir atualização de assinatura na fila (o padrão para publicações criadas com o Assistente para Nova Publicação), a propriedade de assinatura **update_mode** será definida como **failover**. Esse modo permite a troca posterior para atualização em fila, se necessário.

    * Para usar atualização de assinaturas em fila, selecione **Enfileirar alterações e confirmar quando possível**. Se você selecionar essa opção e a publicação permitir atualização imediata de assinaturas (o padrão para publicações criadas com o Assistente para Nova Publicação) e o Assinante estiver executando o SQL Server 2005 ou uma versão posterior, a propriedade de assinatura **update_mode** será definida como **failover** em fila. Esse modo permite troca imediata para atualização posterior, se necessária.

    Para obter informações sobre como alternar os modos de atualização, consulte [Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md) (Alternar entre modos de atualização para uma assinatura transacional atualizável).

10. A página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis) é exibida para assinaturas que usam a atualização imediata ou têm **update_mode** definido para **failover** em fila. Na página **Login for Updatable Subscriptions** (Logon para Assinaturas Atualizáveis), especifique um servidor vinculado por meio do qual as conexões com o Publicador serão feitas para atualizações imediatas de assinaturas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Selecione uma das opções a seguir:

    * **Criar um servidor vinculado que se conecta usando a Autenticação do SQL Server.** Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação cria um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.

    * **Usar servidor vinculado ou remoto já definido.** Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o Assinante e o Publicador usando [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), o SQL Server Management Studio ou outro método.

    Para obter informações sobre as permissões exigidas pela conta de servidor vinculado, consulte o **Assinaturas de atualização em fila** de [inserir descrição do link aqui](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Conclua o assistente.

## <a name="see-also"></a>Consulte Também

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)

[Criar uma assinatura atualizável para uma publicação transacional usando o Transact-SQL](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 

