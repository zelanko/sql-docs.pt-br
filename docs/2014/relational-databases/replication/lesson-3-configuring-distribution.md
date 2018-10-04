---
title: 'Lição 3: Configurando a distribuição | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7fbfb6d659aa8bc96ebc13ad0a3b89df750c5f95
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167466"
---
# <a name="lesson-3-configuring-distribution"></a>Lição 3: Configurando a distribuição
  Nesta lição você configurará a distribuição no Publicador e definirá as permissões necessárias nos bancos de dados de publicação e distribuição. Se você já tiver configurado o Distribuidor, antes de começar a lição será necessário desabilitar primeiramente a publicação e a distribuição. Não faça isto se for preciso manter uma topologia de replicação existente.  
  
 A configuração de um Publicador com um Distribuidor remoto está fora do escopo deste tutorial.  
  
### <a name="configuring-distribution-at-the-publisher"></a>Configurando a distribuição no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e clique em **Configurar Distribuição**.  
  
    > [!NOTE]  
    >  Se você se conectou ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **localhost** em vez do nome de servidor real, receberá um aviso de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar ao **'localhost'** do servidor. Clique em **OK** na caixa de diálogo de aviso. Na caixa de diálogo **Conectar ao Servidor** , altere o **Nome do Servidor** de **localhost** para o nome do seu servidor. Clique em **Conectar**.  
  
     O Assistente para Configuração de Distribuição é iniciado.  
  
3.  Sobre o **distribuidor** página, selecione **'***\<ServerName >***' atuará como seu próprio distribuidor; SQL Server criará um banco de dados de distribuição e de log**e, em seguida, clique em **próxima**.  
  
4.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, na página inicial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agent**, selecione **Sim** para configurar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar automaticamente. Clique em **Avançar**.  
  
5.  Insira **\\\\**\<*Machine_Name>***\repldata** na caixa de texto **Pasta de instantâneos**, em que \<*Machine_Name>* é o nome do Publicador e, em seguida, clique em **Avançar**.  
  
6.  Aceite os valores padrão das páginas restantes do assistente.  
  
7.  Clique em **Concluir** para ativar a distribuição.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Definindo permissões de banco de dados no Publicador  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Segurança**, clique com o botão direito do mouse em **Logons**e selecione **Novo Logon**.  
  
2.  Na página **Geral**, clique em **Pesquisar**, insira \<*Machine_Name>***\repl_snapshot** na caixa **Inserir o nome do objeto a ser selecionado**, em que \<*Machine_Name>* é o nome do servidor do Publicador local. Em seguida, clique em **Verificar Nomes** e em **OK**.  
  
3.  Na página **Mapeamento de Usuário** , na lista **Usuários mapeados para este logon** , selecione os bancos de dados de **distribuição** e de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
     No **associação de função de banco de dados** lista select a `db_owner` função para o logon para ambos os bancos de dados.  
  
4.  Clique em **OK** para criar o logon.  
  
5.  Repita as Etapas 1a 4 para criar um logon para a conta repl_logreader local. Esse logon também deve ser mapeado para os usuários que são membros do `db_owner` função de banco de dados fixa na **distribuição** e **AdventureWorks** bancos de dados.  
  
6.  Repita as Etapas 1a 4 para criar um logon para a conta repl_distribution local. Esse logon deve ser mapeado para um usuário que seja membro do `db_owner` função de banco de dados fixa na **distribuição** banco de dados.  
  
7.  Repita as etapas 1a 4 para criar um logon para a conta repl_merge local. Esse logon deve ter mapeamentos de usuário nos bancos de dados **distribuição** e **AdventureWorks** .  
  
## <a name="see-also"></a>Consulte também  
 [Configurar Distribuição](configure-distribution.md)   
 [Replication Agent Security Model](security/replication-agent-security-model.md)  
  
  
