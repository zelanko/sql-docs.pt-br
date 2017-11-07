---
title: Instalar o Analysis Services no modo do Power Pivot | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 035348a23627db2346d319c69030e74e128e744b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-in-power-pivot-mode"></a>Instale o Analysis Services no modo do Power Pivot.
  Os procedimentos neste tópico conduzem você pela instalação de servidor único de um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] de implantação do SharePoint. As etapas incluem a execução do assistente de instalação do SQL Server, bem como as tarefas de configuração que usam a Administração Central do SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
 **Neste tópico:**  
  
 [Plano de fundo](#bkmk_background)  
  
 [Pré-requisitos](#bkmk_prereq)  
  
 [Etapa 1: Instalar o Power Pivot para SharePoint](#InstallSQL)  
  
 [Etapa 2: Configure a integração básica do Analysis Services SharePoint](#bkmk_config)  
  
 [Etapa 3: Verifique a integração](#bkmk_verify)  
  
 [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](#bkmk_firewall)  
  
 [Atualizar pastas de trabalho e atualização de dados agendada](#bkmk_upgrade_workbook)  
  
 [Além da instalação de servidor único – PowerPivot para Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> Plano de fundo  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint é uma coleção de serviços de camada intermediária e back-end que fornece acesso a dados [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do SharePoint 2016 ou SharePoint 2013.  
  
-   **Serviços de back-end:** se você usar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel para criar pastas de trabalho que contêm dados analíticos, será necessário ter o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint para acessar esses dados em um ambiente de servidor. Você pode executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um computador que tenha o SharePoint Server instalado, ou em um computador diferente que não tenha o SharePoint. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não tem nenhuma dependência no SharePoint.  
  
     **Observação:** este tópico descreve a instalação do servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e os serviços do back-end.  
  
-   **Camada intermediária:** aprimoramentos das experiências do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint, incluindo Galeria [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , atualização de dados agendada, painel de gerenciamento e provedores de dados. Para obter mais informações sobre como instalar e configurar a camada intermediária, consulte o seguinte:  
  
    -   [Instalar ou desinstalar o PowerPivot para suplemento do SharePoint (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
    -   [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2016&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2016.md)  
  
    -   [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
  
1.  Você deve ser um administrador local para executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
2.  O SharePoint Server Enterprise Edition é necessário para o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint. Você também pode usar a edição evaluation enterprise.  
  
3.  O computador deve ser adicionado a um domínio na mesma floresta do Active Directory que o Servidor do Office Online (SharePoint 2016) ou Serviços do Excel (SharePoint 2013).  
  
4.  O nome da instância do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] deve estar disponível. Não é possível ter uma instância nomeada existente do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]no computador em que está instalando o Analysis Services no modo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     **Observação:** o nome da instância deve ser POWERPIVOT.  
  
5.  Examine [Requisitos de hardware e software para servidor do Analysis Services no modo do SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
6.  Examine as notas de versão em [SQL Server 2016 Release Notes](../../../sql-server/sql-server-2016-release-notes.md).  
  
###  <a name="bkmk_sqleditions"></a> Requisitos de edição do SQL Server  
 Os recursos de business intelligence não estão disponíveis em todas as edições do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obter detalhes, consulte [Analysis Services recursos compatíveis com as edições do SQL Server 2016](../../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) e [edições e componentes do SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
##  <a name="InstallSQL"></a> Etapa 1: Instalar o Power Pivot para SharePoint  
 Nesta etapa, você executa a Instalação do SQL Server para instalar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Em uma etapa subsequente, configure os Serviços do Excel para usar esse servidor para modelos de dados da pasta de trabalho.  
  
1.  Execute o Assistente de Instalação do SQL Server (Setup.exe).  
  
2.  Selecione **Instalação** no painel de navegação esquerdo.  
  
3.  Selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
4.  Se a página **Chave do Produto (Product Key)** aparecer, especifique a edição de avaliação ou digite a chave do produto (product key) de uma cópia licenciada da edição empresarial. Selecione **Avançar**. Para obter mais informações sobre edições, consulte [Editions and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Examine e aceite os Termos de Licença do Software Microsoft do acordo e selecione **Avançar**.  
  
6.  Se você vir a página **Regras Globais** , examine todas as informações de regras que o assistente de instalação exibir.  
  
7.  Na página **Microsoft Update** , é recomendável usara o Microsoft Update para verificar se há atualizações e selecione **Avançar**.  
  
8.  A página **Instalar Arquivos de Instalação** ficará em execução por vários minutos. Examine os avisos de regra ou regras com falha e selecione **Avançar**.  
  
9. Se outras **Regras de Suporte à Instalação**forem exibidas, examine os avisos e selecione **Avançar**.  
  
     **Observação:** Como o Firewall do Windows está habilitado, será exibido um aviso solicitando a abertura das portas que permitirão o acesso remoto.  
  
10. Na página **Função de instalação** , selecione **Instalação de recurso do SQL Server**.  
  
     Selecione **Avançar**.  
  
11. Na página Seleção de Recurso, selecione **Analysis Services**. Esta opção permite instalar qualquer um dos três modos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Você selecionará o modo em uma etapa posterior. Selecione **Avançar**.  
  
12. Na página **Configuração de Instância** , selecione **Instância Nomeada** e digite **POWERPIVOT** para o nome da instância e, em seguida, clique em **Avançar**.  
  
     ![A instalação do SQL - configuração de instância, página de aterrissagem](../../../analysis-services/instances/install-windows/media/sql2016-pp-instance-config-landing-page.png "a instalação do SQL - configuração de instância, página de aterrissagem")  
  
13. Na página de **Configuração do Servidor** , configure todos os serviços para **Tipo de Inicialização**automática. Especifique a conta de domínio e a senha desejadas para o **SQL Server Analysis Services**, **(1)** no diagrama a seguir.  
  
    -   No [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], você pode usar uma conta de **usuário de domínio** ou a conta **NetworkService** . Não use contas LocalSystem ou LocalService.  
  
    -   Se você adicionou o Mecanismo de Banco de Dados do SQL Server e o SQL Server Agent, é possível configurar os serviços para serem executados como contas de usuário do domínio ou na conta virtual padrão.  
  
    -   Nunca provisione contas de serviço com sua própria conta de usuário de domínio. Isso concede ao servidor as mesmas permissões que você tem aos recursos em sua rede. Se um usuário mal-intencionado invadir o servidor, esse usuário estará conectado com suas credenciais de domínio. O usuário terá as permissões para baixar ou usar os mesmos dados e aplicativos que você.  
  
     Selecione **Avançar**.  
  
     ![A instalação do SQL - página de aterrissagem da configuração do servidor](../../../analysis-services/instances/install-windows/media/sql2016-pp-server-config-landing-page.png "a instalação do SQL - página de aterrissagem da configuração do servidor")  
  
14. Se você estiver instalando o [!INCLUDE[ssDE](../../../includes/ssde-md.md)], a página **Configuração do Mecanismo de Banco de Dados** será exibida. Em Configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , selecione **Adicionar Usuário Atual** para conceder à conta do usuário permissões de administrador na instância do Mecanismo de Banco de Dados.  
  
     Selecione **Avançar**.  
  
15. Na página **Configuração do Analysis Services** , selecione **Modo PowerPivot** em **Modo de Servidor**  
  
     ![A instalação do SQL - página inicial da configuração do Analysis Services](../../../analysis-services/instances/install-windows/media/sql2016-pp-as-config-landing-page.png "a instalação do SQL - página inicial da configuração do Analysis Services")  
  
16. Na página **Configuração do Analysis Services** , clique em **Adicionar Usuário Atual** para conceder permissões administrativas à conta do usuário. Você precisará de permissão administrativa para configurar o servidor depois que Instalação seja concluída.  
  
    -   Na mesma página, adicione a conta de usuário do Windows de qualquer pessoa que também requer permissões administrativas. Por exemplo, qualquer usuário que queira se conectar à instância do [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para solucionar problemas de conexão de banco de dados deve ter permissões de administrador do sistema. Adicione a conta do usuário de qualquer pessoa que precise solucionar problemas ou administrar o servidor agora.  
  
    -   > [!NOTE]  
        >  Todos os aplicativos de serviço que precisam de acesso à instância de servidor do Analysis Services precisam ter as permissões administrativa do Analysis Service. Por exemplo, adicione as contas de serviço para Serviços do Excel, Power View e Performance Point Services. Além de isso, adicione a conta do farm do SharePoint, que é usada como identidade do aplicativo Web que hospeda a Administração Central.  
  
     Selecione **Avançar**.  
  
17. Na página **Relatório de Erros** , selecione **Avançar**.  
  
18. Na página **Pronto para Instalar** , selecione **Instalar**.  
  
19. Se você visualizar a caixa de diálogo **Reinicialização do Computador Necessária**, selecione **OK**.  
  
20. Quando a instalação for concluída, selecione **Fechar**.  
  
21. Reinicie o computador.  
  
22. Se você tiver um firewall em seu ambiente, revise o tópico dos Manuais Online do SQL Server, [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
### <a name="verify-the-sql-server-installation"></a>Verifique a instalação do SQL Server  
 Verifique se o serviço Analysis Services está em execução.  
  
1.  No Microsoft Windows, selecione **Iniciar**, **Todos os Programas**e selecione o grupo **Microsoft SQL Server 2016** .  
  
2.  Selecione **SQL Server Management Studio**.  
  
3.  Conecte-se à instância do Analysis Services; por exemplo, **[nome do seu servidor]\POWERPIVOT**. Se você conseguir se conectar à instância, isso significa que você verificou se o serviço está sendo executado.  
  
##  <a name="bkmk_config"></a> Etapa 2: Configure a integração básica do Analysis Services SharePoint  
 As etapas a seguir descrevem as alterações de configuração necessárias para que você possa interagir com os modelos de dados avançados do Excel em uma biblioteca de documentos do SharePoint. Conclua essas etapas após instalar o SharePoint e SQL Server Analysis Services.  
  
### <a name="sharepoint-2016"></a>SharePoint 2016  
 Os Serviços do Excel foram removidos do SharePoint 2016 e, em vez disso, o Servidor do Office Online é usado para hospedar o Excel.  
  
#### <a name="grant-office-online-server-machine-account-administration-rights-on-analysis-services"></a>Conceda à conta do computador do Servidor do Office Online direitos de administração no Analysis Services  
 Você não precisará concluir esta seção se, durante a instalação do Analysis Services, tiver adicionado a conta do computador do Servidor do Office Online como um administrador do Analysis Services.  
  
1.  No servidor do Analysis Services, inicie o SQL Server Management Studio e conecte-se à instância do Analysis Services; por exemplo `[MyServer]\POWERPIVOT`.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome da instância e selecione **Propriedades**.  
  
     ![Exibir propriedades de um servidor SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "exibir propriedades de um servidor SSAS")  
  
3.  No painel esquerdo, selecione **Segurança**. Adicione a conta do computador no qual Servidor do Office Online está instalado.  
  
     ![Configurações de segurança de um servidor SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "as configurações de segurança de um servidor SSAS")  
  
#### <a name="register-analysis-services-server-with-office-online-server"></a>Registre o servidor do Analysis Services com o Servidor do Office Online  
 Você deve executar essas etapas no Servidor do Office Online.  
  
-   Abra uma janela de comando do PowerShell como administrador.  
  
-   Carregue o módulo `OfficeWebApps` do PowerShell.  
  
     `Import-Module OfficeWebApps`  
  
-   Adicione o servidor do Analysis Services, por exemplo `[MyServer]\POWERPIVOT`.  
  
     `New-OfficeWebAppsExcelBIServer -ServerId [MyServer]\POWERPIVOT]`  
  
### <a name="sharepoint-2013"></a>SharePoint 2013  
  
#### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Conceder direitos de administração do servidor dos Serviços do Excel no Analysis Services  
 Você não precisará concluir esta seção se, durante a instalação do Analysis Services, tiver adicionado a conta de serviço do Aplicativo de Serviços do Excel como um administrador do Analysis Services.  
  
1.  No servidor do Analysis Services, inicie o SQL Server Management Studio e conecte-se à instância do Analysis Services; por exemplo `[MyServer]\POWERPIVOT`.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome da instância e selecione **Propriedades**.  
  
     ![Exibir propriedades de um servidor SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "exibir propriedades de um servidor SSAS")  
  
3.  No painel esquerdo, selecione **Segurança**. Adicione o logon de domínio que você configurou para o Aplicativo de Serviços do Excel na etapa 1.  
  
     ![Configurações de segurança de um servidor SSAS](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "as configurações de segurança de um servidor SSAS")  
  
#### <a name="configure-excel-services-for-analysis-services-integration"></a>Configurar os Serviços do Excel para integração do Analysis Services  
  
1.  Na Administração Central do SharePoint, no grupo Gerenciamento de Aplicativo, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Clique no nome do aplicativo de serviço; o padrão é **Aplicativo de Serviços do Excel**.  
  
3.  Na página **Gerenciar Aplicativo de Serviços do Excel**, clique em **Configurações de Modelo de Dados**.  
  
4.  Clique em **Adicionar Servidor**.  
  
5.  Em **Nome do Servidor**, digite o nome do servidor do Analysis Services e o nome da instância do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Por exemplo, `MyServer\POWERPIVOT`. O nome da instância [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] é obrigatório.  
  
     Digite uma descrição.  
  
6.  Clique em **OK**.  
  
7.  As alterações entrarão em vigor em alguns minutos ou você pode **Parar** e **Iniciar** o serviço **Serviços de Cálculo do Excel**. Para  
  
     Outra alternativa é abrir um prompt de comando com privilégios administrativos e digitar `iisreset /noforce`.  
  
     Você pode verificar se o servidor é reconhecido pelos Serviços do Excel revisando as entradas no log ULS. Você verá entradas semelhantes à seguinte:  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> Etapa 3: Verifique a integração  
 As etapas a seguir conduzem você pela criação e pelo carregamento de uma nova pasta de trabalho para verificar a integração do Analysis Services. Você precisará de um banco de dados do SQL Server para concluir as etapas.  
  
1.  **Observação:** se você já tiver uma pasta de trabalho avançada com segmentações de dados ou filtros, poderá carregá-la para a biblioteca de documentos do SharePoint e verificar se consegue interagir com as segmentações de dados e os filtros na exibição da biblioteca de documentos.  
  
2.  Inicie a nova pasta de trabalho no Excel.  
  
3.  Na guia Dados, selecione **De Outras Fontes** na faixa de opções em **Obter Dados Externos**.  
  
4.  Selecione **Do SQL Server**.  
  
5.  Em **Assistente para Conexão de Dados**, digite o nome da instância do SQL Server que tem o banco de dados que você deseja usar.  
  
6.  Em Credenciais de logon, verifique se a opção **Usar Autenticação do Windows** está selecionada e selecione **Avançar**.  
  
7.  Selecione o banco de dados a ser usado.  
  
8.  Verifique se a caixa de seleção **Conectar à tabela específica** está marcada.  
  
9. Marque a caixa de seleção **Habilitar seleção de várias tabelas e adicionar tabelas ao Modelo de Dados do Excel** .  
  
10. Selecione as tabelas que deseja importar.  
  
11. Marque a caixa de seleção **Importar relações entre as tabelas selecionadas**e selecione **Avançar**. A importação de várias tabelas de um banco de dados relacional permite que você trabalhe com tabelas já relacionadas. Você economiza etapas porque não precisa criar as relações manualmente.  
  
12. Na página **Salvar Arquivo de Conexão de Dados e concluir** do assistente, digite um nome para a conexão e selecione **Concluir**.  
  
13. A caixa de diálogo **Importar Dados** aparecerá. Escolha **Relatório de Tabela Dinâmica**e selecione **OK**.  
  
14. A Lista de Campos da Tabela Dinâmica aparece na pasta de trabalho.   
    Na lista de campos, selecione a guia **Tudo** .  
  
15. Adicione campos às áreas Linha, Colunas e Valor da lista de campos.  
  
16. Adicione um filtro ou uma segmentação de dados à Tabela Dinâmica. **Não ignore esta etapa**. Um filtro ou uma segmentação de dados é o elemento que o ajudará a verificar a instalação do Analysis Services.  
  
17. Salve a pasta de trabalho em uma biblioteca de documentos no farm do SharePoint. Você também pode salvar a pasta de trabalho em um compartilhamento de arquivos e carregá-la na biblioteca de documentos do SharePoint.  
  
18. Selecione o nome da pasta de trabalho para exibi-lo no Excel Online e clique na segmentação de dados ou altere o filtro adicionado anteriormente. Se ocorrer uma atualização de dados, você sabe que o Analysis Services está instalado e disponível para o Excel. Se você abrir a pasta de trabalho no Excel, estará usando uma cópia armazenada em cache, e não o servidor do Analysis Services.  
  
##  <a name="bkmk_firewall"></a> Configurar o Firewall do Windows para permitir o acesso ao Analysis Services  
 Use as informações do tópico [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para determinar se é necessário desbloquear portas em um firewall para permitir o acesso ao Analysis Services ou [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint. Você pode seguir as etapas fornecidas no tópico para definir as configurações de porta e firewall. Na prática, você deve executar essas etapas juntas para permitir o acesso ao servidor do Analysis Services.  
  
##  <a name="bkmk_upgrade_workbook"></a> Atualizar pastas de trabalho e atualização de dados agendada  
 As etapas necessárias para atualizar pastas de trabalho criadas em versões anteriores do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] dependem de qual versão do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] criou a pasta de trabalho. Para obter mais informações, veja [Atualizar pastas de trabalho e a atualização de dados agendada &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_multiple_servers"></a> Além da instalação de servidor único – PowerPivot para Microsoft SharePoint  
 **WFE (Web front-end)** ou **Camada intermediária:**: para usar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint em um farm do SharePoint maior e instalar recursos adicionais do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no farm, execute o pacote de instalador **spPowerPivot16.msi (SharePoint 2016) ou spPowerPivot.msi (SharePoint 2013)** em cada um dos servidores do SharePoint. O spPowerPivot16.msi ou o spPowerPivot.msi instala os provedores de dados necessários e a ferramenta de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2016 ou 2013.  
  
 Para obter mais informações sobre como instalar e configurar a camada intermediária, consulte o seguinte:  
  
-   [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   Para baixar o .msi, veja [Microsoft SQL Server 2016 PowerPivot para Microsoft SharePoint 2016](http://go.microsoft.com/fwlink/?LinkID=324854)  
  
-   [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **Redundância e carga do servidor:** instalar um segundo ou mais servidores do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] fornecerá a redundância da funcionalidade do servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Os servidores adicionais também distribuirão a carga entre os servidores. Para obter mais informações, consulte o seguinte:  
  
-   [Configurar o Analysis Services para processar modelos de dados nos Serviços do Excel (SharePoint 2013)](http://technet.microsoft.com/library/jj614437\(v=office.15\)) (http://technet.microsoft.com/library/jj614437(v=office.15)).  
  
-   [Gerenciar as configurações de modelo de dados dos Serviços do Excel (SharePoint 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\)) (http://technet.microsoft.com/library/jj219780(v=office.15)).  
  
 ![Configurações do SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configurações SharePoint") [enviar comentários e informações de contato pelo Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Consulte também  
 [Migrar o Power Pivot para o SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Atualizar pastas de trabalho e atualização de dados agendada &#40; SharePoint 2013 &#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  

