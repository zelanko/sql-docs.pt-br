---
title: "Instalar o primeiro servidor de relatório no modo do SharePoint | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 664bf6ff099454060779ff19dd4e07b48acf6d2c
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="install-the-first-report-server-in-sharepoint-mode"></a>Instalar o Primeiro Servidor de Relatório no Modo do SharePoint

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Os procedimentos deste tópico conduzirão você pela instalação de servidor único do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. As etapas incluem a execução do assistente de instalação do SQL Server, bem como as tarefas de configuração que usam a Administração Central do SharePoint. O tópico também pode ser usado para procedimentos individuais para atualizar uma instalação existente, por exemplo, para criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.
  
 Para obter informações sobre como adicionar mais servidores [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um farm existente, consulte o seguinte.  
  
-   [Adicionar um servidor de relatório a um farm &#40;Expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Adicionar um front-end da Web do Reporting Services a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 Uma instalação de servidor único é útil em cenários de desenvolvimento e teste, mas não é recomendável em ambientes de produção.  
  
##  <a name="bkmk_singleserver"></a> Implantação de servidor único de exemplo  
 Uma instalação de servidor único é útil em cenários de desenvolvimento e teste, mas não é recomendável em ambientes de produção. O ambiente de servidor único faz referência a um único computador que tenha o SharePoint e os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados no mesmo computador. O tópico não abrange a expansão com vários servidores [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 O diagrama a seguir ilustra os componentes que fazem parte de uma implantação de servidor único do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
 
 > [!NOTE]
 > Para o SharePoint 2016, os Serviços do Excel foram movidos para o Servidor do Office Online e não podem ser usados em uma implantação de servidor único. O Servidor do Office Online deve ser implantado em um servidor diferente. Para obter mais informações, confira [Office Online Server overview](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) (Visão geral do Servidor do Office Online) e [Configure Excel Online administrative settings](https://technet.microsoft.com/library/jj219698\(v=office.16\).aspx)(Definir as configurações administrativas do Excel Online).
  
|||  
|-|-|  
|**(1)**|Serviço do SharePoint instalado da instalação do SQL Server. Você pode criar um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(2)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o suplemento para produtos do SharePoint fornece os componentes de interface do usuário nos servidores do SharePoint.|  
|**(3)**|O Aplicativo do Serviço do Excel usado pelo Power View e [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Isso não está disponível em uma implantação de servidor único para o SharePoint 2016. É necessário um [Servidor do Office Online](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) .|  
|**(4)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
 ![Implantação de servidor único do modo do SharePoint SSRS](../../reporting-services/install-windows/media/rs-sharepoint-1server-deployment.gif "implantação de servidor único do SSRS modo do SharePoint")  
  
> [!TIP]  
>  Para obter exemplos de implantação mais complexos, veja [Topologias de implantação para recursos de BI do SQL Server no SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).  
  
##  <a name="bkmk_setupaccounts"></a> Contas de instalação  
 Esta seção descreve as contas e permissões usadas nas etapas principais de implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.  
  
 **Instalação e registro do serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :**  
  
-   O conta atual durante a instalação (conhecida como conta de ‘instalação’) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint precisa ter direitos administrativos no computador local. Se você estiver instalando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] depois que o SharePoint for instalado e a conta de ‘instalação’ também for um membro do grupo administradores de farm do SharePoint, a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] registrará o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para você. Se você instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes da instalação do SharePoint ou se a conta de ‘instalação’ não for um membro do grupo administradores de farm, registre o serviço manualmente. Consulte a seção [Etapa 2: Registre e inicie o serviço SharePoint do Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Criando aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  
  
-   Após a instalação e o registro do serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , crie um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A “conta de serviço do farm do SharePoint “ precisa ser temporariamente um membro do grupo de administradores local para que o aplicativo de serviço do Reporting Services possa ser criado. Para obter mais informações sobre as permissões de conta do SharePoint 2013, veja [Permissões de conta e configurações de segurança no SharePoint 2013](http://technet.microsoft.com/library/cc678863.aspx) (http://technet.microsoft.com/library/cc678863.aspx) ou para o SharePoint 2016, veja [Permissões de conta e configurações de segurança no SharePoint 2016](https://technet.microsoft.com/library/cc678863\(v=office.16\).aspx).  
  
     É prática recomendada de segurança que as contas de administrador do farm do SharePoint também não sejam contas locais de administrador do sistema operacional. Se você adicionar uma conta de administrador do farm ao grupo de administradores local como parte do processo de instalação, é recomendável remover a conta do grupo de administradores local depois que a instalação for concluída.  
  
##  <a name="bkmk_install_SSRS"></a> Etapa 1: Instalar o servidor de relatório do Reporting Services no modo do SharePoint  
 Essa etapa instala um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint e o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. Dependendo do que já está instalado no computador, você poderá não ver algumas das páginas de instalação descritas nas etapas a seguir.  
 
 > [!IMPORTANT]
 > Para o SharePoint 2016, o servidor do SharePoint em que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será instalado precisa ter a função de servidor **Custom** . A implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] terá êxito em um servidor do SharePoint que não está na função **Custom** , mas durante a próxima janela de manutenção do SharePoint, MinRole interromperá o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , pois detecta que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo integrado do SharePoint não indica suporte para nenhuma das outras funções de servidor do SharePoint. O aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte apenas à função **Custom** .
 
 > [!NOTE]
 > Se você planeja instalar o serviço do Power Pivot também, no SharePoint 2016, instale-o antes de instalar o Reporting Services. O serviço do Power Pivot não pode ser instalado em um servidor do SharePoint na função **Custom** . Isso evitará a necessidade de várias trocas de funções.
 
 ### <a name="apply-the-custom-server-role-to-a-sharepoint-2016-server"></a>Aplicar a função de servidor Custom a um servidor do SharePoint 2016
 
 > [!NOTE]
 > Isso não se aplica ao SharePoint 2013.
 
 1. Faça logon no servidor do SharePoint em que você planeja instalar o [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)](Definir as configurações administrativas do Excel Online).
 
 2. Inicie o **Shell de Gerenciamento do SharePoint 2016** como administrador. 
  
    Clique com o botão direito do mouse no **Shell de Gerenciamento do SharePoint 2016** e selecione **Executar como administrador**.

3. No prompt de comando do PowerShell, execute o comando a seguir.

    > [!NOTE]
    > Verifique se você especificou o nome correto do servidor do SharePoint.
    
        Set-SPServer SERVERNAME -Role Custom

4. Você deve ver uma resposta indicando que um trabalho de temporizador foi agendado. Você precisará aguardar até a execução do trabalho.

5. Use o comando a seguir para verificar a função atribuída do servidor.

        Get-SPServer SERVERNAME 
 
 6. **Role** deve listar **Custom**.
 
 ### <a name="install-reporting-services"></a>Instalar o Reporting Services
  
1.  Execute o Assistente de Instalação do SQL Server (Setup.exe).  
  
2.  Selecione **Instalação** no lado esquerdo do assistente e selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  

3.  Se você vir a página **Chave do Produto** , digite sua chave ou aceite o padrão da ‘Enterprise Evaluation’ edition.  
  
     Selecione **Avançar**.  
  
4.  Se você vir a página Termos de Licença, revise e aceite os termos da licença. A Microsoft agradece se você concordar em enviar os dados de uso de recursos para ajudar a aprimorar os recursos de produto e o suporte.  
  
     Selecione **Avançar**.  

5.  É recomendável selecionar **Usar o Microsoft Update para verificar se há atualizações (recomendável)**. Isso é opcional.
  
     Selecione **Avançar**.   
  
6.  Na páginas **Instalar Arquivos de Instalação** , dependendo do que já está instalado em seu computador, você poderá ver a seguinte mensagem:  
  
    -   "Um ou mais arquivos afetados têm operações pendentes. Reinicie o computador depois que o processo de instalação for concluído."  
  
    -   Selecione **Avançar**.  
  
7.  Se você vir a página **Regras de Instalação** . Analise todos os avisos ou problemas de bloqueio. Em seguida, selecione **Avançar**.
 
8. Selecione o seguinte na página **Seleção de Recurso** :  
  
    -   **Reporting Services – SharePoint**  
  
    -   **Suplemento Reporting Services para produtos do SharePoint**.  
  
    -   Você pode, opcionalmente, selecionar também **Serviços do Mecanismo de Banco de Dados** para um ambiente completo, porém, é necessário ter uma instância do Mecanismo de Banco de Dados do SQL Server que esteja hospedando os bancos de dados do SharePoint.  
  
     Selecione **Avançar**.  
  
     ![rs_SetupFeatureSelection_SharePoint_with_circles](../../reporting-services/install-windows/media/rs-setupfeatureselection-sharepoint-with-circles.png)
  
9. Se você selecionou os serviços do Mecanismo de Banco de Dados, aceite a instância padrão de **MSSQLSERVER** na página **Configuração da Instância** e clique em **Avançar**.  
  
     ![Observação](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Observação")arquitetura de serviço do SharePoint para o Reporting Services não se baseia em uma "instância" do SQL Server como a arquitetura do Reporting Services anterior.  
  
10. Se você vir a página **Configuração do Servidor** , digite as credenciais apropriadas. Se você usar os recursos de alerta de dados ou de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , será necessário alterar o **Tipo de Inicialização** do SQL Server Agent para **Automática**. Você pode não ver a página de **Configuração do Servidor** , dependendo do que já esteja instalado no computador.  
  
     Selecione **Avançar**.  
  
11. Se você selecionou os serviços do Mecanismo de Banco de Dados, a página **Configuração do Mecanismo de Banco de Dados** será exibida. Adicione contas apropriadas à lista de Administradores SQL e selecione **Avançar**.  
  
12. Na página **Configuração do Reporting Services** , você deverá verificar se a opção **Instalar somente** está selecionada. Esta opção instala os arquivos do servidor de relatório e não configura o ambiente do SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    > [!NOTE]
    > Quando a instalação do SQL Server estiver concluída, siga as outras seções deste tópico para configurar o ambiente do SharePoint. Isso inclui a instalação do serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a criação de aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![ssRS-2016-setup-configuration](../../reporting-services/install-windows/media/ssrs-2016-setup-configuration.png)
  
13. Examine todos os avisos e selecione **Avançar** na página **Regras de Configuração de Recurso** se você parar nesta página.  
  
14. Na página **Pronto para Instalar** , examine o resumo da instalação. O resumo incluirá um nó filho do **Modo SharePoint do Reporting Services** que mostra um valor de **SharePointFilesOnlyMode**. Selecione **Instalar**.  
  
15. A instalação levará vários minutos. Você verá a página de **Concluído** com os recursos listados e o status de cada recurso. Você pode ver uma caixa de diálogo de informações indicando que o computador precisa ser reiniciado.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a> Etapa 2: Registre e inicie o serviço SharePoint do Reporting Services  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "conteúdo relacionado ao PowerShell")  
  
> [!NOTE]
> Se você estiver executando a instalação em um farm existente do SharePoint, não será necessário concluir as etapas nesta seção. O serviço do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi instalado e iniciado durante a execução do assistente de instalação do SQL Server como parte da seção anterior deste documento.  
  
 Estes são os motivos comuns pelos quais você precisa registrar manualmente o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Você instalou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes do SharePoint ter sido instalado.  
  
-   A conta usada para instalar o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não era um membro do grupos de administradores do farm do SharePoint. Para obter mais informações, consulte a seção [Setup accounts](#bkmk_setupaccounts).  
  
 Os arquivos necessários foram instalados como parte do assistente de instalação do SQL Server, mas os serviços precisam ser registrados no farm do SharePoint.  
  
 As seguintes etapas o orientam durante a abertura do Shell de Gerenciamento do SharePoint e execução dos cmdlets do PowerShell:  
  
1.  Selecionar o botão **Iniciar**  
  
2.  Selecione o grupo **Produtos do Microsoft SharePoint 2016** ou **Produtos do Microsoft SharePoint 2013** .  
  
3.  Clique com o botão direito do mouse no **Shell de Gerenciamento do SharePoint 2016**ou **Shell de Gerenciamento do SharePoint 2013**e selecione **Executar como administrador**. 

    > [!NOTE]
    > Os comandos do SharePoint não são reconhecidos na janela padrão do Windows PowerShell. Use o **Shell de Gerenciamento do SharePoint**.  
  
4.  Execute o comando PowerShell a seguir para instalar o serviço do SharePoint do Reporting Services. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. **Nenhuma mensagem será retornada** ao shell de gerenciamento quando o comando for executado com êxito:  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  Execute o comando PowerShell a seguir para instalar o proxy de serviço do Reporting Services. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. **Nenhuma mensagem será retornada** ao shell de gerenciamento quando o comando for executado com êxito:  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Execute o comando PowerShell a seguir para iniciar o serviço ou visualizar as anotações abaixo para obter instruções sobre como iniciar o serviço a partir da Administração central do SharePoint:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
    > [!IMPORTANT]
    > Se uma mensagem de erro semelhante à seguinte for exibida:  
    >   
    >     Install-SPRSService: O termo 'Install-SPRSService' **não é reconhecido** como o nome de um cmdlet, função, arquivo de script ou programa operável. Verifique a ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está correto e tente novamente.  
    >
    > Você está no Windows Powershell, e não no Shell de Gerenciamento do SharePoint, ou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não está instalado. Para obter mais informações sobre o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o PowerShell, veja [Cmdlets do PowerShell para Modo do SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
 Também é possível iniciar o serviço a partir da Administração Central do SharePoint, em vez de executar o terceiro comando PowerShell. As etapas a seguir também são úteis para verificar se o serviço está sendo executado.  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Serviços no Servido** no grupo **Configurações do Sistema** .  
  
2.  Encontre o **Serviço SQL Server Reporting Services** e clique em **Iniciar** na coluna Ação.  
  
3.  O status do serviço Reporting Services será alterado de **Interrompido** para **Iniciado**. Se o serviço Reporting Services não estiver na lista, use o PowerShell para instalar o serviço.  
  
    > [!NOTE]  
    >  Se o serviço Reporting Services permanecer com o status **Iniciando** e não for alterado para **Iniciado**, verifique se o serviço “Administração do SharePoint 2013” foi iniciado no Windows Server Manager.  
  
##  <a name="bkmk_create_serrviceapplication"></a> Etapa 3: Criar um aplicativo de serviço do Reporting Services  
 Esta seção fornece as etapas para criar um aplicativo de serviço e uma descrição das propriedades, se você estiver analisando um aplicativo de serviço existente.  
  
1.  Na Administração Central do SharePoint, no grupo **Gerenciamento de Aplicativo** , selecione **Gerenciar Aplicativos de Serviço**.  
  
2.  Na faixa de opções do SharePoint, selecione o botão **Novo** .  
  
3.  No menu Novo, selecione **Aplicativo de Serviço SQL Server Reporting Services**.  
  
    > [!IMPORTANT]  
    >  Se o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] opção não será exibida na lista, é um **indicação de que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] compartilhados do serviço não está instalado**. Analise a seção anterior sobre como usar cmdlts de PowerShell para instalar o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Na página **Criar Aplicativo de Serviço SQL Server Reporting Services** , insira um nome para o aplicativo. Se você estiver criando vários aplicativos de serviço Reporting Services, um nome descritivo ou uma convenção de nomenclatura ajudará a organizar suas operações de administração e gerenciamento.  
  
5.  Na seção **Pool de Aplicativos** , crie um novo pool de aplicativos para o aplicativo (recomendável). Se você usar o mesmo nome para o pool de aplicativos e o aplicativo de serviço, isso poderá facilitar a administração contínua. Isso também poderá ser afetado por quantos aplicativos de serviço você criará e se você precisar usar vários em um único pool de aplicativos. Consulte a documentação do SharePoint sobre recomendações e práticas recomendadas para o gerenciamento do pool de aplicativos.  
  
     Selecione ou crie uma conta de segurança para o pool de aplicativos. Não se esqueça de especificar uma conta de usuário do domínio. Uma conta de usuário de domínio habilita o uso do recurso de conta gerenciado do SharePoint que o deixa atualizar senhas e informações de conta em um único local. Contas de domínio também serão obrigatórias se você pretender diminuir a implantação para incluir instâncias de serviço adicionais a serem executadas sob a mesma identidade.  
  
6.  No **Servidor de Banco de Dados**, você pode usar o servidor atual ou escolher outro SQL Server.  
  
7.  Em **Nome do Banco de Dados** , o valor padrão é `ReportingService_<guid>`, que é o nome de um banco de dados exclusivo. Se você digitar um novo valor, digite um valor exclusivo. Este é o novo banco de dados a ser criado especificamente para o aplicativo de serviços.  
  
8.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher **Autenticação SQL**, consulte a documentação do SharePoint para conhecer as práticas recomendadas sobre como usar esse tipo de autenticação em uma implantação do SharePoint.  
  
9. Na seção **Associação de Aplicativo Web** , selecione o Aplicativo Web a ser provisionado para acesso pelo Aplicativo de Serviço do Reporting Services atual. Você pode associar um aplicativo de serviço do Reporting Services a um aplicativo Web. Se todos os aplicativos Web atuais já estiverem associados a um aplicativo de serviço do Reporting Services, uma mensagem de aviso será exibida.  
  
10. Escolha **OK**.  
  
11. O processo para criar um aplicativo de serviço poderá demorar vários minutos para ser concluído. Quando for concluído, você verá uma mensagem de confirmação e um link para uma página **Provisionar Assinaturas e Alertas** . Conclua a etapa de provisionamento se quiser usar os recursos de assinaturas ou alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Provision Subscriptions and Alerts for SSRS Service Applications](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Conteúdo relacionado ao PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "conteúdo relacionado ao PowerShell") para obter informações sobre como usar o PowerShell para criar um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo de serviço, consulte:  
  
-   Consulte a seguinte seção [Script do Windows PowerShell para as etapas 1 a 4](#bkmk_full_script).  
  
-   Tópico [Para criar um Aplicativo de Serviço Reporting Services usando PowerShell](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  

##  <a name="bkmk_powerview"></a> Etapa 4: Ativar o recurso de coleção de sites do Power View.

 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do SQL Server 2016 Reporting Services suplemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] produtos do SharePoint, é um recurso de coleção de sites. O recurso é ativado automaticamente para coleções de sites raiz e coleções de sites criadas depois que o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado. Se você planejar usar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], verifique se o recurso está ativado.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Produtos do SharePoint depois da instalação do SharePoint Server, o recurso de integração de Servidor de relatório e o recurso de integração do Power View só será ativado para coleções de sites de raiz. Para outras coleções de sites, ative manualmente os recursos.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Para ativar ou verificar o recurso de coleção de sites do Power View.  
  
1.  As etapas a seguir pressupõem que o site do SharePoint esteja configurado para **versão da experiência**2013, pra o SharePoint 2013.  
  
     Abra o navegador para o site do SharePoint desejado. Por exemplo, http://\<servername >/sites/bi  
  
2.  Selecione **configurações**![configurações SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "configurações SharePoint").  
  
3.  Selecione **Configurações de site**.  
  
4.  No grupo **Administração do Conjunto de Sites** , selecione **Recursos do conjunto de sites**.  
  
5.  Localize **Recurso de Integração do Power View** na lista.  
  
6.  Selecione **Ativar**. O status dos recursos será alterado para **Ativo**.  
  
 Este procedimento é concluído para cada coleção de sites. Para obter mais informações, consulte [Activate the Report Server and Power View Integration Features in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md).  
  
##  <a name="bkmk_full_script"></a> Script do Windows PowerShell para as etapas 1 a 4  
 O script do PowerShell nesta seção é o equivalente a concluir as etapas de 1 a 4 nas seções anteriores. O script conclui o seguinte:  
  
-   Instala o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o proxy do serviço, e inicia o serviço.  
  
-   Cria um proxy de serviço chamado "Reporting Services".  
  
-   Cria um aplicativo do serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] chamado "Aplicativo do Reporting Services".  
  
-   Habilita o recurso do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para um conjunto de sites.  
  
 Parâmetros  
  
-   Atualizar o parâmetro **-Account** para o proxy de serviço. A conta deve ser uma conta de serviço gerenciada no farm do SharePoint. Para obter mais informações, consulte o tópico do SharePoint [Plano para as contas administrativas e de serviço no SharePoint 2013](http://technet.microsoft.com/library/cc263445.aspx).  
  
-   Atualizar o parâmetro **–DatabaseServer** para o aplicativo de serviço. Esse parâmetro é a instância do mecanismo de banco de dados  
  
-   Atualizar o parâmetro **–url** do site para o qual você deseja o recurso do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] habilitado.  
  
 **Para usar o script:**  
  
1.  Abra o Windows PowerShell com privilégios administrativos.  
  
2.  Copie o seguinte código para a janela de script.  
  
3.  Atualize os três parâmetros descritos na seção anterior e execute o script.  
  
```  
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy  
  
```  
  
##  <a name="bkmk_additional_config"></a> Configuração adicional  
 Esta seção descreve as etapas de configuração adicionais que são importantes na maioria das implantações do SharePoint.  
  
###  <a name="bkmk_configure_ECS"></a> Configurar os Serviços do Excel e o Power Pivot  
 Se você quiser exibir os relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Power View em uma pasta de trabalho do Excel 2013 ou 2016 no SharePoint, os Serviços do Excel no farm precisam ser configurados para usar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Server no modo do PowerPivot. 
 
 Para o SharePoint 2016, um [Servidor do Office Online](https://technet.microsoft.com/library/jj219456\(v=office.16\).aspx) precisa ser configurado para usar os Serviços do Excel. Para obter informações detalhadas, confira os white papers a seguir.
 
 - [Implantação do SQL Server 2016 PowerPivot e Power View no SharePoint 2016](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
 
 - [Implantando o SQL Server 2016 PowerPivot e Power View em um farm multicamadas do SharePoint 2016](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
 
 Para SharePoint 2016, você precisará criar e configurar um Aplicativo dos Serviços do Excel. Para obter mais informações, consulte o seguinte:  
  
-   A seção “Configurar Serviços do Excel para a integração do Analysis Services” em [Instalar o Analysis Services no Modo do PowerPivot](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
-   [Gerenciar configurações de modelo de dados de Serviços do Excel (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx).  

Além disso, a conta de segurança do pool de aplicativos usada pelo aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deve ser um administrador no servidor do Analysis Services.
  
###  <a name="bkmk_provision_agent"></a> Provisionar Assinaturas e Alertas  
 As assinaturas e os recursos de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem exigir a configuração de permissões do SQL Server Agent. Se você vir uma mensagem de erro indicando que um SQL Server Agent é necessário e tiver verificado que o SQL Server Agent está em execução, atualize as permissões. Você pode clicar no link **Provisionar Assinaturas e Alertas** na página de criação do aplicativo de serviço bem-sucedida para ir para outra página para provisionamento do SQL Server Agent. A etapa de provisionamento será necessária se a sua implantação for cruzar os limites dos computadores, por exemplo, quando a instância de banco de dados do SQL Server estiver em um computador diferente. Para obter mais informações, veja [Provisionar assinaturas e alertas para aplicativos de serviço SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Configurar o email para aplicativos de serviço SSRS  
 O recurso de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envia alertas de dados em mensagens de email. Para enviar um email, talvez seja necessário configurar o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e modificar a extensão de entrega de email do aplicativo de serviço. Se você estiver planejando usar a extensão de entrega de email do recurso de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , as configurações de email serão necessárias. Para obter mais informações, consulte [configurar o email para um aplicativo de serviço do Reporting Services &#40; SharePoint 2013 e SharePoint 2016 &#41; ](http://msdn.microsoft.com/en-us/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f). 
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Adicione os tipos de conteúdo do Reporting Services para bibliotecas de conteúdo  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece tipos de conteúdo predefinidos usados para gerenciar arquivos de fonte de dados compartilhada (.rsds), modelos de relatórios (.smdl) e arquivos de definição de relatório (.rdl) do Construtor de Relatórios. A adição de um tipo de conteúdo do **Construtor de Relatórios**, do **Modelo de Relatório**ou da **Fonte de Dados de Relatório** a uma biblioteca ativa o comando **Novo** para que você possa criar novos documentos desse tipo. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Ativar o recurso de sincronização de arquivo do Servidor de Relatório  
 Se os usuários forem carregar com frequência itens de relatório publicados diretamente nas bibliotecas de documentos do SharePoint, o recurso no nível de site **Sincronização de arquivos do Servidor de Relatório** será útil. O recurso de sincronização de arquivo sincronizará o catálogo do servidor de relatório com itens nas bibliotecas de documentos mais frequentemente. Para obter mais informações, consulte [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).  
  
##  <a name="bkmk_verify_installation"></a> Verificar a instalação  
 Veja a seguir as etapas e os procedimentos sugeridos para verificar a implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Consulte a seção do SharePoint no tópico de verificação [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   Em uma biblioteca de documentos do SharePoint, crie um relatório básico do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que contém somente uma caixa de texto, por exemplo, um título. O relatório não contém fonte de dados ou conjunto de dados. A meta é verificar se você pode abrir o Construtor de Relatórios, criar um relatório básico e visualizar o relatório.  
  
     Salve o relatório em uma biblioteca de documentos e execute o relatório da biblioteca. Para obter mais informações sobre como criar relatórios com o Construtor de Relatórios, veja [Iniciar o Construtor de Relatórios (Construtor de Relatórios)](http://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="next-steps"></a>Próximas etapas

[Cmdlets do PowerShell para Modo do SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
[Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Edições e recursos com suporte para SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)   
[Serviço do Reporting Services do SharePoint e aplicativos de serviço](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
