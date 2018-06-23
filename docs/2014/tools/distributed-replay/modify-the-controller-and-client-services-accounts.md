---
title: Modificar as contas dos serviços controlador e cliente | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 44a73ddb-18ad-415c-bfbe-126ab2e3290b
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f9bc20a70899e84dacb4f7bfbadf0a0f26f88ffa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009875"
---
# <a name="modify-the-controller-and-client-services-accounts"></a>Modificar as contas dos serviços controlador e cliente
  Neste tópico, você aprenderá a modificar o controlador Distributed Replay e as contas de serviço cliente e depois reaplicar as ACLs (listas de controle de acesso).  
  
### <a name="to-start-or-stop-the-distributed-replay-services-using-computer-management"></a>Para iniciar ou parar os serviços Distributed Replay usando o gerenciamento do computador  
  
1.  No computador em que os serviços Distributed Replay estão instalados, no prompt de comando, digite `dcomcnfg`.  
  
2.  Clique duas vezes em **Serviços**, role para baixo e clique com o botão direito do mouse em **<nome do serviço> do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay\<** e clique em **Iniciar** ou em **Parar**.  
  
### <a name="to-modify-the-distributed-replay-controller-service"></a>Para modificar o serviço controlador Distributed Replay  
  
1.  No computador controlador, pare o serviço controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay.  
  
2.  Em **Serviços**, clique com o botão direito do mouse em **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay**e selecione **Propriedades**.  
  
3.  Na janela **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay** , na guia **Logon** , selecione **Esta conta**, digite ou clique em **Procurar** para inserir a nova conta de logon e clique em **OK**.  
  
     **Importante**: Quando você configura o controlador Distributed Replay, pode especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:  
  
    -   Conta de usuário do domínio  
  
    -   Conta de usuário local criada pelo usuário  
  
    -   Administrador  
  
    -   Conta virtual e MSA (Conta de Serviço Gerenciada)  
  
    -   Serviços de rede, serviços locais e sistema  
  
     Não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).  
  
4.  Inicie o serviço controlador Distributed Replay.  
  
### <a name="to-modify-the-distributed-replay-client-service"></a>Para modificar o serviço cliente do Distributed Replay  
  
1.  Antes de modificar o serviço cliente Distributed Replay, verifique se a conta do serviço cliente que você está alterando foi especificada durante a configuração (no parâmetro CTLRUSERS no computador controlador). Se a conta de serviço de cliente que você está alterando não foi especificada durante a instalação, execute as etapas a seguir primeiro:  
  
    1.  Pare o serviço controlador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay.  
  
    2.  No computador do controlador no qual o serviço do controlador está instalado, no prompt de comando, digite `dcomcnfg`.  
  
    3.  Na janela **Serviços de Componente**, navegue até **Raiz do Console -> Serviços de Componente -> Computadores -> Meu Computador -> Configuração de DCOM ->DReplayController**.  
  
    4.  Clique com o botão direito do mouse em **DReplayController** e clique em **Propriedades**.  
  
    5.  Na janela **Propriedades do DReplayController** , na guia **Segurança** , clique em **Editar** na seção **Permissões de Inicialização e Ativação** .  
  
    6.  Conceda à nova conta de logon do serviço cliente permissões de **Ativação Local e Remota** e clique em **OK**.  
  
    7.  Clique em **Editar** na seção **Permissões de Acesso** e conceda à nova conta de logon do serviço cliente permissões de **Acesso Local e Remoto** e clique em **OK**.  
  
    8.  Clique em **OK** para fechar a janela **Propriedades do DReplayController** .  
  
    9. No computador controlador, adicione a conta de logon do serviço cliente alterado para o grupo **Usuários COM Distribuídos** .  
  
    10. Inicie o serviço controlador SQL Server Distributed Replay.  
  
2.  Pare o serviço cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay.  
  
3.  Na janela **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay** , na guia **Logon** , selecione **Esta conta**, digite ou clique em **Procurar** para inserir a nova conta de logon e clique em **OK**.  
  
4.  Inicie o serviço cliente Distributed Replay.  
  
  