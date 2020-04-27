---
title: Alterar a conta de inicialização do serviço para SQL Server (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a2a830ad4d6fa87cd754910baf8be53216086cab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62810427"
---
# <a name="change-the-service-startup-account-for-sql-server-sql-server-configuration-manager"></a>Alterar a conta de inicialização de serviço do SQL Server (SQL Server Configuration Manager)
  Este tópico descreve como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para alterar as opções de inicialização dos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as contas de serviço usadas por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o PowerShell. Para obter mais informações sobre como selecionar uma conta de serviço adequada, consulte [Configurar contas de serviço e permissões do Windows](configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  Quando você altera a conta de inicialização do serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o [!INCLUDE[ssDE](../../includes/ssde-md.md)]) deve ser reiniciado para que a alteração entre em vigor. Quando o serviço é reinicializado, todos os bancos de dados associados com aquela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ficarão indisponíveis até que o serviço seja reiniciado com êxito. Se for necessário alterar a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, faça isso durante a manutenção regular agendada ou quando os bancos de dados puderem ser colocados offline sem interromper as operações diárias.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Servidores clusterizados  
  
     A alteração da conta de serviço usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser executada no nó ativo do cluster do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Quando executada no Windows Server 2008 (em uma configuração não padrão que usa grupos de domínio), a alteração da conta de serviço usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent requer o Gerenciador de Configurações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colocando os grupos offline.  
  
-   Atualização de SKU (SKU do[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] para não Express)  
  
     Durante a instalação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é configurado para usar a conta de Serviço de Rede, mas desabilitado. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager pode alterar a conta atribuída para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, mas o serviço não pode ser habilitado ou iniciado. Depois da atualização da SKU do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] para não Express, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não é habilitado automaticamente, mas pode ser habilitado quando necessário usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e alterando o modo de início do serviço para Manual ou Automático.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>Para alterar a conta de inicialização do serviço do SQL Server  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **página inicial**, digite SQLServerManager12. msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua 12 por um número menor. Clique em SQLServerManager12.msc para abrir o Configuration Manager. Para fixar o Configuration Manager na página inicial ou na barra de tarefas, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **abrir local do arquivo**. No explorador de arquivos do Windows, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **fixar para iniciar** ou **fixar na barra de tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar** , em **aplicativos**, digite **SQLServerManager\<versão>. msc** , como `SQLServerManager12.msc`e pressione **Enter**.  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, clique em **Serviços do SQL Server**.  
  
3.  No painel de detalhes clique com o botão direito do mouse no nome da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja alterar a conta de inicialização do serviço e em seguida clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server \< ***InstanceName***>** , clique na guia **logon** e selecione um tipo de conta **fazer logon como** .  
  
5.  Após selecionar a nova conta de inicialização do serviço, clique em **OK**.  
  
     Uma caixa de mensagem pergunta se você quer reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Clique em **Sim**e feche o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
