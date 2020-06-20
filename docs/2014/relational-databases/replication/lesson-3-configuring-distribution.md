---
title: 'Lição 3: Configurando a distribuição | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: rothja
ms.author: jroth
ms.openlocfilehash: 28df67dad52bcd11a18fc5deb42a6725700dde5a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065944"
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
  
3.  Na página **distribuidor** , selecione **'** _\<ServerName>_ **' atuará como seu próprio distribuidor; SQL Server criará um banco de dados de distribuição e um log**e, em seguida, clique em **Avançar**.  
  
4.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, na página inicial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agent**, selecione **Sim** para configurar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar automaticamente. Clique em **Próximo**.  
  
5.  Insira **\\\\** \<_Machine_Name> _**\repldata** na caixa de texto **pasta de instantâneo** , em que \<*Machine_Name> * é o nome do Publicador e clique em **Avançar**.  
  
6.  Aceite os valores padrão das páginas restantes do assistente.  
  
7.  Clique em **Concluir** para ativar a distribuição.  
  
### <a name="setting-database-permissions-at-the-publisher"></a>Definindo permissões de banco de dados no Publicador  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , expanda **segurança**, clique com o botão direito do mouse em **logons**e selecione **novo logon**.  
  
2.  Na página **geral** , clique em **Pesquisar**, insira \<_Machine_Name> _**\ repl_snapshot** na caixa **Inserir o nome do objeto a ser selecionado** , em que \<*Machine_Name> * é o nome do servidor do Publicador local, clique em **verificar nomes**e em **OK**.  
  
3.  Na página **mapeamento de usuário** , na lista **Usuários mapeados para este logon** , selecione a **distribuição** e os [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] bancos de dados.  
  
     Na lista **associação da função de banco de dados** , selecione a `db_owner` função para o logon para ambos os bancos.  
  
4.  Clique em **OK** para criar o logon.  
  
5.  Repita as Etapas 1a 4 para criar um logon para a conta repl_logreader local. Esse logon também deve ser mapeado para os usuários que são membros da `db_owner` função de banco de dados fixa na **distribuição** e no bancos de dados **AdventureWorks** .  
  
6.  Repita as Etapas 1a 4 para criar um logon para a conta repl_distribution local. Esse logon deve ser mapeado para um usuário que seja membro da função de `db_owner` banco de dados fixa no banco de dados de **distribuição** .  
  
7.  Repita as etapas 1a 4 para criar um logon para a conta repl_merge local. Esse logon deve ter mapeamentos de usuário nos bancos de dados **distribuição** e **AdventureWorks** .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a distribuição](configure-distribution.md)   
 [Modelo de segurança do agente de replicação](security/replication-agent-security-model.md)  
  
  
