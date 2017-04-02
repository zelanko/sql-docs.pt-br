---
title: "Configurar o Gerenciador de Relat&#243;rios (modo nativo) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gerenciador de Relatórios [Reporting Services], configurando"
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 28
---
# Configurar o Gerenciador de Relat&#243;rios (modo nativo)
  O Gerenciador de Relatórios é um aplicativo de front-end da Web usado para exibir relatórios, gerenciar o conteúdo do servidor de relatórios e conceder a um usuário o acesso ao servidor de relatórios no modo nativo. O Gerenciador de Relatórios será instalado com o serviço Web Servidor de Relatório na mesma instância do servidor de relatório e, opcionalmente, configurado se você selecionar a opção **Instalar na configuração de modo nativo padrão** na Instalação. Também é possível configurar o Gerenciador de Relatórios como uma tarefa posterior à instalação. Este tópico fornece informações sobre os seguintes cenários de configuração do Gerenciador de Relatórios:  
  
-   [Configurar o Gerenciador de Relatórios para usar a URL padrão](#ConfigureRMURL)  
  
     O Gerenciador de Relatórios é um aplicativo Web que os usuários acessam em um navegador da Web. Você deve definir a URL usada para abrir o aplicativo em uma janela do navegador. A URL consiste em um nome de host, uma porta e um diretório virtual. Os valores padrão dessa URL incluem o nome de host e os valores de porta definidos para a URL do serviço Web Servidor de Relatório, mais o nome do diretório virtual de **relatórios**. Se você tiver uma instância nomeada, o diretório virtual será **reports_instance**, em que **instance** será o nome da instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   **Execução do Gerenciador de Relatórios em um computador remoto**. Dependendo da configuração da rede, você pode precisar habilitar a porta 80 em computadores para permitir solicitações com o Gerenciador de Relatórios.  
  
    > [!TIP]  
    >  Se você tentar acessar o Gerenciador de Relatórios em um computador remoto e receber mensagens de erro de conexão no navegador, uma causa comum são as configurações do firewall. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
     Se necessário, habilite a porta 80 em ambos os computadores para permitir solicitações por essa porta. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
-   [Configurar o Gerenciador de Relatórios para usar a URL de um servidor de relatório específico](#ConfigureSpecificURL)  
  
     Por padrão, o Gerenciador de Relatórios se conecta ao serviço Web Servidor de Relatórios executado no mesmo serviço Servidor de Relatórios. O Gerenciador de Relatórios usa a URL do serviço Web Servidor de Relatórios para estabelecer a conexão. Se você definir várias URLs para o serviço Web Servidor de Relatórios, o Gerenciador de Relatórios usará a última URL definida. No entanto, para algumas implantações, talvez você queira que o Gerenciador de Relatórios sempre se conecte ao serviço Web por meio de uma URL estática. Um exemplo de um motivo pelo qual talvez você queira fazer isso seria se tivesse configurado a filtragem de pacotes em uma determinada porta ou endereço IP, e quisesse que todas as conexões com o servidor de relatórios passassem pelas regras de filtragem definidas.  
  
-   [Apontar o Gerenciador de Relatórios para um servidor de relatórios remoto](#ConfigureRemoteRS)  
  
     Por padrão, o Gerenciador de Relatórios fornece acesso de front-end ao serviço Web Servidor de Relatório executado na mesma instância do servidor, mas você poderá configurar o Gerenciador de Relatórios para se conectar a um serviço Web Servidor de Relatórios remoto se desejar executar o serviço Web e o Gerenciador de Relatórios em processos separados ou se estiver configurando o acesso ao servidor de modo diferente para cada servidor (por exemplo, caso esteja implantando o Gerenciador de Relatórios para os usuários em uma extranet ou conexão com a Internet e queira colocar um firewall entre o servidor de relatórios e o Gerenciador de Relatórios).  
  
-   [Personalizar estilos e o título do aplicativo](#ModifyTitle)  
  
     É possível personalizar o Gerenciador de Relatórios, o visualizador de relatório HTML e a barra de ferramentas de relatório de maneiras limitadas alterando os estilos e editando o título do aplicativo mostrado no Gerenciador de Relatórios.  
  
-   [Desativar o Gerenciador de Relatórios](#DisableRM)  
  
     Quando você instala uma instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que usa modo nativo, por padrão, o Gerenciador de Relatórios é habilitado. Entretanto, você pode desabilitar o Gerenciador de Relatórios se tiver um aplicativo de front-end que forneça funções equivalentes ou se quiser usar apenas as interfaces Acesso da URL ou SOAP para acessar o servidor de relatórios ou se estiver usando o Gerenciador de Relatórios a partir de uma instância diferente do servidor de relatórios.  
  
## Pré-requisitos  
 Para usar o Gerenciador de Relatórios, é preciso atender aos seguintes pré-requisitos:  
  
-   Você deve ter um servidor de relatórios minimamente configurado. Para obter mais informações sobre como definir um servidor de relatório com as configurações mínimas, veja [Configurar um servidor de relatório &#40;Modo Nativo do Reporting Services&#41;](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md).  
  
-   É necessário que o servidor de relatório seja executado no modo nativo. Não é possível usar o Gerenciador de Relatórios com um servidor de relatórios configurado para o modo integrado do SharePoint. No SQL Server 2012, você não pode alternar um servidor de relatório de um modo para outro. Para alterar o tipo de servidor de relatório que seu ambiente usa, instale o modo desejado do servidor de relatório e copie ou mova os itens de relatório para o novo servidor de relatório. Esse processo geralmente é denominado 'migração'. As etapas necessárias para migrar dependem do modo que você está migrando e a versão da qual você está migrando. Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   Você também deve ter o Internet Explorer 7.0 ou posterior com script habilitado. Para obter mais informações, veja [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
##  <a name="ConfigureRMURL"></a> Configurar o Gerenciador de Relatórios para usar a URL padrão  
 Por padrão, a URL do Gerenciador de Relatórios consiste em um nome de diretório virtual exclusivo, mais a porta e o nome de host definidos para o serviço Web Servidor de Relatórios executado na mesma instância. Na maioria dos casos, o nome de host é o nome de rede do computador servidor de relatórios, mas também pode ser um endereço IP ou cabeçalho de host que resolva o computador. Para configurar o Gerenciador de Relatórios para usar a URL padrão, use a página **URL do Gerenciador de Relatórios** na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
#### Para configurar a URL do Gerenciador de Relatórios padrão e o diretório virtual  
  
1.  Abra a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e se conecte à instância do servidor de relatório.  
  
2.  Na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], clique em **URL do Gerenciador de Relatórios** para abrir a página para configurar a URL.  
  
3.  Digite um nome de diretório virtual exclusivo para o Gerenciador de Relatórios.  
  
4.  Clique em **Aplicar**.  
  
5.  Se você estiver usando o [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] ou o Windows Server 2008, talvez sejam necessárias algumas etapas adicionais antes de usar o Gerenciador de Relatórios. Para obter mais informações, veja [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="ConfigureSpecificURL"></a> Configurar o Gerenciador de Relatórios para usar a URL de um servidor de relatório específico  
 Quando você configura as URLs na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o Gerenciador de Relatórios detecta e usa automaticamente todas as URLs novas e atualizadas do servidor de relatórios executado na mesma instância do servidor. Se a sua implantação exigir o uso de uma única URL estática para todas as solicitações do servidor de relatórios, você poderá especificar essa URL no arquivo RSReportServer.config.  
  
#### Para configurar uma URL estática do servidor de relatório  
  
1.  Abra o arquivo **RSReportServer.config** em um editor de texto. Por padrão, ele está localizado em \Arquivos de Programas\Microsoft SQL Server\MSRS12.\<*nome da instância*>\Reporting Services\ReportServer.  
  
2.  Localize **ReportServerURL**.  
  
3.  Substitua-o pela URL da instância do servidor de relatórios.  
  
4.  Salve suas alterações e feche o arquivo.  
  
 Para obter mais informações sobre o arquivo de configuração, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) no [Arquivo de configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
##  <a name="ConfigureRemoteRS"></a> Configurar o Gerenciador de Relatórios para usar um servidor de relatórios remoto  
 Para configurações de implantação que usam o Gerenciador de Relatórios e o servidor de relatórios em computadores diferentes, é preciso ter duas instalações separadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. O Gerenciador de Relatórios é inserido no serviço Servidor de Relatórios e não é instalado por si só. Para executar o Gerenciador de Relatórios em outro computador em seu próprio processo, instale um segundo servidor de relatórios. Ambas as instâncias de servidor devem ser servidores de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### Para conectar o Gerenciador de Relatórios a uma instância do servidor de relatórios remoto  
  
1.  Instale duas instâncias de servidor de relatório.  
  
2.  Configure a primeira instalação que hospedará o servidor de relatórios:  
  
    1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    2.  Clique em **URL do Serviço Web** para configurar um nome de host, porta e diretório virtual para o servidor de relatório.  
  
    3.  Clique em **Banco de Dados** para configurar o banco de dados do servidor de relatório.  
  
3.  Configure a segunda instalação que hospedará o Gerenciador de Relatórios:  
  
    1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    2.  Clique em **URL do Gerenciador de Relatórios** para entrar em um nome do diretório virtual para o Gerenciador de Relatórios.  
  
     Não configure o banco de dados. Não teste as URLs.  
  
4.  No computador com o Gerenciador de Relatórios, modifique as definições de configuração em RSReportServer.config para apontar para a instância do servidor de relatório remoto. Durante a inicialização, o Gerenciador de Relatórios lerá o arquivo de configuração para obter a URL para o servidor de relatórios:  
  
    1.  Abra o RSReportServer.config em um editor de texto. Por padrão, ele está localizado em \Arquivos de Programas\Microsoft SQL Server\MSRS11.\<*nome da instância*>\Reporting Services\ReportServer.  
  
    2.  Localize **ReportServerURL**.  
  
    3.  Substitua pela URL da instância do servidor de relatórios remoto.  
  
    4.  Salve suas alterações e feche o arquivo.  
  
5.  > [!TIP]  
    >  Se necessário, habilite a porta 80 em ambos os computadores para permitir solicitações por essa porta. Para obter instruções, veja [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Reinicie o servidor de relatório.  
  
7.  Abra o Gerenciador de Relatórios em uma janela do navegador. Caso já esteja aberto, atualize o navegador para verificar se o Gerenciador de Relatórios está conectado ao servidor remoto. Você deverá ver o conteúdo do servidor de destino.  
  
8.  Desative os recursos de servidor que você não estiver usando:  
  
    -   No computador do Gerenciador de Relatórios, desative **WebServiceAndHTTPAccessEnabled** e **ScheduleEventsAndReportDeliveryEnabled**.  
  
    -   No computador Servidor de Relatório, desative **ReportManagerEnabled**.  
  
 Para obter mais informações sobre como desativar recursos, consulte a seção [Ativar e desativar recursos do Reporting Services](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md).  
  
##  <a name="ModifyTitle"></a> Personalizar estilos ou o título do aplicativo  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] não dá suporte à personalização das folhas de estilo do Gerenciador de Relatórios. No entanto, se você tiver experiência no desenvolvimento Web, poderá modificar os estilos por sua conta e risco. Para obter mais informações sobre quais arquivos contêm informações de estilo, consulte [Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de Relatórios](../Topic/Customize%20Style%20Sheets%20for%20HTML%20Viewer%20and%20Report%20Manager.md).  
  
 O Gerenciador de Relatórios tem um título de aplicativo que aparece na parte superior da página. Por padrão, o título é **SQL Server Reporting Services**. Este título pode ser personalizado. Para alterar o título, use a página Configurações de Site no Gerenciador de Relatórios. Para modificar as configurações do aplicativo no Gerenciador de Relatórios, você deve receber a função **Administrador de Sistema** para definir propriedades na página Configurações de Site. Para exibir o título do aplicativo, os usuários devem receber a função **Usuário do Sistema**.  
  
#### Para modificar o título do aplicativo  
  
1.  Faça logon usando uma conta que com permissões de **Administrador de Sistema** no servidor de relatório.  
  
2.  Abra o Internet Explorer.  
  
3.  Insira a URL do Gerenciador de Relatórios. Por padrão, considera-se http://\<**nome-do-servidor**>/relatórios, mas se você tiver instalado o Reporting Services como uma instância nomeada, a URL padrão será http://\<**nome-do-servidor**>/relatórios\<**_nome-da-instância**>.  
  
4.  Clique em **Configurações de Site**.  
  
5.  Na guia **Geral**, em **Nome**, substitua **SQL Server Reporting Services** por outro nome.  
  
6.  Clique em **Aplicar**.  
  
##  <a name="DisableRM"></a> Desativar o Gerenciador de Relatórios  
 Você poderá desativar o Gerenciador de Relatórios se tiver um aplicativo personalizado que forneça funções equivalentes ou se estiver usando o aplicativo Gerenciador de Relatórios de uma instância de serviço diferente. Para desativar o Gerenciador de Relatórios, modifique o arquivo RSReportServer.config.  
  
#### Para desativar o Gerenciador de Relatórios  
  
1.  Abra o arquivo RSReportServer.config em um editor de texto. Por padrão, ele está localizado em \Arquivos de Programas\Microsoft SQL Server\MSRS11.\<*nome da instância*>\Reporting Services\ReportServer.  
  
2.  Localize **IsReportManagerEnabled**.  
  
3.  Defina o valor como **False**.  
  
4.  Salve suas alterações e feche o arquivo.  
  
 Para obter mais informações sobre como modificar esse arquivo de configuração, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Para obter mais informações sobre como desabilitar recursos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Ativar e desativar recursos do Reporting Services](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md).  
  
## Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)   
 [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)   
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de Relatórios](../Topic/Customize%20Style%20Sheets%20for%20HTML%20Viewer%20and%20Report%20Manager.md)   
 [Ativar e desativar recursos do Reporting Services](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
 [Gerenciar um servidor de relatórios de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  