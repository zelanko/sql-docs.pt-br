---
title: SQL Server Configuration Manager | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], managing
- network protocols [SQL Server], managing
- Client Network Utility
- accounts [SQL Server]
- SQL Server Configuration Manager
- Server Network Utility
- accounts [SQL Server], services
- services [SQL Server], managing
- tools [SQL Server], SQL Server Configuration Manager
- configuration manager [SQL Server]
ms.assetid: e6beaea4-164c-4078-95ae-b9e28b0aefe8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 123f0fcececee98826bf70b929a9857bbaff32dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044451"
---
# <a name="sql-server-configuration-manager"></a>SQL Server Configuration Manager
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager é uma ferramenta para gerenciar os serviços associados ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], configurar os protocolos de rede usados pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e para gerenciar a configuração de conectividade de rede de computadores cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] O Configuration Manager é um snap-in do [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console que está disponível no menu Iniciar ou pode ser adicionado a qualquer outra exibição do Console de Gerenciamento do [!INCLUDE[msCoName](../includes/msconame-md.md)] . [!INCLUDE[msCoName](../includes/msconame-md.md)]O console de gerenciamento (MMC. exe) usa o arquivo SQLServerManager10. msc na pasta system32 do Windows [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para abrir Configuration Manager.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] O Configuration Manager e o SQL Server Management Studio usam o WMI (Instrumentação de Gerenciamento do Windows) para exibir e modificar algumas das propriedades de servidor. O WMI fornece uma forma unificada para fazer interface com as chamadas de API que gerenciam as operações de registro solicitadas pelas ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e para fornecer um controle e manipulação melhorados sobre os serviços selecionados de SQL do componente de snap-in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager. Para obter informações sobre como configurar permissões relacionadas ao WMI, veja [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md).  
  
> [!NOTE]
>  Como o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
> 
>  -   **Windows 10**:  
>          Para abrir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, na **página inicial**, digite SQLServerManager12. msc (para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] substitua 12 por um número menor. Clique em SQLServerManager12.msc para abrir o Configuration Manager. Para fixar o Configuration Manager na página inicial ou na barra de tarefas, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **abrir local do arquivo**. No explorador de arquivos do Windows, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **fixar para iniciar** ou **fixar na barra de tarefas**.  
> -   **Windows 8**:  
>          Para abrir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar** , em **aplicativos**, digite **SQLServerManager\<versão>. msc** , como `SQLServerManager12.msc`e pressione **Enter**.  
  
 Para iniciar, interromper, pausar, retomar ou configurar os serviços em outro computador usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, veja [Conectar-se a um outro computador &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/scm-services-connect-to-another-computer.md).  
  
## <a name="managing-services"></a>Gerenciando serviços  
 Use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager para iniciar, pausar, retomar ou interromper os serviços, para exibir as propriedades de serviço ou para alterar as propriedades de serviço.  
  
 Use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager para iniciar o [!INCLUDE[ssDE](../includes/ssde-md.md)] usando parâmetros de inicialização.  Para obter mais informações, veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
## <a name="changing-the-accounts-used-by-the-services"></a>Alterando as contas usadas pelos serviços  
 Gerencie os serviços do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.  
  
> [!IMPORTANT]  
>  Sempre use as ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, para alterar a conta usada pelos serviços [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent, ou para alterar a senha da conta. Além de alterar o nome da conta, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration manager executa configurações adicionais, como definição de permissões no Registro do Windows de modo que a nova conta possa ler as definições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Outras ferramentas como o Gerenciador de Controle de Serviços do Windows podem alterar o nome da conta mas não alteram as definições vinculadas a ela. Se o serviço não puder acessar a parte do registro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o serviço pode não iniciar corretamente.  
  
 Como benefício adicional, as senhas alteradas com o uso do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, SMO ou WMI passam a vigorar imediatamente sem reiniciar o serviço.  
  
## <a name="manage-server--client-network-protocols"></a>Gerenciar protocolos de rede do servidor & cliente  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager permite configurar protocolos de rede de cliente e servidor e opções de conectividade. Depois que os protocolos corretos são habilitados, normalmente não é preciso alterar as conexões de rede de servidor. No entanto, você pode usar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager se precisar reconfigurar as conexões do servidor de modo que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] escute um determinado protocolo de rede, porta ou pipe. Para obter mais informações sobre como habilitar protocolos, veja [Habilitar ou desabilitar um protocolo de rede de servidor](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md). Para obter informações sobre como habilitar o acesso a protocolos por meio de um firewall, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] O Configuration Manager permite que você gerencie os protocolos de rede de servidor e cliente, incluindo o recurso de impor a criptografia do protocolo, exibir as propriedades do alias ou habilitar/desabilitar um protocolo.  
  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager permite que você crie ou remova um alias, altere a ordem em que os protocolos são usados ou exiba as propriedades do alias de um servidor, incluindo:  
  
-   Alias de servidor: alias do servidor usado para o computador ao qual o cliente está se conectando.  
  
-   Protocolo – o protocolo de rede usado para a entrada de configuração.  
  
-   Parâmetros de Conexão – os parâmetros associados ao endereço de conexão da configuração do protocolo de rede.  
  
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager também permite que você visualize as informações sobre as instâncias de cluster de failover, apesar do Administrador de Cluster dever ser usado para algumas ações como iniciar e interromper os serviços.  
  
### <a name="available-network-protocols"></a>Protocolos de rede disponíveis  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dá suporte a protocolos de Memória Compartilhada, TCP/IP e Pipes Nomeados. Para obter informações sobre como escolher protocolos de rede, consulte [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md). 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não dá suporte aos protocolos de rede VIA, Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk ou NWLink IPX/SPX. Os clientes que se conectavam anteriormente usando esses protocolos devem selecionar um protocolo diferente para conectar-se com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você não pode usar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager para configurar o proxy de WinSock. Configurar o proxy de WinSock, consulte sua documentação do Servidor ISA.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Tópicos de instruções sobre gerenciamento de serviços &#40;SQL Server Configuration Manager&#41;](../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
 [Definir uma instância do SQL Server para iniciar automaticamente &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)  
  
 [Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)  
  
  
