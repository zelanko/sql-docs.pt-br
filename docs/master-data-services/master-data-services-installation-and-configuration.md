---
title: "Instala&#231;&#227;o e configura&#231;&#227;o do Master Data Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 37
---
# Instala&#231;&#227;o e configura&#231;&#227;o do Master Data Services
  Este artigo aborda a instalação do [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] em um computador com Windows Server 2012 R2, configuração do site e banco de dados do MDS e implantação dos dados e modelos de exemplo. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) permite que sua organização gerencie uma versão confiável dos dados.   
   
Para obter uma visão geral de como organizar dados no [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Visão geral do MDS (Master Data Services)](../master-data-services/master-data-services-overview-mds.md).     
  
 Para obter informações sobre os novos recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Novidades do MDS &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
 
Para obter links para vídeos e outros recursos de treinamento para ajudá-lo a saber mais sobre o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Learn Master Data Services (Saiba mais sobre o Master Data Services)](../master-data-services/learn-sql-server-master-data-services.md). 
  
> **Download**  
>-   Para baixar o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], acesse o  **[Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
>-   Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** para criar uma Máquina Virtual com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  já instalado.  
 
> **Não está conseguindo criar um site do MDS?**
>>Confira este artigo de suporte da Microsoft para obter instruções sobre como resolver esse problema.
[Não é possível criar um site do MDS por meio de uma conta de baixo privilégio no SQL Server 2016](https://aka.ms/mdssupport) 
  
## <a name="installing-master-data-services-and-iis-roles-and-features"></a>Instalando o Master Data Services e as funções e os recursos do IIS  
 Você usa o assistente de instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou um prompt de comando para instalar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
 **Para instalar o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usando a Configuração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador Windows Server 2012 R2**  
  
1.  Clique duas vezes em Setup.exe e siga as etapas no assistente de instalação.  
  
2.  Selecione [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] na página **Seleção de Recursos** em **Recursos Compartilhados**.  
  
     A opção instala o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], assemblies, um snap-in do Windows PowerShell, pastas e arquivos de aplicativos Web e serviços Web.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  Conclua o assistente de instalação.  
  
4.  No [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)], clique no ícone **Gerenciador do Servidor** na barra de tarefas da **Área de Trabalho**.  
  
     ![Icon for the Server Manager in Windows Server 2012 taskbar](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Icon for the Server Manager in Windows Server 2012 taskbar")  
  
5.  Em **Gerenciador do Servidor**, clique em **Adicionar Funções e Recursos** no menu **Gerenciar** .  
  
     ![In Server Manage, the Add Roles and Features menu command](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "In Server Manage, the Add Roles and Features menu command")  
  
6.  Na página **Tipo de Instalação** do **Assistente para Adicionar Funções e Recursos**, aceite o valor padrão (**Instalação baseada em função ou em recurso**) e clique em **Avançar**.  
  
7.  Clique em **Selecionar um servidor no pool de servidores**e clique no servidor em que você instalou o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
     ![Server Selection page on the Add Roles and Features Wizard](../master-data-services/media/mds-servermanagerdashboard-addrolesandfeatureswizard-serverselection.png "Server Selection page on the Add Roles and Features Wizard")  
  
8.  Na caixa **Funções** , clique nas funções e nos serviços de funções necessários para o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] no [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]e clique em **Avançar**. As imagens a seguir mostram as funções e os serviços de funções necessários selecionados.  
  
    > [!WARNING]  
    >  Não instale o serviço de função Publicação do WebDAV. Publicação do WebDAV não é compatível com o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
    > [!IMPORTANT]  
    > A **Compactação de Conteúdo Dinâmico** é habilitada por padrão. Isso reduz consideravelmente o tamanho da resposta xml e salva a E/S de rede, embora o uso da CPU aumente.  Para obter mais informações, veja **Melhoria do desempenho do [CTP] 2.0** in [What's New in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
  
    |Função e serviços de função|Função e serviços de função|  
    |-----------------------------|-----------------------------|  
    |![Common HTTP Features](../master-data-services/media/mds-servermanagerdashboard-commonhttpfeaturesroles.png "Common HTTP Features")|![Health Diagnostics Roles](../master-data-services/media/mds-servermanagerdashboard-healthdiagnosticsroles.png "Health Diagnostics Roles")|  
    |![Performance Roles](../master-data-services/media/mds-servermanagerdashboard-performanceroles.png "Performance Roles")|![Security Roles](../master-data-services/media/mds-servermanagerdashboard-securityroles.png "Security Roles")|  
    |![WebServer Application Development Roles](../master-data-services/media/mds-servermanagerdashboard-webserverapplicationdevelopmentroles.png "WebServer Application Development Roles")|![Management Tools](../master-data-services/media/mds-servermanagerdashboard-managementtoolsroles.png "Management Tools")|  
  
     Para obter uma lista das funções e dos serviços de funções necessários em outros sistemas operacionais, consulte [Requisitos do aplicativo Web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
9. Na caixa **Recursos** , clique nos recursos necessários para o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] no [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]e clique em **Avançar**. As imagens a seguir mostram os recursos necessários selecionados.  
  
    |Recursos|Recursos|  
    |--------------|--------------|  
    |![Net Framework Features](../master-data-services/media/mds-servermanagerdashboard-netframeworkfeatures.png "Net Framework Features")|![Windows Process Features](../master-data-services/media/mds-servermanagerdashboard-windowsprocessfeatures.png "Windows Process Features")|  
  
     Para obter uma lista dos recursos necessários em outros sistemas operacionais, consulte [Requisitos do aplicativo Web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
 Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a configuração, veja [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Configuração&#41;](../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md).  
  
 Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando um prompt de comando, consulte [Instalar o SQL Server 2016 por meio do prompt de comando](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Ao usar um prompt de comando, o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está disponível como um parâmetro de recurso.  
  
 Para obter uma descrição breve com links para mais informações sobre tarefas de pré-instalação, consulte [Instalar o Master Data Services](../master-data-services/install-windows/install-master-data-services.md).  
  
##  <a name="a-namesetupweba-setting-up-the-database-and-website"></a> Configurar o banco de dados e o site  
 **Para configurar o banco de dados e o site usando o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]**  
  
1.  Inicie o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]e clique em **Configuração do Banco de Dados** no painel esquerdo.  
  
2.  Clique em **Criar Banco de Dados**e em **Avançar** no **Assistente para Criar Banco de Dados**.  
  
3.  Na página **Servidor de Banco de Dados** , selecione o **Tipo de autenticação** e clique em **Testar Conexão** para confirmar se você pode se conectar ao banco de dados usando as credenciais para o tipo de autenticação selecionado.  
  
    > [!NOTE]  
    >  Quando você seleciona **Usuário Atual – Segurança Integrada** como o tipo de autenticação, a caixa **Nome de usuário** é somente leitura e exibe o nome da conta de usuário do Windows que está conectado ao computador.  
  
     ![The Database server page in the Create Database Wizard](../master-data-services/media/mds-configurationmanager-createdatabasewizard-serverpage.png "The Database server page in the Create Database Wizard")  
  
4.  Digite um nome no campo **Nome do banco de dados** . Opcionalmente, para selecionar um agrupamento do Windows e especificar uma ou mais das opções disponíveis como **Diferencia maiúsculas de minúsculas**, desmarque a caixa de seleção **Agrupamento padrão do SQL Server** .  
  
     ![The Database page in the Create Database Wizard](../master-data-services/media/mds-configurationmanager-createdatabasewizard-databasepage.png "The Database page in the Create Database Wizard")  
  
     Para obter mais informações sobre o agrupamento do Windows, consulte [Nome de agrupamento do Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).  
  
5.  No campo **Nome de usuário** , especifique a conta do Windows do usuário que será o Superusuário padrão do Master Data Services. Um Superusuário tem acesso a todas as áreas funcionais e pode adicionar, excluir e atualizar todos os modelos.  
  
     ![The Administrator Account page in the Create Database Wizard.](../master-data-services/media/mds-configurationmanager-createdatabasewizard-adminpage.png "The Administrator Account page in the Create Database Wizard.")  
  
6.  Clique em **Avançar** para exibir um resumo das configurações do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] e em **Avançar** novamente para criar o banco de dados.  
  
     Para obter mais informações sobre as configurações do **Assistente para Criar Banco de Dados**, consulte [Assistente para Criar Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
7.  Na página Configuração do Banco de Dados do [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], clique em Selecionar Banco de Dados.  
  
8.  Clique em **Conectar**e selecione o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] criado na Etapa 6.  
  
     ![Connect to Database dialog box for the Database Configuration page](../master-data-services/media/mds-configurationmanager-selectdatabasebutton-connecttodatabasedialog.png "Connect to Database dialog box for the Database Configuration page")  
  
     Você terminou de configurar o banco de dados. A página **Configuração do Banco de Dados** agora exibe a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual você está conectado no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], o banco de dados criado e a versão atual do banco de dados.  
  
     ![Database Configuration page in the Configuration Manager shows a completed database setup.](../master-data-services/media/mds-configurationmanager-databaseconfig-completed.png "Database Configuration page in the Configuration Manager shows a completed database setup.")  
  
9. Em [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], clique em **Configuração da Web** no painel esquerdo.  
  
10. Na caixa de listagem **Site** , clique em **Site Padrão**e em **Criar** para criar um aplicativo Web.  
  
    > [!NOTE]  
    >  Quando você seleciona **Site Padrão**, é necessário criar um aplicativo Web. Se você selecionar **Criar novo site** na caixa de listagem, o aplicativo será criado automaticamente.  
  
     ![Web Configuration page in the Configuration Manager](../master-data-services/media/mds-configurationmanager-webconfig.png "Web Configuration page in the Configuration Manager")  
  
11. Na seção **Pool de Aplicativos** , escolha uma das ações a seguir.  
  
    -   Insira o mesmo nome de usuário inserido na Etapa 5 para o banco de dados **Conta de Administrador**, insira a senha e clique em **OK**.  
  
         **-OU-**  
  
    -   Insira outro nome de usuário, insira a senha e clique em OK.  
  
         Você não precisa usar a mesma conta ao criar o banco de dados e o aplicativo Web.  
  
     ![Create Web Application dialog box, Web Configuration page](../master-data-services/media/mds-configurationmanager-webconfig-createwebapplication.png "Create Web Application dialog box, Web Configuration page")  
  
     Para obter mais informações sobre a caixa de diálogo **Criar Aplicativo Web**, consulte [Caixa de diálogo Criar Aplicativo Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
12. Na página **Configuração da Web** da caixa **Aplicativo Web**, clique no aplicativo criado e em **Selecionar** na seção **Associar Aplicativo ao Banco de Dados**.  
  
13. Clique em **Conectar**, selecione o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que você deseja associar ao aplicativo Web e clique em **OK**.  
  
     Você terminou de configurar o site. A página **Configuração da Web** agora exibe o site selecionado, o aplicativo Web criado e o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] associado ao aplicativo.  
  
     ![The completed Web site configuration](../master-data-services/media/mds-configurationmanager-webconfig-completed.png "The completed Web site configuration")  
  
     Para obter mais informações sobre as configurações da página Configuração da Web, consulte [Página Configuração da Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 Você também pode usar o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar configurações para os aplicativos Web e serviços Web associados ao banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Por exemplo, você pode especificar a frequência com que os dados são carregados ou os emails de validação são enviados. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
##  <a name="a-namedeploysamplea-deploying-sample-models-and-data"></a> Implantar dados e modelos de exemplo  
 Os três pacotes de modelo de exemplo a seguir estão incluídos no  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].   Esses modelos de exemplo incluem dados. **O local padrão dos pacotes de modelo de exemplo é %programfiles%\Microsoft SQL Server\130\Master Data Services\Samples\Packages.**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 Você implanta os pacotes usando a ferramenta MDSModelDeploy. O local padrão da ferramenta MDSModelDeploy é *drive*\Program Files\Microsoft SQL Server\ 130\Master Data Services\Configuration.  
  
 Para obter informações sobre os pré-requisitos para executar essa ferramenta, consulte [Implantar um pacote de implantação de modelo usando MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
 Para obter informações sobre as atualizações feitas nos dados para dar suporte aos novos recursos do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Amostras: Pacotes de implantação de modelo &#40;Master Data Services&#41;](../Topic/Samples:%20Model%20Deployment%20Packages%20\(Master%20Data%20Services\).md).  
  
 **Para implantar modelos de exemplo**  
  
1.  Copie os pacotes de modelo de exemplo em *drive*\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
2.  Abra um Prompt de Comando Administrador: e procure MDSModelDeploy.exe, executando o comando a seguir.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration  
    ```  
  
3.  Implante cada um dos modelos de exemplo no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] executando cada um dos comandos a seguir.  
  
    > [!IMPORTANT]  
    >  Nos exemplos abaixo, o valor do serviço do `MDS1` é especificado. Use esse valor se você selecionou  **Site Padrão** ao configurar o site do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  Consulte a seção [Configurando o banco de dados e o site](#SetUpWeb) .  
    >   
    >  Se você criou um novo site ou selecionou outro site existente, execute o comando a seguir primeiro para determinar o valor do serviço correto.  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  O primeiro valor do serviço na lista de valores retornados é aquele que você especificou para implantar um modelo.  
  
     **Para implantar o modelo de exemplo chartofaccounts_en.pkg**  
  
    ```  
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **Para implantar o modelo de exemplo customer_en.pkg**  
  
    ```  
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **Para implantar o modelo de exemplo product_en.pkg**  
  
    ```  
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
  
    ```  
  
     Quando um modelo é implantado com êxito, a mensagem **operação do MDSModelDeploy concluída** é exibida.  
  
     A imagem a seguir mostra o comando para implantar o modelo de exemplo product_en.pkg.  
  
     ![Command line for deploying the Product sample model](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "Command line for deploying the Product sample model")  
  
4.  Para exibir os modelos de exemplo, faça o seguinte.  
  
    1.  Navegue até o site do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que você configurou. Consulte a seção [Configurando o banco de dados e o site](#SetUpWeb) .  
  
         O endereço do site é http://*server name*/*web application*/.  
  
    2.  Selecione um modelo na caixa de listagem **Modelo** e clique em **Explorer**.  
  
         ![MDS Web site, home page.](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS Web site, home page.")  
  
## <a name="next-step"></a>Próxima etapa  
 Crie um novo modelo e entidades para os dados. Consulte [Criar um modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) e [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 Para obter uma visão geral de como você pode usar um modelo e entidades para criar uma estrutura para seus dados no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Visão geral do MDS &#40;Master Data Services &#41;](../master-data-services/master-data-services-overview-mds.md)  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Get%20Started%20with%20Master%20Data%20Services)  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados dos Master Data Services](../master-data-services/master-data-services-database.md)   
 [Aplicativo Web Master Data Manager](../master-data-services/master-data-manager-web-application.md)   
 [Página Configuração do Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Novidades no MDS &#40;Master Data Services&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  