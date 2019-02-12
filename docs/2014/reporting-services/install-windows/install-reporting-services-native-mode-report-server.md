---
title: Instalar o Reporting Services servidor de relatório de modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f0c52d22f9592d149f25f6ae8a6de2813dfcba1d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043287"
---
# <a name="install-reporting-services-native-mode-report-server"></a>Instalar o servidor de relatórios de modo nativo do Reporting Services
  Um servidor de relatório do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode ser instalado do assistente de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou da linha de comando. No assistente de instalação, você pode selecionar para 1) instalar arquivos e configurar o servidor com as configurações padrão ou 1) somente instalar os arquivos e o servidor não é configurado pelo assistente de instalação. Esse tópico analisa a *Configuração padrão para o modo nativo* em que a Instalação instala e configura uma instância do servidor de relatório. Depois que a Instalação for concluída, o servidor de relatório estará em execução e pronto para uso. Um servidor de relatório no modo nativo é executado como um servidor de aplicativo autônomo. O modo nativo é o padrão de servidor.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
-   [O que é a configuração padrão?](#bkmk_whatisdefaultconfiguration)  
  
-   [Quando instalar a configuração padrão para o modo nativo](#bkmk_whentoinstalldefaultconfig)  
  
-   [Requisitos](#bkmk_requirements)  
  
-   [Reservas de URL padrão](#bkmk_defaultURLreservations)  
  
-   [Instalar o modo nativo com o Assistente de instalação do SQL Server](#bkmk_installwithwizard)  
  
-   [Instalar o modo nativo com a linha de comando](#bkmk_commandline)  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> O que é a configuração padrão?  
 A Instalação instala os seguintes recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quando você seleciona a configuração padrão para a opção de modo nativo:  
  
-   O serviço Servidor de Relatório (que inclui o serviço Web do Servidor de Relatório, o aplicativo de processamento em segundo plano e o Gerenciador de Relatórios)  
  
-   O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Os utilitários de linha de comando do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsconfig.exe, rskeymgmt.exe e rs.exe)  
  
 Essa opção não é aplicada a recursos compartilhados, tais como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], que devem ser especificados como itens separados se você desejar instalá-los.  
  
 A Instalação configura o seguinte para uma instalação de servidor de relatório no modo nativo:  
  
-   Conta de serviço para o serviço Servidor de Relatório.  
  
-   URL do serviço Web Servidor de Relatórios.  
  
-   URL do Gerenciador de Relatórios.  
  
-   Banco de dados do Servidor de Relatório.  
  
-   Acesso da conta de serviço aos bancos de dados do servidor de relatório.  
  
-   Conexão DSN para banco de dados do servidor de relatório.  
  
 A Instalação não configura a conta de execução autônoma, o email do servidor de relatório, o backup das chaves de criptografia ou uma implantação de expansão. Você pode usar a ferramenta Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar essas propriedades. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> Quando instalar a configuração padrão para o modo nativo  
 Uma configuração padrão instala o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um estado operacional para que você possa usar o servidor de relatório imediatamente após a Instalação ser concluída. Especifique esse modo quando desejar economizar etapas pela eliminação de quaisquer tarefas de configuração necessárias, que de outra maneira precisariam ser executadas na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A instalação da configuração padrão não garante que o servidor de relatório funcionará depois que a Instalação for concluída. É possível que as URLs padrão não sejam registradas quando o serviço for iniciado. Sempre teste sua instalação para verificar se o serviço é iniciado e executado como esperado.  
  
##  <a name="bkmk_requirements"></a> Requisitos  
 A opção de configuração padrão usa valores padrão para definir as configurações básicas necessárias para tornar operacional um servidor de relatório. Ela tem os seguintes requisitos:  
  
-   O seu hardware deve atender aos requisitos mínimos de hardware e software para executar o Microsoft SQL Server. Para obter mais informações, consulte [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] devem ser instalados juntos na mesma instância. A instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] hospeda o banco de dados do servidor de relatório que a Instalação cria e configura.  
  
-   A conta de usuário utilizada para executar a instalação deve ser membro do grupo local Administradores e ter permissão para acessar e criar bancos de dados na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda os bancos de dados do servidor de relatório.  
  
-   A instalação deve poder usar os valores padrão para reservar as URLs que dão acesso ao servidor de relatório e ao Gerenciador de Relatórios. Esses valores são a porta 80, um curinga forte e os nomes de diretório virtual no formato **ReportServer_\<***instance_name***>** e **Reports_\<***instance_name***>**.  
  
-   A Instalação deve poder usar os valores padrão para criar os bancos de dados de servidor de relatório. Esses valores são **ReportServer** e **ReportServerTempDB**. Se você tiver bancos de dados existentes de uma instalação anterior, a instalação será bloqueada porque não poderá configurar o servidor de relatório na configuração padrão para o modo nativo. Você deve renomear, mover ou excluir os bancos de dados para desbloquear a instalação.  
  
 Se o computador não atender a todos os requisitos de uma instalação padrão, você deverá instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo somente arquivos e usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurá-lo após o término da instalação.  
  
 Não tente reconfigurar o computador apenas para permitir que uma instalação padrão continue. Isso poderia requerer várias horas de trabalho, eliminando efetivamente o benefício de economia de tempo que a opção de instalação fornece. A melhor solução é instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo somente arquivos e configurar o servidor de relatório para usar valores específicos.  
  
##  <a name="bkmk_defaultURLreservations"></a> Reservas de URL padrão  
 As reservas de URL são compostas de um prefixo, nome de host, porta e diretório virtual:  
  
|Parte|Descrição|  
|----------|-----------------|  
|Prefixo|O prefixo padrão é HTTP. Se você instalou anteriormente um certificado de protocolo SSL, a Instalação tentará criar reservas de URL que usem o prefixo HTTPS.|  
|Nome do host|O nome de host padrão é um curinga forte (+). Especifica que o servidor de relatório aceitará qualquer solicitação HTTP na porta designada para qualquer nome de host é resolvido para o computador, incluindo http://\<computername > / reportserver, http://localhost/reportserver, ou http://\<IPAddress > / ReportServer.|  
|Porta|A porta padrão é 80. Observe que, se você usar qualquer porta que não seja a 80, precisará adicioná-la explicitamente à URL quando abrir um aplicativo Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma janela do navegador.|  
|Diretório virtual|Por padrão, os diretórios virtuais são criados no formato de ReportServer_\<*nome_instância*> para o serviço Web servidor de relatórios e Reports_\<*nome_instância*> Gerenciador de relatórios. Para o serviço Web Servidor de Relatórios, o diretório virtual padrão é **reportserver**. Para o Gerenciador de Relatórios, o diretório virtual padrão é **reports**.|  
  
 Um exemplo de cadeia de caracteres de URL completa poderia ser como segue:  
  
-   http://+:80/reportserver, fornece acesso ao servidor de relatório.  
  
-   http://+:80/reports, fornece acesso ao Gerenciador de relatórios.  
  
##  <a name="bkmk_installwithwizard"></a> Instalar o modo nativo com o Assistente de instalação do SQL Server  
 A lista a seguir descreve as etapas específicas e as opções do  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você seleciona no Assistente de Instalação do SQL Server. A lista não descreve cada página que você verá no assistente de instalação, somente as páginas relacionadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que fazem parte de uma instalação do modo nativo.  
  
1.  Na página **Função de instalação** , selecione **Instalação de recurso do SQL Server**.  
  
     ![Instalação de recurso do SQL Server para a função de instalação](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalação de recurso do SQL Server para a função de instalação")  
  
2.  Na página **Seleção de Recurso** , selecione o seguinte:  
  
    -   **Serviços do Mecanismo de Banco de Dados**, a menos que uma instância do mecanismo do banco de dados já esteja instalada.  
  
    -   **Reporting Services-Native**.  
  
    -   **Ferramentas de gerenciamento - básico**. As ferramentas de gerenciamento não são necessárias, mas são recomendadas a menos que você tenha alguma outra instalação das ferramentas de gerenciamento. A opção de configuração padrão resultará em um servidor de relatório está funcionando, mas você talvez queira alterar as opções de configuração em uma data posterior. Algumas opções como 'Meus relatórios' são gerenciadas por meio de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
     ![Seleção do modo nativo do SSRS na seleção de recursos](../../../2014/sql-server/install/media/rs-setupfeatureselection-native-withcircles.gif "Seleção do modo nativo do SSRS na seleção de recursos")  
  
3.  Se você planejar usar o recurso de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , na página **Configuração de Servidor** , verifique se o SQL Server Agent está configurado para o tipo de inicialização **Automático** .  
  
4.  Na página **Configuração do Reporting Services** , selecione **Instalar e Configurar**.  
  
     ![Configuração do modo nativo do SSRS](../../../2014/sql-server/install/media/rs-setupconfiguration-native-with-circles.gif "Configuração do modo nativo do SSRS")  
  
5.  Depois que o assistente de instalação do SQL Server estiver concluído, verifique a instalação padrão do modo nativo usando as etapas básicas a seguir.  
  
    -   Abra o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e confirme que você pode conectar-se ao servidor de relatório.  
  
    -   Abra seu navegador com privilégios administrativos e conecte-se ao Gerenciador de Relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , por exemplo `http://loclahost/Reports`.  
  
    -   Abra seu navegador com privilégios administrativos e conecte-se à página do servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por exemplo,  `http://loclahost/ReportServer`  
  
 Para obter mais informações, consulte a seção Nativa dos dois tópicos a seguir:  
  
 [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Solucionar um problema da instalação do Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
##  <a name="bkmk_commandline"></a> Instalar o modo nativo com a linha de comando  
 O exemplo a seguir inclui o serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] porque ele é necessário para uma configuração padrão.  
  
```  
setup /q /ACTION=install /FEATURES=SQL,RS,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS"   
/RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK   
SERVICE" /RSSVCSTARTUPTYPE="Manual" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
 Para obter mais informações e exemplos, consulte [Prompt de comando instalação do Reporting Services SharePoint Mode e modo nativo](../../reporting-services/install-windows/install-reporting-services-at-the-command-prompt.md) e [instalar o SQL Server 2014 do Prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar um problema da instalação do Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Instalação somente de arquivos &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
 [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Configurar conexões SSL em um servidor de relatórios de modo nativo](../security/configure-ssl-connections-on-a-native-mode-report-server.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Instalação de Início Rápido do SQL Server 2014](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
