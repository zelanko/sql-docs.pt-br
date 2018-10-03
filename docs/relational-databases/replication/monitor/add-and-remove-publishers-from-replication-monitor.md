---
title: Adicionar e remover publicadores do Replication Monitor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7bb17f73c4a3d9d1cd1127b7a11856a91cf4dab3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781536"
---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>Adicionar e remover Publicadores do Replication Monitor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O servidor no qual você inicia o Replication Monitor será adicionado automaticamente ao monitor se for um Publicador. Publicadores adicionais podem ser adicionados na caixa de diálogo **Adicionar Publicador** . Depois de adicionar um Publicador, será exibido em um grupo no painel esquerdo do monitor. O grupo **Meus Publicadores** é incluído por padrão, mas você pode criar novos grupos para gerenciar uma ou mais topologias de replicação. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-add-a-sql-server-publisher"></a>Para adicionar um Editor SQL Server  
  
1.  Clique com o botão direito do mouse no nó **Replication Monitor** ou em um nó do Grupo do publicador no painel esquerdo e, então, clique em **Adicionar Publicador**.  
  
2.  Na caixa de diálogo **Adicionar Publicador** , clique em **Adicionar**e, então, clique em **Adicionar um Editor SQL Server**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , digite o nome do Publicador e selecione o tipo de autenticação. Se você selecionar **Autenticação do SQL Server**, digite um logon e senha. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou o logon do SQL Server especificado deve ser um membro da função de servidor fixa **sysadmin** ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição.  
  
4.  Clique em **Conectar**. Se o Publicador usar um Distribuidor remoto, você receberá uma solicitação para conectar-se ao Distribuidor na caixa de diálogo **Conectar ao Servidor** . As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou o logon do SQL Server especificado deve ser um membro da função de servidor fixa **sysadmin** ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição.  
  
5.  O nome do Publicador e do Distribuidor são exibidos na grade **Iniciar a monitoração nos seguintes Publicadores** .  
  
6.  Para especificar opções de atualização e conexão com o Publicador, selecione o Publicador na grade e modifique as opções, se necessário. Para obter mais informações sobre essas opções de atualização, consulte [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selecione o grupo no qual o Publicador deverá ser exibido no Replication Monitor. Para criar um novo grupo, clique em **Novo Grupo**e digite o nome do grupo; selecione o grupo na lista **Mostrar esses Publicadores no seguinte grupo** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>Para adicionar um Editor Oracle  
  
1.  Clique com o botão direito do mouse no nó **Replication Monitor** ou em um nó do Grupo do publicador no painel esquerdo e, então, clique em **Adicionar Publicador**.  
  
2.  Na caixa de diálogo **Adicionar Publicador** , clique em **Adicionar**e, então, clique em **Adicionar um Editor Oracle**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , digite o nome do Distribuidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] associado ao Editor Oracle, e, então, selecione o tipo de autenticação. Se você selecionar **Autenticação do SQL Server**, digite um logon e senha. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou o logon do SQL Server especificado deve ser um membro da função de servidor fixa **sysadmin** ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição.  
  
4.  Clique em **Conectar**.  
  
5.  O nome do Publicador e do Distribuidor são exibidos na grade **Iniciar a monitoração nos seguintes Publicadores** .  
  
6.  Para especificar opções de atualização e conexão com o Publicador, selecione o Publicador na grade e modifique as opções, se necessário. Para obter mais informações sobre essas opções de atualização, consulte [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selecione o grupo no qual o Publicador deverá ser exibido no Replication Monitor. Para criar um novo grupo, clique em **Novo Grupo**e digite o nome do grupo; selecione o grupo na lista **Mostrar esses Publicadores no seguinte grupo** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>Para adicionar um ou mais Publicadores que usam o mesmo Distribuidor  
  
1.  Clique com o botão direito do mouse no nó **Replication Monitor** ou em um nó do Grupo do publicador no painel esquerdo e, então, clique em **Adicionar Publicador**.  
  
2.  Na caixa de diálogo **Adicionar Publicador** , clique em **Adicionar**e então clique em **Especificar um Distribuidor e Adicionar seus Publicadores**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , digite o nome do Distribuidor e selecione o tipo de autenticação. Se você selecionar **Autenticação do SQL Server**, digite um logon e senha. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou o logon do SQL Server especificado deve ser um membro da função de servidor fixa **sysadmin** ou membro da função de banco de dados fixa **replmonitor** no banco de dados de distribuição.  
  
4.  Clique em **Conectar**.  
  
5.  O nome do Distribuidor e de cada Publicador são exibidos na grade **Iniciar a monitoração nos seguintes Publicadores** . Se um Publicador já foi adicionado ao Replication Monitor, não será exibido na grade.  
  
6.  Para especificar opções de atualização e conexão com o Publicador, selecione o Publicador na grade e modifique as opções, se necessário. Para obter mais informações sobre essas opções de atualização, consulte [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selecione o grupo no qual os Publicadores deverão ser exibidos no Replication Monitor. Para criar um novo grupo, clique em **Novo Grupo**e digite o nome do grupo; selecione o grupo na lista **Mostrar esses Publicadores no seguinte grupo** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>Para modificar as configurações para o Publicador e o Grupo do publicador  
  
1.  Clique com o botão direito do mouse no Publicador do painel esquerdo, e, então, clique em **Configurações do Publicador**.  
  
2.  Faça todas as alterações na caixa de diálogo **Configurações do Publicador** :  
  
    -   Para alterar as credenciais que o Replication Monitor usa para conectar ao servidor, clique em **Conexão do Publicador** ou **Conexão do Distribuidor**e, então, digite as credenciais na caixa de diálogo **Conectar ao Servidor** .  
  
    -   Para mover um Publicador de um grupo para o outro, selecione o Publicador na grade **Iniciar a monitoração nos seguintes Publicadores** e selecione o novo grupo na lista **Mostrar esses Publicadores no seguinte grupo** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>Para remover o Publicador do Replication Monitor  
  
1.  Clique com o botão direito do mouse em um Publicador no painel esquerdo.  
  
2.  Clique em **Remover**.  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>Para adicionar um Grupo do publicador ao Replication Monitor  
  
1.  Só podem ser criados Grupos do publicador ao adicionar um Publicador ou modificar as configurações de um Publicador. Para obter mais informações, consulte os procedimentos sobre como adicionar um Publicador.  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>Para remover um grupo do Publicador do Replication Monitor  
  
1.  Mova todos os Publicadores para um grupo diferente ou remova-os do Replication Monitor. Para obter mais informações, consulte os procedimentos anteriores neste tópico.  
  
2.  Clique com o botão direito do mouse no grupo do Publicador e, então, clique em **Remover**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../../relational-databases/replication/configure-distribution.md)   
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
