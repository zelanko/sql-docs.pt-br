---
title: PowerPivot para instalação do SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95642654da9492087b3720e1b85c369131b55ed2
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487387"
---
# <a name="powerpivot-for-sharepoint-2013-installation"></a>Instalação do PowerPivot para SharePoint 2013
  Os procedimentos neste tópico conduzem você pela instalação de servidor único de um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo de implantação do SharePoint. As etapas incluem a execução do assistente de instalação do SQL Server, bem como as tarefas de configuração que usam a Administração Central do SharePoint 2013.  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 | SharePoint 201  
  
 **Neste tópico:**  
  
 [Informações](#bkmk_background)  
  
 [Pré-requisitos](#bkmk_prereq)  
  
 [Etapa 1: Instale o PowerPivot para SharePoint](#InstallSQL)  
  
 [Etapa 2: Configure a integração básica do Analysis Services SharePoint](#bkmk_config)  
  
 [Passo 3: Verifique a Integração](#bkmk_verify)  
  
 [Configure the Windows Firewall to Allow Analysis Services Access](#bkmk_firewall)  
  
 [Atualizar pastas de trabalho e atualização de dados agendada](#bkmk_upgrade_workbook)  
  
 [Além da instalação de um servidor único - PowerPivot para Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="background"></a><a name="bkmk_background"></a> Segundo Plano  
 O PowerPivot para SharePoint é uma coleção de serviços de camada intermediária e backend que fornece acesso a dados PowerPivot em um farm do SharePoint 2013.  
  
-   **Serviços de back-end:** se você usar o PowerPivot para Excel para criar pastas de trabalho que contêm dados analíticos, será necessário ter o PowerPivot para SharePoint para acessar esses dados em um ambiente de servidor. Você pode executar a Instalação do SQL Server em um computador que tenha o SharePoint Server 2013 instalado, ou em um computador diferente que não tenha o SharePoint. O Analysis Services não tem nenhuma dependência no SharePoint.  
  
     **Observação:** este tópico descreve a instalação do servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e os serviços do back-end.  
  
-   **Camada intermediária:** aprimoramentos às experiências do PowerPivot no SharePoint incluindo Galeria PowerPivot, atualização de dados agendada, painel de gerenciamento e provedores de dados. Para obter mais informações sobre como instalar e configurar a camada intermediária, consulte o seguinte:  
  
    -   [Instale ou desinstale o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
    -   [Configure soluções powerpivot e implante &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> Pré-requisitos  
  
1.  Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
2.  O SharePoint Server 2013 Enterprise Edition é necessário para o PowerPivot para SharePoint. Você também pode usar a edição evaluation enterprise.  
  
3.  O computador deve ser adicionado a um domínio na mesma floresta do Active Directory que os Serviços do Excel.  
  
4.  O nome da instância do PowerPivot deve estar disponível. Você não pode ter uma instância nomeada existente do PowerPivot no computador em que está instalando o Analysis Services no modo do SharePoint.  
  
5.  Revisar [os requisitos de hardware e software para o servidor de serviços de análise no modo SharePoint &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md).  
  
6.  Revise as notas de versão no [SQL Server 2012 Service Pack 1 Release Notes](https://go.microsoft.com/fwlink/?LinkID=248389) (https://go.microsoft.com/fwlink/?LinkID=248389).  
  
###  <a name="sql-server-edition-requirements"></a><a name="bkmk_sqleditions"></a> Requisitos de edição do SQL Server  
 Os recursos de business intelligence não estão disponíveis em todas as edições do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obter detalhes, consulte [Recursos suportados pelas edições dohttps://go.microsoft.com/fwlink/?linkid=232473) SQL Server 2012 (](https://go.microsoft.com/fwlink/?linkid=232473) e [Edições e Componentes do SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
 As notas de versão atuais podem ser encontradas no [SQL Server 2012 SP1 Release Notes](https://go.microsoft.com/fwlink/?LinkID=248389) (https://go.microsoft.com/fwlink/?LinkID=248389).  
  
 [Notas de versão do Microsoft SQL Server 2012 (https://go.microsoft.com/fwlink/?LinkId=236893)](https://go.microsoft.com/fwlink/?LinkId=236893).  
  
##  <a name="step-1-install-powerpivot-for-sharepoint"></a><a name="InstallSQL"></a>Passo 1: Instalar powerpivot para SharePoint  
 Nesta etapa, você executa a Instalação do SQL Server para instalar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Em uma etapa subsequente, configure os Serviços do Excel para usar esse servidor para modelos de dados da pasta de trabalho.  
  
1.  Execute o Assistente de Instalação do SQL Server (Setup.exe).  
  
2.  Clique em **Instalação** no painel de navegação esquerdo.  
  
3.  Clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
4.  Se a página **Chave do Produto (Product Key)** aparecer, especifique a edição de avaliação ou digite a chave do produto (product key) de uma cópia licenciada da edição empresarial. Clique em **Próximo**. Para obter mais informações sobre edições, consulte [Editions and Components of SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Examine e aceite os Termos de Licença do Software Microsoft do acordo e clique em **Avançar**.  
  
6.  Se você vir a página **Regras Globais** , examine todas as informações de regras que o assistente de instalação exibir.  
  
7.  Na página **Microsoft Update** , é recomendável usara o Microsoft Update para verificar se há atualizações e, em seguida, clique em **Avançar**.  
  
8.  A página **Instalar Arquivos de Instalação** ficará em execução por vários minutos. Examine os avisos de regra ou regras com falha e clique em **Avançar**.  
  
9. Se outras **Regras de Suporte à Instalação**forem exibidas, revise os avisos e clique em **Avançar**.  
  
     **Observação:** Como o Firewall do Windows está habilitado, será exibido um aviso solicitando a abertura das portas que permitirão o acesso remoto.  
  
10. Na página **Função de Instalação** , selecione **SQL Server PowerPivot para SharePoint**. Essa opção instala o Analysis Services no modo do SharePoint.  
  
     Opcionalmente, você pode acrescentar uma instância do Mecanismo de banco de dados a sua instalação. Você pode adicionar o Mecanismo de Banco de Dados ao configurar uma nova fazenda e precisa de um servidor de banco de dados para executar a configuração e os bancos de dados de conteúdo da fazenda. Essa opção também instala o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
     Se você adicionou o Mecanismo de Banco de Dados, ele foi instalado como uma instância nomeada do **PowerPivot** . Sempre que você especificar uma conexão com esta instância, insira o nome do banco de dados neste formato: [`servername`]\PowerPivot.  
  
     Clique em **Próximo**.  
  
     ![Função de instalação](../../../sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "Função de instalação")  
  
11. Em Seleção de Recursos, uma lista somente leitura dos recursos será exibida para fins informativos. Não é possível adicionar ou remover os itens pré-selecionados para essa função. Clique em **Próximo**.  
  
12. Na página **Configuração da Instância** , um nome de instância somente leitura do 'PowerPivot' é exibido para fins informativos. Esse nome de instância é obrigatório e não pode ser modificado. No entanto, é possível inserir um ID da Instância exclusivo para especificar um nome de diretório descritivo e chaves do Registro. Clique em **Próximo**.  
  
13. Na página de **Configuração do Servidor** , configure todos os serviços para **Tipo de Inicialização**automática. Especifique a conta de domínio e a senha desejadas para o **SQL Server Analysis Services**, **(1)** no diagrama a seguir.  
  
    -   No [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], você pode usar uma conta de **usuário de domínio** ou a conta **NetworkService** . Não use contas LocalSystem ou LocalService.  
  
    -   Se você adicionou o Mecanismo de Banco de Dados do SQL Server e o SQL Server Agent, é possível configurar os serviços para serem executados como contas de usuário do domínio ou na conta virtual padrão.  
  
    -   Nunca provisione contas de serviço com sua própria conta de usuário de domínio. Isso concede ao servidor as mesmas permissões que você tem aos recursos em sua rede. Se um usuário mal-intencionado invadir o servidor, esse usuário estará conectado com suas credenciais de domínio. O usuário terá as permissões para baixar ou usar os mesmos dados e aplicativos que você.  
  
     Clique em **Próximo**.  
  
     ![Configuração do SSAS Server](../../../sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "Configuração do SSAS Server")  
  
14. Se você estiver instalando o [!INCLUDE[ssDE](../../../includes/ssde-md.md)], a página **Configuração do Mecanismo de Banco de Dados** será exibida. Em Configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , clique em **Adicionar Usuário Atual** para conceder à conta do usuário permissões de administrador na instância do Mecanismo de Banco de Dados.  
  
     Clique em **Próximo**.  
  
15. Na página **Configuração do Analysis Services** , clique em **Adicionar Usuário Atual** para conceder à conta do usuário permissões administrativas. Você precisará de permissão administrativa para configurar o servidor depois que Instalação seja concluída.  
  
    -   Na mesma página, adicione a conta de usuário do Windows de qualquer pessoa que também requer permissões administrativas. Por exemplo, qualquer usuário que queira se conectar à instância do [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para solucionar problemas de conexão de banco de dados deve ter permissões de administrador do sistema. Adicione a conta do usuário de qualquer pessoa que precise solucionar problemas ou administrar o servidor agora.  
  
    -   > [!NOTE]  
        >  Todos os aplicativos de serviço que precisam de acesso à instância de servidor do Analysis Services precisam ter as permissões administrativa do Analysis Service. Por exemplo, adicione as contas de serviço para Serviços do Excel, Power View e Performance Point Services. Além de isso, adicione a conta do farm do SharePoint, que é usada como identidade do aplicativo Web que hospeda a Administração Central.  
  
     Clique em **Próximo**.  
  
16. Na página **Relatório de Erros**, clique em **Avançar**.  
  
17. Na página **Pronto para instalar**, clique em **Instalar**.  
  
18. Se você visualizar a caixa de diálogo **Reinicialização do Computador Necessária**, clique em **OK**.  
  
19. Quando a instalação for concluída, clique em **Fechar**.  
  
20. Reinicie o computador.  
  
21. Se você tiver um firewall em seu ambiente, revise o tópico dos Manuais Online do SQL Server, [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
### <a name="verify-the-sql-server-installation"></a>Verifique a instalação do SQL Server  
 Verifique se o serviço Analysis Services está em execução.  
  
1.  No Microsoft Windows, clique em **Iniciar**, clique em **Todos os Programas**e clique no grupo **Microsoft SQL Server 2012** .  
  
2.  Clique em **SQL Server Management Studio**.  
  
3.  Conecte-se à instância do Analysis Services; por exemplo, **[nome do seu servidor]\POWERPIVOT**. Se você conseguir se conectar à instância, isso significa que você verificou se o serviço está sendo executado.  
  
##  <a name="step-2-configure-basic-analysis-services-sharepoint-integration"></a><a name="bkmk_config"></a>Passo 2: Configurar a integração do SharePoint dos Serviços básicos de análise  
 As etapas a seguir descrevem as alterações de configuração necessárias para que você possa interagir com os modelos de dados avançados do Excel em uma biblioteca de documentos do SharePoint. Conclua essas etapas após instalar o SharePoint Server 2013 e SQL Server Analysis Services.  
  
### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Conceder direitos de administração do servidor dos Serviços do Excel no Analysis Services  
 Você não precisará concluir esta seção se, durante a instalação do Analysis Services, tiver adicionado a conta de serviço do Aplicativo de Serviços do Excel como um administrador do Analysis Services.  
  
1.  No servidor do Analysis Services, inicie o SQL Server Management Studio e conecte-se à instância do Analysis Services; por exemplo `[MyServer]\POWERPIVOT`.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome da instância e clique em **Propriedades**.  
  
     ![Exibir propriedades de um servidor SSAS](../../../sql-server/install/media/as-ssms-proeprties.gif "Exibir propriedades de um servidor SSAS")  
  
3.  No painel esquerdo, clique em **Segurança**. Adicione o logon de domínio que você configurou para o Aplicativo de Serviços do Excel na etapa 1.  
  
     ![Configurações de segurança de um SSAS Server](../../../sql-server/install/media/as-ssms-security.gif "Configurações de segurança de um SSAS Server")  
  
### <a name="configure-excel-services-for-analysis-services-integration"></a>Configurar os Serviços do Excel para integração do Analysis Services  
  
1.  Na Administração Central do SharePoint, no grupo Gerenciamento de Aplicativos, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do aplicativo de serviço; o padrão é **Aplicativo de Serviços do Excel**.  
  
3.  Na página **Gerenciar Aplicativo de Serviços do Excel**, clique em **Configurações de Modelo de Dados**.  
  
4.  Clique em **Adicionar Servidor**.  
  
5.  Em **Nome do Servidor**, digite o nome do servidor do Analysis Services e o nome da instância do PowerPivot. Por exemplo, `MyServer\POWERPIVOT`. O nome da instância do PowerPivot é necessária.  
  
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
  
##  <a name="step-3-verify-the-integration"></a><a name="bkmk_verify"></a>Passo 3: Verifique a Integração  
 As etapas a seguir conduzem você pela criação e pelo carregamento de uma nova pasta de trabalho para verificar a integração do Analysis Services. Você precisará de um banco de dados do SQL Server para concluir as etapas.  
  
1.  **Observação:** se você já tiver uma pasta de trabalho avançada com segmentações de dados ou filtros, poderá carregá-la para a biblioteca de documentos do SharePoint e verificar se consegue interagir com as segmentações de dados e os filtros na exibição da biblioteca de documentos.  
  
2.  Inicie a nova pasta de trabalho no Excel.  
  
3.  Na guia Dados, clique em **De Outras Fontes** na faixa de opções em **Obter Dados Externos**.  
  
4.  Selecione **Do SQL Server**.  
  
5.  Em **Assistente para Conexão de Dados**, digite o nome da instância do SQL Server que tem o banco de dados que você deseja usar.  
  
6.  Ou, em Credenciais de logon, verifique se a opção **Usar Autenticação do Windows** está selecionada e clique em **Avançar**.  
  
7.  Selecione o banco de dados a ser usado.  
  
8.  Verifique se a caixa de seleção **Conectar à tabela específica** está marcada.  
  
9. Clique na caixa de seleção **Habilitar seleção de várias tabelas e adicionar tabelas ao Modelo de Dados do Excel** .  
  
10. Selecione as tabelas que deseja importar.  
  
11. Clique na caixa de seleção **Importar relações entre as tabelas selecionadas**e clique em **Avançar**. A importação de várias tabelas de um banco de dados relacional permite que você trabalhe com tabelas já relacionadas. Você economiza etapas porque não precisa criar as relações manualmente.  
  
12. Na página **Salvar Arquivo de Conexão de Dados e concluir** do assistente, digite um nome para a conexão e clique em **Concluir**.  
  
13. A caixa de diálogo **Importar Dados** aparecerá. Escolha **Relatório de Tabela Dinâmica**e clique em **OK**.  
  
14. A Lista de Campos da Tabela Dinâmica aparece na pasta de trabalho.   
    Na lista de campos, clique na guia **Tudo** .  
  
15. Adicione campos às áreas Linha, Colunas e Valor da lista de campos.  
  
16. Adicione um filtro ou uma segmentação de dados à Tabela Dinâmica. **Não ignore esta etapa**. Um filtro ou uma segmentação de dados é o elemento que o ajudará a verificar a instalação do Analysis Services.  
  
17. Salve a pasta de trabalho em uma biblioteca de documentos em um SharePoint Server 2013 que tenha os Serviços do Excel configurados. Você também pode salvar a pasta de trabalho em um compartilhamento de arquivos e carregá-la na biblioteca de documentos do SharePoint Server 2013.  
  
18. Clique no nome da pasta de trabalho para exibi-lo no SharePoint e clique na segmentação de dados ou altere o filtro adicionado anteriormente. Se ocorrer uma atualização de dados, você sabe que o Analysis Services está instalado e disponível para os Serviços do Excel. Se você abrir a pasta de trabalho no Excel, estará usando uma cópia armazenada em cache, e não o servidor do Analysis Services.  
  
##  <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a><a name="bkmk_firewall"></a>Configure o Firewall do Windows para permitir o acesso aos serviços de análise  
 Use as informações doe tópico [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md) para determinar se é necessário desbloquear portas em um firewall para permitir o acesso ao Analysis Services ou ao PowerPivot para SharePoint. Você pode seguir as etapas fornecidas no tópico para definir as configurações de porta e firewall. Na prática, você deve executar essas etapas juntas para permitir o acesso ao servidor do Analysis Services.  
  
##  <a name="upgrade-workbooks-and-scheduled-data-refresh"></a><a name="bkmk_upgrade_workbook"></a>Atualizar livros de trabalho e atualização de dados agendados  
 As etapas necessárias para atualizar pastas de trabalho criadas em versões anteriores do PowerPivot dependem de qual versão do PowerPivot criou a pasta de trabalho. Para obter mais informações, veja [Atualizar pastas de trabalho e a atualização de dados agendada &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013).  
  
##  <a name="beyond-the-single-server-installation--powerpivot-for-microsoft-sharepoint"></a><a name="bkmk_multiple_servers"></a>Além da instalação de um servidor único - PowerPivot para Microsoft SharePoint  
 **WFE (Web front-end)** ou **Camada intermediária:**: para usar um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint em um farm do SharePoint maior e instalar recursos adicionais do PowerPivot no farm, execute o pacote de instalador **spPowerPivot.msi** em cada um dos servidores do SharePoint. O spPowerPivot.msi instala os provedores de dados necessários e a ferramenta de configuração do PowerPivot para SharePoint 2013.  
  
 Para obter mais informações sobre como instalar e configurar a camada intermediária, consulte o seguinte:  
  
-   [Instale ou desinstale o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
-   Para baixar o .msi, consulte [Microsoft SQL Server 2014 PowerPivot para Microsoft SharePoint 2013](https://go.microsoft.com/fwlink/?LinkID=324854)  
  
-   [Configure soluções powerpivot e implante &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013)  
  
 **Redundância e carga do servidor:** instalar um segundo ou mais servidores do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint fornecerá a redundância da funcionalidade do servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Os servidores adicionais também distribuirão a carga entre os servidores. Para saber mais, consulte o seguinte:  
  
-   [Configure serviços de análise para o processamento de modelos de dados em Serviços excel](https://technet.microsoft.com/library/jj614437\(v=office.15\)) (https://technet.microsoft.com/library/jj614437(v=office.15)).  
  
-   [Gerenciar as configurações do modelo de dados do Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\)) (https://technet.microsoft.com/library/jj219780(v=office.15)).  
  
 ![Configurações do SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configurações do SharePoint") [Envie feedback e informações de contato através do Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Consulte Também  
 [Migrar powerpivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)   
 [Instale ou desinstale o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)   
 [Atualizar livros de trabalho e atualizar dados agendados &#40;sharepoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013)  
  
  
