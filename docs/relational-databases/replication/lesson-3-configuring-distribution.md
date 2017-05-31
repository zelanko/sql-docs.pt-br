---
title: "Lição 3: Configurando a distribuição | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e582c5fb7853c69a083755a944bd3922d0d4c5af
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-3-configuring-distribution"></a>Lição 3: Configurando a distribuição
Nesta lição você configurará a distribuição no Publicador e definirá as permissões necessárias nos bancos de dados de publicação e distribuição. Se você já tiver configurado o Distribuidor, antes de começar a lição será necessário desabilitar primeiramente a publicação e a distribuição. Não faça isto se for preciso manter uma topologia de replicação existente.  
  
A configuração de um Publicador com um Distribuidor remoto está fora do escopo deste tutorial.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Configurando a distribuição no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e clique em **Configurar Distribuição**.  
  
    > [!NOTE]  
    > Se você se conectou ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **localhost** em vez do nome de servidor real, receberá um aviso de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar ao **'localhost'**do servidor. Clique em **OK** na caixa de diálogo de aviso. Na caixa de diálogo **Conectar ao Servidor** , altere o **Nome do Servidor** de **localhost** para o nome do seu servidor. Clique em **Conectar**.  
  
    O Assistente para Configuração de Distribuição é iniciado.  
  
3.  Na página **Distribuidor**, a seleção de “ServerName” atuará como seu próprio Distribuidor; o SQL Server criará um banco de dados de distribuição e um log**. Depois, clique em **Avançar**.  
  
4.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, na página inicial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agent**, selecione **Sim** para configurar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar automaticamente. Clique em **Avançar**.  
  
5.  Insira **\\\\**\<*Machine_Name>***\repldata** na caixa de texto **Pasta de instantâneos**, em que \<*Machine_Name>* é o nome do Publicador e, em seguida, clique em **Avançar**.  
  
6.  Aceite os valores padrão das páginas restantes do assistente.  
  
7.  Clique em **Concluir** para ativar a distribuição.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Definindo permissões de banco de dados no Publicador  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.  
  
2.  Na página **Geral**, clique em **Pesquisar**, insira \<*Machine_Name>***\repl_snapshot** na caixa **Inserir o nome do objeto a ser selecionado**, em que \<*Machine_Name>* é o nome do servidor do Publicador local. Em seguida, clique em **Verificar Nomes** e em **OK**.  
  
3.  Na página **Mapeamento de Usuário** , na lista **Usuários mapeados para este logon** , selecione os bancos de dados de **distribuição** e de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
    Na lista **Associação à função de banco de dados** selecione a função **db_owner** para o logon de ambos os bancos de dados.  
  
4.  Clique em **OK** para criar o logon.  
  
5.  Repita as Etapas 1a 4 para criar um logon para a conta repl_logreader local. Esse logon também deve ser mapeado para usuários que são membros da função de bancos de dados fixa **db_owner** na **distribuição** e nos bancos de dados **AdventureWorks** .  
  
6.  Repita as Etapas 1a 4 para criar um logon para a conta repl_distribution local. É necessário também mapear esse logon para um usuário que seja membro da função de banco de dados fixa **db_owner** no banco de dados da **distribuição** .  
  
7.  Repita as etapas 1a 4 para criar um logon para a conta repl_merge local. Esse logon deve ter mapeamentos de usuário nos bancos de dados **distribuição** e **AdventureWorks** .  
  
## <a name="see-also"></a>Consulte também  
[Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
[Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)  
  
  
  

