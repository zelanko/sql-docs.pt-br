---
title: 'Tutorial: Como localizar e iniciar as Ferramentas do SSRS (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 60d8938b8fd74a5a62ac9b122c897dc0008d4f9f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290734"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>Tutorial: Como localizar e iniciar as Ferramentas do SSRS (Reporting Services)
  Este tutorial apresenta as ferramentas usadas para configurar um servidor de relatório, gerenciar o conteúdo e as operações do servidor de relatório e criar e publicar relatórios. O propósito deste tutorial é ajudar os novos usuários a entender como localizar e abrir cada ferramenta. Se você já está familiarizado com as ferramentas, pode passar para outros tutoriais que possam ajudá-lo a aprender importantes habilidades para usar o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Para obter mais informações sobre outros tutoriais, consulte [tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md).  
  
 Neste tópico:  
  
-   [Gerenciador de Configurações do Reporting Services (Modo Nativo)](#bkmk_configuration_manager)  
  
-   [Gerenciador de relatórios (modo nativo)](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [SQL Server Data Tools com o Designer de relatórios e o Assistente de relatório](#bkmk_ssdt)  
  
-   [Construtor de Relatórios](#bkmk_report_builder)  
  
##  <a name="bkmk_configuration_manager"></a> Gerenciador de Configurações do Reporting Services (Modo Nativo).  
 Use o gerenciador de configurações do modo nativo para concluir o seguinte:, , , , , e.  
  
-   Especifique a conta de serviço.  
  
-   Crie ou atualize o banco de dados do servidor de relatório.  
  
-   Modifique as propriedades de conexão.  
  
-   Especifique as URLs.  
  
-   Gerenciar as chaves de criptografia.  
  
-   Configurar o processamento autônomo de relatório e a entrega por email.  
  
 **Instalação:** O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é instalado quando você instala o Modo nativo do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Instalar um servidor de relatório de modo nativo do Reporting Services](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>Para iniciar o Gerenciador de Configuração do Reporting Services  
  
1.  Na tela Iniciar do Windows, digite `reporting` e, nas **Apps** resultados da pesquisa, clique em **Reporting Services Configuration Manager**.  
  
     ![Gerenciador de Configurações do Reporting Services na inicialização](../media/bi-ssrs-configmanager-win8-startscreen.gif "Gerenciador de Configurações do Reporting Services na inicialização")  
  
     **Or**  
  
     Clique em **Iniciar**, **Programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Ferramentas de Configuração**e **Gerenciador de Configurações do Reporting Services**.  
  
     A caixa de diálogo **Seleção da Instância de Instalação do Servidor de Relatório** será exibida, para que você possa selecionar a instância do servidor de relatório que deseja configurar.  
  
2.  Em **Nome do Servidor**, especifique o nome do computador no qual a instância do servidor de relatório está instalada. O nome do computador local é especificado por padrão, mas você também pode digitar o nome de uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Se você especificar um computador remoto, clique em **Localizar** para estabelecer uma conexão. O servidor de relatório deve ser configurado com antecedência para administração remota. Para obter mais informações, consulte [Configurar um Servidor de Relatório para Administração Remota](../report-server/configure-a-report-server-for-remote-administration.md).  
  
3.  Em **Emstance Name**, escolha a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que deseja configurar. Somente instâncias de servidor de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]e do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aparecem na lista. Você não pode configurar versões anteriores do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
4.  Clique em **Conectar**.  
  
5.  Para verificar se você iniciou a ferramenta, compare seus resultados com a seguinte imagem:  
  
     ![Ferramenta de configuração do Reporting Services](../media/rs-ui-reportserverconfigkatmai.gif "Ferramenta de configuração do Reporting Services")  
  
 **Próximas etapas:** [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md) e [Gerenciador de Configurações do Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
##  <a name="bkmk_report_manager"></a> Gerenciador de relatórios (modo nativo)  
 Use [Gerenciador de relatórios &#40;modo nativo do SSRS&#41; ](../report-manager-ssrs-native-mode.md) para definir permissões, gerenciar assinaturas e agendas e trabalhar com relatórios. Também é possível usar o Gerenciador de Relatórios para exibir relatórios.  
  
 **Instalação:** O Gerenciador de relatórios é instalado quando você instala [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] modo nativo: [Instalar o servidor de relatórios de modo nativo do Reporting Services](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 Antes de poder abrir o Gerenciador de Relatórios, é necessário ter permissões suficientes (inicialmente, somente os membros do grupo Administradores local têm permissões que fornecem acesso aos recursos do Gerenciador de Relatórios). O Gerenciador de Relatórios fornece diferentes páginas e opções que dependem das atribuições de função do usuário atual. Os usuários que não têm nenhuma permissão obterão uma página em branco. Os usuários com permissões para exibir relatórios obterão links nos quais podem clicar para abrir os relatórios. Para saber mais sobre permissões, consulte [Funções e permissões &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md).  
  
#### <a name="to-start-report-manager"></a>Para iniciar o Gerenciador de Relatórios  
  
1.  Abra seu navegador. Para obter informações sobre navegadores e versões de navegador compatíveis, consulte [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
2.  Na barra de endereço do navegador da Web, digite a URL do Gerenciador de Relatórios. Por padrão, a URL é **http://\<serverName > / reports**. Você pode usar a ferramenta Configuração do Reporting Services para confirmar o nome de servidor e a URL. Para obter mais informações sobre as URLs usadas no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], veja [Configurar as URLs do Servidor de Relatório &#40;Configuration Manager do SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
3.  O Gerenciador de Relatórios é aberto na janela de navegador. A página de inicialização é a pasta Base. Dependendo das permissões, você poderá ver pastas adicionais, hiperlinks para relatórios e arquivos de recursos na página de inicialização. Você também poderá ver botões e comandos adicionais na barra de ferramentas.  
  
4.  Se você executar o Gerenciador de relatórios no servidor de relatório local, consulte [configurar um servidor de relatório do modo nativo para administração Local &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 **Próximas etapas:** [Configurar o Gerenciador de relatórios &#40;modo nativo&#41;](../report-server/configure-web-portal.md).  
  
##  <a name="bkmk_managements_studio"></a> Management Studio  
 Os administradores de servidor de relatório podem usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para gerenciar um servidor de relatório com outros servidores de componente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md).  
  
#### <a name="to-start-sql-server-management-studio"></a>Para iniciar o SQL Server Management Studio  
  
1.  Do tipo de tela Iniciar do Windows `sql server` e, na **Apps** resultados da pesquisa, clique em **SQL Server Management Studio**.  
  
     ![tela de início do management studio no windows](../media/bi-ssms-win8-startscreen.gif "tela de início do management studio no windows")  
  
     **Or**  
  
     Clique em **Iniciar**e em **Todos os Programas**. Em seguida, clique em [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]e em **SQL Server Management Studio**. A caixa de diálogo **Conectar ao Servidor** é exibida.  
  
2.  Se a caixa de diálogo **Conectar ao Servidor** não aparecer, no **Pesquisador de Objetos**, clique em **Conectar** e selecione **Reporting Services**.  
  
3.  Na lista **Tipo de servidor** , selecione **Reporting Services**. Se o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não estiver na lista, ele não será instalado.  
  
4.  Na lista **Nome do servidor** , selecione uma instância de servidor de relatório. As instâncias locais aparecem na lista. Você também pode digitar o nome de uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
5.  Clique em **Conectar**. Você pode expandir o nó de raiz para definir propriedades de servidor, modificar definições de função ou desativar recursos de servidor de relatório.  
  
##  <a name="bkmk_ssdt"></a> Ferramenta de Dados do SQL Server com Designer de Relatórios e Assistente de Relatórios  
 O Designer de Relatórios está disponível dentro do [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] - Business Intelligence para Visual Studio 2012. A superfície de design da ferramenta inclui janelas tabuladas, assistentes e menus usados para acessar recursos de criação de relatórios. A ferramenta do designer de relatórios torna-se disponível quando você escolhe um modelo de Projeto do Report Server ou um Assistente do Report Server. Para saber mais, consulte [Reporting Services no SQL Server Data Tools &#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md).  
  
#### <a name="to-start-report-designer"></a>Para iniciar o Designer de Relatórios  
  
1.  Na tela inicial do Windows, digite **data** e, nos resultados da pesquisa de **Aplicativos** , clique em **SQL Server Data Tools para Visual Studio 2012**.  
  
     **Or**  
  
     Clique em **inicie**, aponte para **todos os programas**, aponte para [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]e, em seguida, clique em **SQL Server Data Tools (SSDT)**.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Na lista **Tipos de Projeto** , clique em **Projetos de Business Intelligence**.  
  
4.  Na lista **Modelos** , clique em **Projeto do Servidor de Relatório**. O diagrama a seguir mostra como os modelos de projeto aparecem na caixa de diálogo:  
  
     ![Caixa de diálogo do modelo Novo Projeto](../media/rs-ui-newrsproject.gif "Caixa de diálogo do modelo Novo Projeto")  
  
5.  Digite um nome e um local para o projeto ou clique em **Procurar** e selecione um local.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] é aberto com a página inicial do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] . O Gerenciador de Soluções fornece categorias para criar relatórios e fontes de dados. Você pode usar essas categorias para criar novos relatórios e fontes de dados. As janelas tabuladas aparecem ao criar uma definição de relatório. As janelas tabuladas são Dados, Layout e Visualização.  
  
 Para iniciar seu primeiro relatório, consulte [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md). Para obter mais informações sobre designers de consulta, você pode usar no Designer de relatórios, consulte [ferramentas de Design de consulta no relatório Designer SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md).  
  
##  <a name="bkmk_report_builder"></a> Construtor de Relatórios  
 Use [construtor de relatórios &#40;SSRS&#41; ](report-builder-authoring-environment-ssrs.md) para criar relatórios em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] parecido com o Office ambiente de criação. Você pode personalizar e atualizar todos os relatórios existentes, quer tenham sido criados no Designer de Relatórios ou nas versões anteriores do Construtor de Relatórios. Contate o administrador para saber a localização do arquivo ReportBuilder3.msi que você executa para instalar o Construtor de Relatórios no computador local.  
  
 **Instalação:** O clique-depois que a versão do construtor de relatórios é instalada pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] modo nativo ou modo do SharePoint. A versão autônoma do Construtor de Relatórios é um download separado.  Ver [instalar a versão autônoma do construtor de relatórios &#40;construtor de relatórios&#41;](../install-windows/install-report-builder.md)  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>Para iniciar o Construtor de Relatórios ClickOnce a partir do Gerenciador de Relatórios (modo nativo)  
  
1.  No navegador da Web, digite a URL do Gerenciador de Relatórios do servidor de relatório. Por padrão, a URL é http://\<*servername*>/reports. O Gerenciador de Relatórios é aberto.  
  
2.  Clique em **Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>Para iniciar o Construtor de Relatórios ClickOnce usando a URL  
  
1.  No seu navegador da Web, digite a seguinte URL na barra de endereços:  
  
     **http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application**  
  
2.  Pressione ENTER.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>Para iniciar o Construtor de Relatórios ClickOnce no modo do SharePoint do Reporting Services  
  
1.  Navegue até o site que contém a biblioteca onde você deseja criar um novo relatório.  
  
2.  Abra a biblioteca.  
  
3.  No menu **Novo** , clique em **Relatório do Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
#### <a name="to-start-report-builder-stand-alone"></a>Para iniciar a versão autônoma do Construtor de Relatórios  
  
1.  Na tela inicial do Windows, digite **report builder** e clique em **Construtor de Relatórios 3.0**.  
  
     **Or**  
  
     No menu Iniciar, clique em **Todos os Programas**e clique em **Microsoft SQL Server 2014 Report Builder**.  
  
2.  Clique em **Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório.  
  
3.  Clique na **Ajuda do Construtor de Relatórios** para abrir a documentação do Construtor de Relatórios.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar, desinstalar e oferecer suporte ao construtor de relatórios](../install-uninstall-and-report-builder-support.md)   
 [Instalação do modo do SharePoint do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Servidor de Relatório do Reporting Services](../reporting-services-report-server.md)   
 [Ferramentas de Design no Designer do SQL Server Data Tools de relatório de consulta &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
