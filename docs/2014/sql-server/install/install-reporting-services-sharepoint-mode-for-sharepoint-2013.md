---
title: Instalar o Reporting Services SharePoint Mode para SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ec543839524c78f22758e58b391a34e3473ee9b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167786"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>Instalar o Reporting Services SharePoint Mode para SharePoint 2013
  Os procedimentos deste tópico conduzirão você pela instalação de servidor único do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. As etapas incluem a execução do assistente de instalação do SQL Server, bem como as tarefas de configuração que usam a Administração Central do SharePoint. O tópico também pode ser usado para procedimentos individuais para atualizar uma instalação existente, por exemplo, para criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; **Observação:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint **não** dá suporte à multilocação do SharePoint Server.|  
  
 Para obter informações sobre como adicionar mais servidores [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um farm existente, consulte o seguinte.  
  
-   [Adicionar um servidor de relatório a um farm &#40;Expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Adicionar um front-end da Web do Reporting Services a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 Uma instalação de servidor único é útil em cenários de desenvolvimento e teste, mas não é recomendável em ambientes de produção.  
  
 **Neste tópico:**  
  
-   [Exemplo de implantação de servidor único](#bkmk_singleserver)  
  
-   [Contas de instalação](#bkmk_setupaccounts)  
  
-   [Etapa 1: Instalar o Reporting Services Report Server no modo do SharePoint](#bkmk_install_SSRS)  
  
-   [Etapa 2: Registre e inicie o serviço SharePoint do Reporting Services](#bkmk_install_SSRS_sharedservice)  
  
-   [Etapa 3: Criar um aplicativo de serviço do Reporting Services](#bkmk_create_serrviceapplication)  
  
-   [Etapa 4: Ative o recurso de coleção de sites do Power View.](#bkmk_powerview)  
  
-   [Script do Windows PowerShell para obter as etapas 1 a 4](#bkmk_full_script)  
  
-   [Configuração adicional](#bkmk_additional_config) incluindo o provisionamento para assinaturas e alertas, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tipos de conteúdo e configuração dos serviços do Excel para usar um servidor do Analysis Services.  
  
-   [Verificar a instalação](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a> Implantação de servidor único de exemplo  
 Uma instalação de servidor único é útil em cenários de desenvolvimento e teste, mas não é recomendável em ambientes de produção. O ambiente de servidor único faz referência a um único computador que tenha o SharePoint e os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados no mesmo computador. O tópico não abrange a expansão com vários servidores [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 O diagrama a seguir ilustra os componentes que fazem parte de uma implantação de servidor único do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|||  
|-|-|  
|**(1)**|Serviço do SharePoint instalado da instalação do SQL Server. Você pode criar um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(2)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o suplemento para produtos do SharePoint fornece os componentes de interface do usuário nos servidores do SharePoint.|  
|**(3)**|O Aplicativo dos Serviços do Excel usado pelo Power View e PowerPivot.|  
|**(4)**|Aplicativo de serviço PowerPivot.|  
  
 ![Implantação de servidor único no modo do SharePoint do SSRS](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "Implantação de servidor único no modo do SharePoint do SSRS")  
  
> [!TIP]  
>  Para obter exemplos de implantação mais complexos, consulte [topologias de implantação para recursos de BI do SQL Server no SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
##  <a name="bkmk_setupaccounts"></a> Contas de instalação  
 Esta seção descreve as contas e permissões usadas nas etapas principais de implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.  
  
 **Instalação e registro do serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :**  
  
-   O conta atual durante a instalação (conhecida como conta de ‘instalação’) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint precisa ter direitos administrativos no computador local. Se você estiver instalando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] depois que o SharePoint for instalado e a conta de ‘instalação’ também for um membro do grupo administradores de farm do SharePoint, a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] registrará o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para você. Se você instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes da instalação do SharePoint ou se a conta de ‘instalação’ não for um membro do grupo administradores de farm, registre o serviço manualmente. Consulte a seção [Etapa 2: Registre e inicie o serviço SharePoint do Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Criando aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  
  
-   Após a instalação e o registro do serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , crie um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A “conta de serviço do farm do SharePoint “ precisa ser temporariamente um membro do grupo de administradores local para que o aplicativo de serviço do Reporting Services possa ser criado. Para obter mais informações sobre as permissões de conta do SharePoint 2013, consulte [permissões de conta e configurações de segurança no SharePoint 2013](http://technet.microsoft.com/library/cc678863.aspx) (http://technet.microsoft.com/library/cc678863.aspx).  
  
     É prática recomendada de segurança que as contas de administrador do farm do SharePoint também não sejam contas locais de administrador do sistema operacional. Se você adicionar uma conta de administrador do farm ao grupo de administradores local como parte do processo de instalação, é recomendável remover a conta do grupo de administradores local depois que a instalação for concluída.  
  
##  <a name="bkmk_install_SSRS"></a> Etapa 1: Instalar o servidor de relatório do Reporting Services no modo do SharePoint  
 Essa etapa instala um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint e o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. Dependendo do que já está instalado no computador, você poderá não ver algumas das páginas de instalação descritas nas etapas a seguir.  
  
1.  Execute o Assistente de Instalação do SQL Server (Setup.exe).  
  
2.  Clique em **Instalação** no lado esquerdo do assistente e clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
3.  Clique em **OK** na página **Regras de Suporte à Instalação** , presumindo que todas as regras foram aprovadas.  
  
4.  Clique em **Instalar** na página **Arquivos de Suporte à Instalação** . Dependendo do que já está instalado em seu computador, você verá a seguinte mensagem:  
  
    -   "Um ou mais arquivos afetados têm operações pendentes. Reinicie o computador depois que o processo de instalação for concluído."  
  
    -   Clique em **OK**.  
  
5.  Clique em **Avançar** depois que os arquivos de suporte tiverem concluído a instalação e as páginas de **Regras de Suporte** mostrarem um status de **Aprovadas**. Analise todos os avisos ou problemas de bloqueio.  
  
6.  Na página **Tipo de Instalação** , clique em **Adicionar recursos a uma instância existente do SQL Server 2014**. Selecione a instância correta na lista suspensa e clique em **Avançar**.  
  
7.  Se você vir a página **Chave do Produto** , digite sua chave ou aceite o padrão da ‘Enterprise Evaluation’ edition.  
  
     Clique em **Avançar**.  
  
8.  Se você vir a página Termos de Licença, revise e aceite os termos da licença. A Microsoft agradece se você clicar e concordar em enviar os dados de uso de recursos para ajudar a aprimorar os recursos de produto e o suporte.  
  
     Clique em **Avançar**.  
  
9. Se você vir a página **Função de instalação** , selecione **Instalação de recurso do SQL Server**  
  
     Clique em **Avançar**.  
  
     ![Instalação de recurso do SQL Server para a função de instalação](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalação de recurso do SQL Server para a função de instalação")  
  
10. Selecione o seguinte na página **Seleção de Recurso** :  
  
    -   **Reporting Services – SharePoint**  
  
    -   **Suplemento Reporting Services para produtos do SharePoint**.  
  
         ![Observação](../../../2014/reporting-services/media/rs-fyinote.png "Observação") a opção do Assistente de instalação para instalar o suplemento é nova com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de versão.  
  
    -   Se você ainda não tiver uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)], você também poderá selecionar **serviços de mecanismo de banco de dados** e **ferramentas de gerenciamento completo** para um ambiente completo.  
  
     Clique em **Avançar**.  
  
     ![Seleção de recursos SSRS no modo do SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "seleção de recursos SSRS no modo do SharePoint")  
  
11. Se você vir a página **Regras de Instalação** . Analise todos os avisos ou problemas de bloqueio. Em seguida, clique em **Avançar**  
  
12. Se você selecionou os serviços do Mecanismo de Banco de Dados, aceite a instância padrão de **MSSQLSERVER** na página **Configuração da Instância** e clique em **Avançar**.  
  
     ![observação](../../../2014/reporting-services/media/rs-fyinote.png "note")A arquitetura de serviço do SharePoint do Reporting Services não se baseia em uma “instância” do SQL Server, como a arquitetura anterior do Reporting Services.  
  
13. Examine a página **Requisitos de Espaço em Disco** e clique em **Avançar**.  
  
14. Se você vir a página **Configuração do Servidor** , digite as credenciais apropriadas. Se você usar os recursos de alerta de dados ou de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , será necessário alterar o **Tipo de Inicialização** do SQL Server Agent para **Automática**. Você pode não ver a página de **Configuração do Servidor** , dependendo do que já esteja instalado no computador.  
  
     Clique em **Avançar**.  
  
15. Se você selecionou os serviços do Mecanismo de Banco de Dados, a página **Configuração do Mecanismo de Banco de Dados** será exibida. Adicione contas apropriadas à lista de Administradores SQL e clique em **Avançar**.  
  
16. Na página **Configuração do Reporting Services** , você deverá verificar se a opção **Instalar somente** está selecionada. Esta opção instala os arquivos do servidor de relatório e não configura o ambiente do SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    > [!NOTE]  
    >  Quando a instalação do SQL Server estiver concluída, siga as outras seções deste tópico para configurar o ambiente do SharePoint. Isso inclui a instalação do serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a criação dos aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     ![Assistente de instalação do SQL Server - página de configuração do SSRS](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "Assistente de instalação do SQL Server - página de configuração do SSRS")  
  
17. Ajude a Microsoft a aperfeiçoar os recursos e os serviços do SQL Server clicando na caixa de seleção para enviar relatórios de erros na página **Relatórios de Erros** .  
  
     Clique em **Avançar**.  
  
18. Revise os avisos e clique em **Avançar** na página **Regras de Configuração da Instalação** .  
  
19. Na página **Pronto para Instalar** , analise o resumo da instalação e clique em **Avançar**. O resumo incluirá um nó filho do **Modo SharePoint do Reporting Services** que mostra um valor de **SharePointFilesOnlyMode**. Clique em **Instalar**.  
  
20. A instalação levará vários minutos. Você verá a página de **Concluído** com os recursos listados e o status de cada recurso. Você pode ver uma caixa de diálogo de informações indicando que o computador precisa ser reiniciado.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a> Etapa 2: Registre e inicie o serviço SharePoint do Reporting Services  
 ![Conteúdo relacionado ao PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
> [!NOTE]  
>  Se você estiver executando a instalação em um farm existente do SharePoint, não será necessário concluir as etapas nesta seção. O serviço do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi instalado e iniciado durante a execução do assistente de instalação do SQL Server como parte da seção anterior deste documento.  
  
 Estes são os motivos comuns pelos quais você precisa registrar manualmente o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Você instalou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes do SharePoint ter sido instalado.  
  
-   A conta usada para instalar o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não era um membro do grupos de administradores do farm do SharePoint. Para obter mais informações, consulte a seção [Setup accounts](#bkmk_setupaccounts).  
  
 Os arquivos necessários foram instalados como parte do assistente de instalação do SQL Server, mas os serviços precisam ser registrados no farm do SharePoint. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão introduz o suporte do PowerShell para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.  
  
 As etapas a seguir orientam você durante a abertura do Shell de Gerenciamento do SharePoint e dos cmdlets de execução:  
  
1.  Clique no botão **Iniciar**  
  
2.  Clique no grupo **Produtos do Microsoft SharePoint 2013** .  
  
3.  Clique com o botão direito do mouse em **Shell de Gerenciamento do SharePoint 2013** e clique em **Executar como administrador**. OBSERVAÇÃO: os comandos do SharePoint não são reconhecidos na janela padrão do Windows PowerShell. Use o **Shell de Gerenciamento do SharePoint 2013**.  
  
4.  Execute o comando PowerShell a seguir para instalar o serviço do SharePoint. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. **Nenhuma mensagem será retornada** ao shell de gerenciamento quando o comando for executado com êxito:  
  
    ```  
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  Se uma mensagem de erro semelhante à seguinte for exibida:  
    >   
    >  Install-SPRSService: O termo 'Install-SPRSService' **não é reconhecido** como o  
    > nome de cmdlet, função, arquivo de script ou programa operável. Verifique a  
    > ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está  
    > correto e tente novamente.  
  
5.  Execute o comando PowerShell a seguir para instalar o proxy de serviço. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. **Nenhuma mensagem será retornada** ao shell de gerenciamento quando o comando for executado com êxito:  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Execute o comando PowerShell a seguir para iniciar o serviço ou visualizar as anotações abaixo para obter instruções sobre como iniciar o serviço a partir da Administração central do SharePoint:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 Você está no Windows Powershell, e não no Shell de Gerenciamento do SharePoint, ou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não está instalado. Para obter mais informações sobre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o PowerShell, consulte [cmdlets do PowerShell para o Reporting Services SharePoint Mode](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
 Também é possível iniciar o serviço a partir da Administração Central do SharePoint, em vez de executar o terceiro comando PowerShell. As etapas a seguir também são úteis para verificar se o serviço está sendo executado.  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Serviços no Servido** no grupo **Configurações do Sistema** .  
  
2.  Encontre o **Serviço SQL Server Reporting Services** e clique em **Iniciar** na coluna Ação.  
  
3.  O status do serviço Reporting Services será alterado de **Interrompido** para **Iniciado**. Se o serviço Reporting Services não estiver na lista, use o PowerShell para instalar o serviço.  
  
    > [!NOTE]  
    >  Se o serviço Reporting Services permanecer com o status **Iniciando** e não for alterado para **Iniciado**, verifique se o serviço “Administração do SharePoint 2013” foi iniciado no Windows Server Manager.  
  
##  <a name="bkmk_create_serrviceapplication"></a> Etapa 3: Criar um aplicativo de serviço do Reporting Services  
 Esta seção fornece as etapas para criar um aplicativo de serviço e uma descrição das propriedades, se você estiver analisando um aplicativo de serviço existente.  
  
1.  Na Administração Central do SharePoint, no grupo **Gerenciamento de Aplicativo** , clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Na faixa de opções do SharePoint, clique no botão **Novo** .  
  
3.  No menu Novo, clique em **Aplicativo de Serviço SQL Server Reporting Services**.  
  
    > [!IMPORTANT]  
    >  Se o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] opção não será exibida na lista, ele é um **indicação de que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] compartilhado de serviço não está instalado**. Analise a seção anterior sobre como usar cmdlts de PowerShell para instalar o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Na página **Criar Aplicativo de Serviço SQL Server Reporting Services** , insira um nome para o aplicativo. Se você estiver criando vários aplicativos de serviço Reporting Services, um nome descritivo ou uma convenção de nomenclatura ajudará a organizar suas operações de administração e gerenciamento.  
  
5.  Na seção **Pool de Aplicativos** , crie um novo pool de aplicativos para o aplicativo (recomendável). Se você usar o mesmo nome para o pool de aplicativos e o aplicativo de serviço, isso poderá facilitar a administração contínua. Isso também poderá ser afetado por quantos aplicativos de serviço você criará e se você precisar usar vários em um único pool de aplicativos. Consulte a documentação do SharePoint sobre recomendações e práticas recomendadas para o gerenciamento do pool de aplicativos.  
  
     Selecione ou crie uma conta de segurança para o pool de aplicativos. Não se esqueça de especificar uma conta de usuário do domínio. Uma conta de usuário de domínio habilita o uso do recurso de conta gerenciado do SharePoint que o deixa atualizar senhas e informações de conta em um único local. Contas de domínio também serão obrigatórias se você pretender diminuir a implantação para incluir instâncias de serviço adicionais a serem executadas sob a mesma identidade.  
  
6.  No **Servidor de Banco de Dados**, você pode usar o servidor atual ou escolher outro SQL Server.  
  
7.  Em **Nome do Banco de Dados** , o valor padrão é `ReportingService_<guid>`, que é o nome de um banco de dados exclusivo. Se você digitar um novo valor, digite um valor exclusivo. Este é o novo banco de dados a ser criado especificamente para o aplicativo de serviços.  
  
8.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher **Autenticação SQL**, consulte a documentação do SharePoint para conhecer as práticas recomendadas sobre como usar esse tipo de autenticação em uma implantação do SharePoint.  
  
9. Na seção **Associação de Aplicativo Web** , selecione o Aplicativo Web a ser provisionado para acesso pelo Aplicativo de Serviço do Reporting Services atual. Você pode associar um aplicativo de serviço do Reporting Services a um aplicativo Web. Se todos os aplicativos Web atuais já estiverem associados a um aplicativo de serviço do Reporting Services, uma mensagem de aviso será exibida.  
  
10. Clique em **OK**.  
  
11. O processo para criar um aplicativo de serviço poderá demorar vários minutos para ser concluído. Quando for concluído, você verá uma mensagem de confirmação e um link para uma página **Provisionar Assinaturas e Alertas** . Conclua a etapa de provisionamento se quiser usar os recursos de assinaturas ou alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Provisionar assinaturas e alertas para aplicativos de serviço do SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Conteúdo relacionado ao PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "conteúdo relacionado ao PowerShell") para obter informações sobre como usar o PowerShell para criar um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo de serviço, consulte:  
  
-   Consulte a seguinte seção [Script do Windows PowerShell para as etapas 1 a 4](#bkmk_full_script).  
  
-   Tópico [Para criar um aplicativo do serviço Reporting Services usando o PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  
##  <a name="bkmk_powerview"></a> Etapa 4: Ativar o recurso de coleção de sites do Power View.  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] produtos do SharePoint, é um recurso de coleção de sites. O recurso é ativado automaticamente para coleções de sites raiz e coleções de sites criadas depois que o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado. Se você planejar usar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], verifique se o recurso está ativado.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Produtos do SharePoint depois da instalação do SharePoint Server, o recurso de integração de Servidor de relatório e o recurso de integração do Power View só será ativado para coleções de sites de raiz. Para outras coleções de sites, ative manualmente os recursos.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Para ativar ou verificar o recurso de coleção de sites do Power View.  
  
1.  As etapas a seguir pressupõem que o site do SharePoint esteja configurado para **versão da experiência**2013.  
  
     Abra o navegador para o site do SharePoint desejado. Por exemplo, http://\<servername>/sites/bi  
  
2.  Clique em **as configurações**![configurações do SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Settings").  
  
3.  Clique em **Configurações de site**.  
  
4.  No grupo **Administração do Conjunto de Sites** , clique em **Recursos do conjunto de sites**.  
  
5.  Localize **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**. O status dos recursos será alterado para **Ativo**.  
  
 Este procedimento é concluído para cada coleção de sites. Para obter mais informações, consulte [ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md).  
  
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
  
###  <a name="bkmk_configure_ECS"></a> Configurar os serviços do Excel e PowerPivot  
 Se você quiser exibir [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] relatórios do Power View em uma pasta de trabalho do Excel 2013 no SharePoint, um aplicativo de serviços do Excel no farm precisa ser configurado para usar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] servidor no modo do SharePoint. Além disso, a conta de segurança do pool de aplicativos usada pelo aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deve ser um administrador no servidor do Analysis Services. Para obter mais informações, consulte o seguinte:  
  
-   A seção "configurar serviços do Excel para integração do Analysis Services" na [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
-   [Gerenciar configurações de modelo de dados de Serviços do Excel (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx).  
  
###  <a name="bkmk_provision_agent"></a> Provisionar Assinaturas e Alertas  
 As assinaturas e os recursos de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem exigir a configuração de permissões do SQL Server Agent. Se você vir uma mensagem de erro indicando que um SQL Server Agent é necessário e tiver verificado que o SQL Server Agent está em execução, atualize as permissões. Você pode clicar no link **Provisionar Assinaturas e Alertas** na página de criação do aplicativo de serviço bem-sucedida para ir para outra página para provisionamento do SQL Server Agent. A etapa de provisionamento será necessária se a sua implantação for cruzar os limites dos computadores, por exemplo, quando a instância de banco de dados do SQL Server estiver em um computador diferente. Para obter mais informações, veja [Provisionar assinaturas e alertas para aplicativos de serviço SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Configurar o email para aplicativos de serviço SSRS  
 O recurso de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envia alertas de dados em mensagens de email. Para enviar um email, talvez seja necessário configurar o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e modificar a extensão de entrega de email do aplicativo de serviço. Se você estiver planejando usar a extensão de entrega de email do recurso de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , as configurações de email serão necessárias. Para obter mais informações, consulte [configurar o email para um aplicativo de serviço do Reporting Services &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Adicione os tipos de conteúdo do Reporting Services para bibliotecas de conteúdo  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece tipos de conteúdo predefinidos usados para gerenciar arquivos de fonte de dados compartilhada (.rsds), modelos de relatórios (.smdl) e arquivos de definição de relatório (.rdl) do Construtor de Relatórios. A adição de um tipo de conteúdo do **Construtor de Relatórios**, do **Modelo de Relatório**ou da **Fonte de Dados de Relatório** a uma biblioteca ativa o comando **Novo** para que você possa criar novos documentos desse tipo. Para obter mais informações, consulte [Adicionar servidor de tipos de conteúdo relatório em uma biblioteca do &#40;Reporting Services no modo integrado do SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Ativar o recurso de sincronização de arquivo do Servidor de Relatório  
 Se os usuários forem carregar com frequência itens de relatório publicados diretamente nas bibliotecas de documentos do SharePoint, o recurso no nível de site **Sincronização de arquivos do Servidor de Relatório** será útil. O recurso de sincronização de arquivo sincronizará o catálogo do servidor de relatório com itens nas bibliotecas de documentos mais frequentemente. Para obter mais informações, consulte [Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
##  <a name="bkmk_verify_installation"></a> Verificar a instalação  
 Veja a seguir as etapas e os procedimentos sugeridos para verificar a implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Consulte a seção do SharePoint no tópico de verificação [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   Em uma biblioteca de documentos do SharePoint, crie um relatório básico do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que contém somente uma caixa de texto, por exemplo, um título. O relatório não contém fonte de dados ou conjunto de dados. A meta é verificar se você pode abrir o Construtor de Relatórios, criar um relatório básico e visualizar o relatório.  
  
     Salve o relatório em uma biblioteca de documentos e execute o relatório da biblioteca. Para obter mais informações sobre como criar relatórios com o Construtor de Relatórios, veja [Iniciar o Construtor de Relatórios (Construtor de Relatórios)](http://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Cmdlets do PowerShell para o Reporting Services no modo do SharePoint](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Roteiro do conteúdo: Instalar e configurar o SharePoint Server e o BI do SQL Server](http://technet.microsoft.com/library/dn205112.aspx)   
 [Recursos com suporte nas edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473)   
 [Serviço SharePoint do Reporting Services e aplicativos de serviço](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  
