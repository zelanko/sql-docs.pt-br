---
title: Serviços SCM – alterar a conta de inicialização do serviço | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6ee798510dd33a5df695c2be9f62b37bb7314341
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40175076"
---
# <a name="scm-services---change-the-service-startup-account"></a>Serviços SCM – alterar a conta de inicialização do serviço
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como usar o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alterar as opções de inicialização dos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as contas de serviço usadas pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o PowerShell. Para obter mais informações sobre como selecionar uma conta de serviço adequada, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  Quando você altera a conta de inicialização do serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o [!INCLUDE[ssDE](../../includes/ssde-md.md)]) deve ser reiniciado para que a alteração entre em vigor. Quando o serviço é reinicializado, todos os bancos de dados associados com aquela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ficarão indisponíveis até que o serviço seja reiniciado com êxito. Se for necessário alterar a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, faça isso durante a manutenção regular agendada ou quando os bancos de dados puderem ser colocados offline sem interromper as operações diárias.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Servidores clusterizados  
  
     A alteração da conta de serviço usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser executada no nó ativo do cluster do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Quando executada no Windows Server 2008 (em uma configuração não padrão que usa grupos de domínio), a alteração da conta de serviço usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent requer o Gerenciador de Configurações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colocando os grupos offline.  
  
-   Atualização de SKU (SKU do[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] para não Express)  
  
     Durante a instalação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é configurado para usar a conta de Serviço de Rede, mas desabilitado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager pode alterar a conta atribuída para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, mas o serviço não pode ser habilitado ou iniciado. Depois da atualização da SKU do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] para não Express, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não é habilitado automaticamente, mas pode ser habilitado quando necessário usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e alterando o modo de início do serviço para Manual ou Automático.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>Para alterar a conta de inicialização do serviço do SQL Server  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **Página Inicial**, digite SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , substitua 13 por um número menor. Clicar em SQLServerManager13.msc abre o Configuration Manager. Para fixar o Configuration Manager na Página Inicial ou na Barra de Tarefas, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Abrir local do arquivo**. No Explorador de Arquivos do Windows, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Fixar na Tela Inicial** ou **Fixar na Barra de Tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager\<versão>.msc**, como **SQLServerManager13.msc** e pressione **Enter**.  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, clique em **Serviços do SQL Server**.  
  
3.  No painel de detalhes clique com o botão direito do mouse no nome da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja alterar a conta de inicialização do serviço e em seguida clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades de \<***instancename***> do SQL Server**, clique na guia **Logon** e selecione um tipo de conta **Fazer logon como**.  
  
5.  Após selecionar a nova conta de inicialização do serviço, clique em **OK**.  
  
     Uma caixa de mensagem pergunta se você quer reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Clique em **Sim**e feche o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
