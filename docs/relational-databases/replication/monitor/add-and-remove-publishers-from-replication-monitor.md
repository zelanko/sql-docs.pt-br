---
title: "Adicionar e remover Publicadores do Replication Monitor | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Replication Monitor, adicionando e removendo Publicadores"
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Adicionar e remover Publicadores do Replication Monitor
  O servidor no qual você inicia o Replication Monitor será adicionado automaticamente ao monitor se for um Publicador. Publicadores adicionais podem ser adicionados por meio de **Adicionar publicador** caixa de diálogo. Depois de adicionar um Publicador, será exibido em um grupo no painel esquerdo do monitor. O **Meus Publicadores** grupo é incluído por padrão, mas você pode criar novos grupos para gerenciar um ou mais topologias de replicação. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para adicionar um Editor SQL Server  
  
1.  Clique com botão direito do **Replication Monitor** nó ou um editor de nó no painel à esquerda do grupo e, em seguida, clique em **Adicionar publicador**.  
  
2.  Na **Adicionar publicador** caixa de diálogo, clique em **Add**, e, em seguida, clique em **Adicionar publicador do SQL Server**.  
  
3.  No **conectar ao servidor** caixa de diálogo, digite o nome do Editor e, em seguida, selecione o tipo de autenticação. Se você selecionar **autenticação do SQL Server**, insira um logon e senha. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou um logon do SQL Server especificado deve ser um membro do **sysadmin** fixa a função de servidor ou um membro do **replmonitor** função de banco de dados fixa no banco de dados de distribuição.  
  
4.  Clique em **Conectar**. Se o publicador usar um distribuidor remoto, você deverá conectar-se ao distribuidor no **conectar ao servidor** caixa de diálogo. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou um logon do SQL Server especificado deve ser um membro do **sysadmin** fixa a função de servidor ou um membro do **replmonitor** função de banco de dados fixa no banco de dados de distribuição.  
  
5.  O nome do publicador e distribuidor são exibidos no **Iniciar o monitoramento nos seguintes Publicadores** grade.  
  
6.  Para especificar opções de atualização e conexão com o Publicador, selecione o Publicador na grade e modifique as opções, se necessário. Para obter mais informações sobre opções de atualização, consulte [cache, atualização e monitorar o desempenho da replicação](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selecione o grupo no qual o Publicador deverá ser exibido no Replication Monitor. Para criar um novo grupo, clique em **novo grupo**, e insira um nome de grupo, selecione o grupo no **Mostrar esses Publicadores no seguinte grupo** lista.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para adicionar um Editor Oracle  
  
1.  Clique com botão direito do **Replication Monitor** nó ou um editor de nó no painel à esquerda do grupo e, em seguida, clique em **Adicionar publicador**.  
  
2.  Na **Adicionar publicador** caixa de diálogo, clique em **Add**, e, em seguida, clique em **Adicionar editor Oracle**.  
  
3.  No **conectar ao servidor** caixa de diálogo, digite o nome do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] distribuidor associado ao editor Oracle e, em seguida, selecione o tipo de autenticação. Se você selecionar **autenticação do SQL Server**, insira um logon e senha. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou um logon do SQL Server especificado deve ser um membro do **sysadmin** fixa a função de servidor ou um membro do **replmonitor** função de banco de dados fixa no banco de dados de distribuição.  
  
4.  Clique em **Conectar**.  
  
5.  O nome do publicador e distribuidor são exibidos no **Iniciar o monitoramento nos seguintes Publicadores** grade.  
  
6.  Para especificar opções de atualização e conexão com o Publicador, selecione o Publicador na grade e modifique as opções, se necessário. Para obter mais informações sobre opções de atualização, consulte [cache, atualização e monitorar o desempenho da replicação](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selecione o grupo no qual o Publicador deverá ser exibido no Replication Monitor. Para criar um novo grupo, clique em **novo grupo**, e insira um nome de grupo, selecione o grupo no **Mostrar esses Publicadores no seguinte grupo** lista.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para adicionar um ou mais Publicadores que usam o mesmo Distribuidor  
  
1.  Clique com botão direito do **Replication Monitor** nó ou um editor de nó no painel à esquerda do grupo e, em seguida, clique em **Adicionar publicador**.  
  
2.  Na **Adicionar publicador** caixa de diálogo, clique em **Add**, e, em seguida, clique em **especificar um distribuidor e adicionar seus Publicadores**.  
  
3.  No **conectar ao servidor** caixa de diálogo, digite o nome do distribuidor e, em seguida, selecione o tipo de autenticação. Se você selecionar **autenticação do SQL Server**, insira um logon e senha. As credenciais que você especificar serão salvas pelo Replication Monitor para usar ao conectar-se a esse servidor no futuro. A conta do Windows ou um logon do SQL Server especificado deve ser um membro do **sysadmin** fixa a função de servidor ou um membro do **replmonitor** função de banco de dados fixa no banco de dados de distribuição.  
  
4.  Clique em **Conectar**.  
  
5.  O nome do distribuidor e cada publicador são exibidos no **Iniciar o monitoramento nos seguintes Publicadores** grade. Se um Publicador já foi adicionado ao Replication Monitor, não será exibido na grade.  
  
6.  Para especificar opções de atualização e conexão com o Publicador, selecione o Publicador na grade e modifique as opções, se necessário. Para obter mais informações sobre opções de atualização, consulte [cache, atualização e monitorar o desempenho da replicação](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Selecione o grupo no qual os Publicadores deverão ser exibidos no Replication Monitor. Para criar um novo grupo, clique em **novo grupo**, e insira um nome de grupo, selecione o grupo no **Mostrar esses Publicadores no seguinte grupo** lista.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para modificar as configurações para o Publicador e o Grupo do publicador  
  
1.  Clique com botão direito um publicador no painel esquerdo e, em seguida, clique em **configurações do publicador**.  
  
2.  Faça as alterações no **configurações do publicador** caixa de diálogo:  
  
    -   Para alterar as credenciais que o Monitor de replicação usa para se conectar a um servidor, clique em **conexão do publicador** ou **conexão do distribuidor**, e, em seguida, insira as credenciais no **conectar ao servidor** caixa de diálogo.  
  
    -   Para mover um publicador de um grupo para outro, selecione o Editor no **Iniciar o monitoramento nos seguintes Publicadores** grade e selecione o novo grupo no **Mostrar esses Publicadores no seguinte grupo** lista.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para remover o Publicador do Replication Monitor  
  
1.  Clique com o botão direito do mouse em um Publicador no painel esquerdo.  
  
2.  Clique em **Remover**.  
  
### Para adicionar um Grupo do publicador ao Replication Monitor  
  
1.  Só podem ser criados Grupos do publicador ao adicionar um Publicador ou modificar as configurações de um Publicador. Para obter mais informações, consulte os procedimentos sobre como adicionar um Publicador.  
  
### Para remover um grupo do Publicador do Replication Monitor  
  
1.  Mova todos os Publicadores para um grupo diferente ou remova-os do Replication Monitor. Para obter mais informações, consulte os procedimentos anteriores neste tópico.  
  
2.  Clique com botão direito do grupo do publicador e, em seguida, clique em **Remover**.  
  
## Consulte também  
 [Configurar a distribuição](../../../relational-databases/replication/configure-distribution.md)   
 [Replicação de monitoramento](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  