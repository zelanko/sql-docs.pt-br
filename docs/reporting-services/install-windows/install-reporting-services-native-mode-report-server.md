---
title: Instalar o servidor de relatório no modo nativo do Reporting Services 2016 | Microsoft Docs
ms.custom: ''
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
caps.latest.revision: 68
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1e41f40025a7ccf883f2643baf538f4f045f5b65
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35322125"
---
# <a name="install-reporting-services-2016-native-mode-report-server"></a>Instalar o servidor de relatório no modo nativo do Reporting Services 2016

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Saiba como instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo nativo. Isso dará acesso a um [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] em que você pode gerenciar relatórios e outros itens.

> [!NOTE]
> Procurando o Servidor de Relatórios do Power BI? Consulte [Instalar o Servidor de Relatórios do Power BI](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

Um servidor de relatório do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é o modo de servidor padrão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e pode ser instalado por meio do assistente de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou da linha de comando. No assistente de instalação, você pode selecionar para instalar arquivos e configurar o servidor com as configurações padrão ou somente instalar os arquivos. Esse tópico analisa a *Configuração padrão para o modo nativo* em que a Instalação instala e configura uma instância do servidor de relatório. Depois de concluída a instalação, o servidor de relatório está em execução e pronto para uso para gerenciamento de relatórios e exibição de relatórios básicos.  Recursos adicionais como integração com o [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] e entrega de email com processamento de assinatura exigem configuração adicional.  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> Qual é a configuração padrão?  
 A Instalação instala os seguintes recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quando você seleciona a configuração padrão para a opção de modo nativo:  
  
-   O serviço Servidor de Relatório (que inclui o serviço Web do Servidor de Relatório, o aplicativo de processamento em segundo plano e o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] para exibir e gerenciar relatórios e permissões).  
  
-   O Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Os utilitários de linha de comando do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] rsconfig.exe, rskeymgmt.exe e rs.exe.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] agora são downloads separados.  
  
 A Instalação configura o seguinte para uma instalação de servidor de relatório no modo nativo:  
  
-   Conta de serviço para o serviço Servidor de Relatório.  
  
-   URL do serviço Web Servidor de Relatórios.  
  
-   A URL [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] .  
  
-   Banco de dados do Servidor de Relatório.  
  
-   Acesso da conta de serviço aos bancos de dados do servidor de relatório.  
  
-   Informações de conexão, também conhecidas como DSN, (nome da fonte de dados) para os bancos de dados do servidor de relatório.  
  
 A Instalação não configura a conta de execução autônoma, o email do servidor de relatório, o backup das chaves de criptografia ou uma implantação de expansão. Você pode usar a ferramenta Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar essas propriedades. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> Quando instalar a configuração padrão para o modo nativo  
 Uma configuração padrão instala o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um estado operacional para que você possa usar o servidor de relatório imediatamente após a Instalação ser concluída. Especifique esse modo quando desejar economizar etapas pela eliminação de quaisquer tarefas de configuração necessárias, que de outra maneira precisariam ser executadas na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A instalação da configuração padrão não garante que o servidor de relatório funcionará depois que a Instalação for concluída. É possível que as URLs padrão não sejam registradas quando o serviço for iniciado. Sempre teste sua instalação para verificar se o serviço é iniciado e executado como esperado.  Confira [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).
  
##  <a name="bkmk_requirements"></a> Requisitos  
 A opção de configuração padrão usa valores padrão para definir as configurações básicas necessárias para tornar operacional um servidor de relatório. Ela tem os seguintes requisitos:  
  
-   Examine [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) .  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] devem ser instalados juntos na mesma instância. A instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] hospeda o banco de dados do servidor de relatório que a Instalação cria e configura.  
  
-   A conta de usuário utilizada para executar a instalação deve ser membro do grupo local Administradores e ter permissão para acessar e criar bancos de dados na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda os bancos de dados do servidor de relatório.  
  
-   A instalação deve poder usar os valores padrão para reservar as URLs que dão acesso ao servidor de relatório e ao [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. Esses valores são a porta 80, um curinga forte e os nomes de diretório virtual no formato **ReportServer_\<***instance_name***>** e **Reports_\<***instance_name***>**.  
  
-   A Instalação deve poder usar os valores padrão para criar os bancos de dados de servidor de relatório. Esses valores são **ReportServer** e **ReportServerTempDB**. Se você tiver bancos de dados existentes de uma instalação anterior, a instalação será bloqueada porque não poderá configurar o servidor de relatório na configuração padrão para o modo nativo. Você deve renomear, mover ou excluir os bancos de dados para desbloquear a instalação.  
  
 Se o computador não atender a todos os requisitos de uma instalação padrão, você deverá instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo somente arquivos e usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurá-lo após o término da instalação.
 
 > [!IMPORTANT]
 > Embora o Reporting Services possa ser instalado em um ambiente que tem um RODC (Controlador de Domínio Somente Leitura), o Reporting Services precisa acessar um Controlador de Domínio Leitura-Gravação para funcionar corretamente. Caso o Reporting Services tenha acesso apenas a um RODC, você poderá encontrar erros ao tentar administrar o serviço.
  
##  <a name="bkmk_defaultURLreservations"></a> Reservas de URL padrão  
 As reservas de URL são compostas de um prefixo, nome de host, porta e diretório virtual:  
  
|Parte|Descrição|  
|----------|-----------------|  
|Prefixo|O prefixo padrão é HTTP. Se você instalou anteriormente um certificado de protocolo SSL, a Instalação tentará criar reservas de URL que usem o prefixo HTTPS.|  
|Nome do host|O nome de host padrão é um curinga forte (+). Ele especifica que o servidor de relatório aceitará qualquer solicitação HTTP na porta designada para qualquer nome do host resolvido para o computador, incluindo `http://<computername>/reportserver`, `http://localhost/reportserver` ou `http://<IPAddress>/reportserver`.|  
|Porta|A porta padrão é 80. Observe que, se você usar qualquer porta que não seja a 80, precisará adicioná-la explicitamente à URL quando abrir um aplicativo Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma janela do navegador.|  
|Diretório virtual|Por padrão, os diretórios virtuais são criados no formato ReportServer_\<*instance_name*> para o serviço Web Servidor de Relatórios e Reports_\<*instance_name*> para o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. Para o serviço Web Servidor de Relatórios, o diretório virtual padrão é **reportserver**. Para o [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], o diretório virtual padrão é **reports**.|  
  
 Um exemplo de cadeia de caracteres de URL completa poderia ser como segue:  
  
-   `http://+:80/reportserver`, fornece acesso ao servidor de relatório.  
  
-   `http://+:80/reports`, fornece acesso ao [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)].
  
##  <a name="bkmk_installwithwizard"></a> Instalar o modo nativo com o assistente de instalação do SQL Server  
 A lista a seguir descreve as etapas específicas e as opções do  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você seleciona no Assistente de Instalação do SQL Server. A lista não descreve cada página que você verá no assistente de instalação, somente as páginas relacionadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que fazem parte de uma instalação do modo nativo.  
  
1.  Execute o Assistente de instalação do SQL Server (setup.exe) e avance pelas seguintes páginas preliminares:  
  
    -   Chave do produto  
  
    -   Termos de Licença  
  
    -   Regras globais  
  
    -   Microsoft Update  
  
    -   Atualizações de produto  
  
    -   Instalar arquivos de instalação  
  
    -   Normas de instalação  
  
2.  Na página **Função de instalação** , selecione **Instalação de recurso do SQL Server**.  
  
     ![Instalação de recurso do SQL Server para a função de instalação](../../reporting-services/install-windows/media/rs-setuprole.png "Instalação de recurso do SQL Server para a função de instalação")  
  
3.  Na página **Seleção de Recurso** , selecione o seguinte:  
  
    -   (1) **Serviços do Mecanismo de Banco de Dados**, a menos que uma instância do mecanismo do banco de dados já esteja instalada.  
  
    -   (2) **Reporting Services Nativo**.  
  
     ![Seleção do modo nativo do SSRS na seleção de recursos](../../reporting-services/install-windows/media/rs-setupfeatureselection-native-withcircles.png "Seleção do modo nativo do SSRS na seleção de recursos")  
  
4.  Examine as **Regras de Recurso** aprovadas.  
  
5.  Na página Configuração da instância, lembre-se de que, se você optar por configurar uma **Instância Nomeada**, será necessário usar o nome da instância em URLs quando você navegar para o Gerenciador de Relatórios e para o servidor de relatório em si. Se a instância tiver sido nomeada como "THESQLINSTANCE", as URLs terão aparência semelhante à seguinte:  
  
    -   `http://[ServerName]/ReportServer_THESQLINSTANCE`  
  
    -   `http://[ServerName]/Reports_THESQLINSTANCE`  
  
6.  **Configuração de Servidor**: se você pretende usar o recurso de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , na página **Configuração de Servidor** , configure o tipo de Inicialização **Automático** do SQL Server Agent.   O padrão é manual.  
  
7.  Adicione administradores do SQL Server à página **Configuração do Mecanismo de Banco de Dados** .  
  
8.  Na página **Configuração do Reporting Services** , selecione **Instalar e Configurar**.  
  
     ![Configuração do modo nativo do SSRS](../../reporting-services/install-windows/media/rs-setupconfiguration-native-with-circles.png "Configuração do modo nativo do SSRS")  
  
    > [!NOTE]  
    >  A opção**Instalar e Configurar** não estará disponível a menos que o recurso de banco de dados a ser instalado também esteja selecionado.  
  
9. Regras de configuração de recurso: verifique as regras aprovadas. O assistente de instalação avançará automaticamente para **Pronto para instalar** se todas as regras forem aprovadas.  Específicas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], as regras verificam se um catálogo do servidor de relatório e um banco de dados de catálogo temporário ainda não existem.  
  
10. Na página **Pronto para instalar**, anote o caminho para o arquivo de configuração, pois poderá ser consultado posteriormente para obter um bom resumo da configuração de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicial dos servidores, incluindo os componentes instalados, as contas de serviço e os administradores.  
  
11. Depois que o assistente de instalação do SQL Server estiver concluído, verifique a instalação padrão do modo nativo usando as etapas básicas a seguir.  
  
    -   Abra o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e confirme que você pode conectar-se ao servidor de relatório.  
  
    -   Abra seu navegador **com privilégios administrativos** e conecte-se ao [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], por exemplo `http://localhost/Reports`.  
  
    -   Abra seu navegador com privilégios administrativos e conecte-se à página do servidor de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por exemplo,  `http://localhost/ReportServer`  
  
 Para obter mais informações, consulte a seção Nativa dos dois tópicos a seguir:  
  
 [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Solucionar um problema da instalação do Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
  
##  <a name="bkmk_additional_configuration"></a> Configuração adicional  
  
-   Para configurar a integração do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)], de modo que você possa fixar itens de relatório em um painel do [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)], consulte [Integração do Servidor de Relatórios do Power BI](../../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
-   Para configurar o email para o processamento de assinaturas, consulte [Configurações de email – modo nativo do Reporting Services](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [Entrega de email no Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Para configurar o portal da Web para que você possa acessá-lo em um computador de relatório, a fim de exibir e gerenciar relatórios, consulte [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) e [Configurar um servidor de relatório para administração remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
## <a name="see-also"></a>Consulte Também

[Solucionar um problema da instalação do Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
[Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Configurar a conta de serviço do Servidor de Relatório](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
[Configurar as URLs do Servidor de Relatório](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Configurar uma conexão de banco de dados do Servidor de Relatório](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Instalação somente de arquivos &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
[Inicializar um Servidor de Relatório](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
[Configurar conexões SSL em um servidor de relatórios de modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
