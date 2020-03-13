---
title: Instalar o Reporting Services modo do SharePoint para SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8874d4c57e2fb7b94e4efac44c90e93865d2b40f
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289614"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>Instalar o Reporting Services SharePoint Mode para SharePoint 2013
  Os procedimentos deste tópico conduzirão você pela instalação de servidor único do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. As etapas incluem a execução do assistente de instalação do SQL Server, bem como as tarefas de configuração que usam a Administração Central do SharePoint. O tópico também pode ser usado para procedimentos individuais para atualizar uma instalação existente, por exemplo, para criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; **Observação:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o modo do **SharePoint não oferece** suporte a multilocação do SharePoint Server.|  
  
 Para obter informações sobre como adicionar mais servidores [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um farm existente, consulte o seguinte.  
  
-   [Adicione um servidor de relatório adicional a um farm &#40;expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Adicionar um front-end da Web do Reporting Services a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 Uma instalação de servidor único é útil em cenários de desenvolvimento e teste, mas não é recomendável em ambientes de produção.  
  
 **Neste tópico:**  
  
-   [Implantação de servidor único de exemplo](#bkmk_singleserver)  
  
-   [Contas de instalação](#bkmk_setupaccounts)  
  
-   [Etapa 1: instalar Reporting Services servidor de relatório no modo do SharePoint](#bkmk_install_SSRS)  
  
-   [Etapa 2: registrar e iniciar o Reporting Services o serviço SharePoint](#bkmk_install_SSRS_sharedservice)  
  
-   [Etapa 3: criar um aplicativo de serviço de Reporting Services](#bkmk_create_serrviceapplication)  
  
-   [Etapa 4: ativar o Power View o recurso de conjunto de sites.](#bkmk_powerview)  
  
-   [Script do Windows PowerShell para as etapas 1-4](#bkmk_full_script)  
  
-   [Configuração adicional](#bkmk_additional_config) , incluindo o provisionamento de assinaturas e alertas, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tipos de conteúdo e configuração de serviços do Excel para usar um servidor de Analysis Services.  
  
-   [Verificar a instalação](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a>Implantação de servidor único de exemplo  
 Uma instalação de servidor único é útil em cenários de desenvolvimento e teste, mas não é recomendável em ambientes de produção. O ambiente de servidor único faz referência a um único computador que tenha o SharePoint e os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados no mesmo computador. O tópico não abrange a expansão com vários servidores [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 O diagrama a seguir ilustra os componentes que fazem parte de uma implantação de servidor único do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|||  
|-|-|  
|**uma**|Serviço do SharePoint instalado da instalação do SQL Server. Você pode criar um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**2**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o suplemento para produtos do SharePoint fornece os componentes de interface do usuário nos servidores do SharePoint.|  
|**Beta**|O Aplicativo dos Serviços do Excel usado pelo Power View e PowerPivot.|  
|**quatro**|Aplicativo de serviço PowerPivot.|  
  
 ![Implantação de servidor de modo único do SSRS SharePoint](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "Implantação de servidor de modo único do SSRS SharePoint")  
  
> [!TIP]  
>  Para obter exemplos de implantação mais complexos, veja [Topologias de implantação para recursos de BI do SQL Server no SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
##  <a name="bkmk_setupaccounts"></a>Contas de instalação  
 Esta seção descreve as contas e permissões usadas nas etapas principais de implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.  
  
 **Instalação e registro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço:**  
  
-   A conta atual durante a instalação (conhecida como a conta de ' instalação ') do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint precisa ter direitos administrativos no computador local. Se você estiver instalando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o após a instalação do SharePoint e a conta de ' instalação ' também for um membro do grupo Administradores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] farm do SharePoint, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a instalação registrará o serviço para você. Se você instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o antes de o SharePoint ser instalado ou a conta de ' instalação ' não for um membro do grupo Administradores de farm, registre o serviço manualmente. Consulte a seção [Etapa 2: Registre e inicie o serviço SharePoint do Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Criando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativos de serviço**  
  
-   Após a instalação e o registro do serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , crie um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A "conta de serviço do farm do SharePoint" precisa ser temporariamente um membro do grupo de administradores local para que o aplicativo de serviço do Reporting Services possa ser criado. Para obter mais informações sobre as permissões de conta do SharePoint 2013, consulte [permissões de conta e configurações de segurança no SharePoint 2013](https://technet.microsoft.com/library/cc678863.aspx) (https://technet.microsoft.com/library/cc678863.aspx).  
  
     É prática recomendada de segurança que as contas de administrador do farm do SharePoint também não sejam contas locais de administrador do sistema operacional. Se você adicionar uma conta de administrador do farm ao grupo de administradores local como parte do processo de instalação, é recomendável remover a conta do grupo de administradores local depois que a instalação for concluída.  
  
##  <a name="bkmk_install_SSRS"></a>Etapa 1: instalar Reporting Services servidor de relatório no modo do SharePoint  
 Essa etapa instala um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint e o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint. Dependendo do que já está instalado no computador, você poderá não ver algumas das páginas de instalação descritas nas etapas a seguir.  
  
1.  Execute o Assistente de Instalação do SQL Server (Setup.exe).  
  
2.  Clique em **Instalação** no lado esquerdo do assistente e clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
3.  Clique em **OK** na página **Regras de Suporte à Instalação** , presumindo que todas as regras foram aprovadas.  
  
4.  Clique em **Instalar** na página **Arquivos de Suporte à Instalação** . Dependendo do que já está instalado em seu computador, você verá a seguinte mensagem:  
  
    -   "Um ou mais arquivos afetados têm operações pendentes. Reinicie o computador depois que o processo de instalação for concluído."  
  
    -   Clique em **OK**.  
  
5.  Clique em **Avançar** depois que os arquivos de suporte tiverem concluído a instalação e as páginas de **Regras de Suporte** mostrarem um status de **Aprovadas**. Analise todos os avisos ou problemas de bloqueio.  
  
6.  Na página **Tipo de Instalação** , clique em **Adicionar recursos a uma instância existente do SQL Server 2014**. Selecione a instância correta na lista suspensa e clique em **Avançar**.  
  
7.  Se você vir a página **chave do produto (Product Key)**, digite sua chave ou aceite o padrão da edição "Enterprise Evaluation".  
  
     Clique em **Próximo**.  
  
8.  Se você vir a página Termos de Licença, revise e aceite os termos da licença. A Microsoft agradece se você clicar e concordar em enviar os dados de uso de recursos para ajudar a aprimorar os recursos de produto e o suporte.  
  
     Clique em **Próximo**.  
  
9. Se você vir a página **Função de instalação** , selecione **Instalação de recurso do SQL Server**  
  
     Clique em **Avançar**.  
  
     ![Instalação de recurso do SQL Server para função de instalação](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalação de recurso do SQL Server para função de instalação")  
  
10. Selecione o seguinte na página **Seleção de Recurso** :  
  
    -   **Reporting Services-SharePoint**  
  
    -   **Reporting Services suplemento para produtos do SharePoint**.  
  
         ![Observação](../../../2014/reporting-services/media/rs-fyinote.png "observação") A opção do assistente de instalação para instalar o suplemento é nova com a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão.  
  
    -   Se você ainda não tiver uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)], também poderá selecionar **Serviços do Mecanismo de Banco de Dados** e **Ferramentas de Gerenciamento Completas** para um ambiente completo.  
  
     Clique em **Próximo**.  
  
     ![Seleção de recurso SSRS para o modo SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "Seleção de recurso SSRS para o modo SharePoint")  
  
11. Se você vir a página **Regras de Instalação** . Analise todos os avisos ou problemas de bloqueio. Em seguida, clique em **Avançar**  
  
12. Se você selecionou os serviços do Mecanismo de Banco de Dados, aceite a instância padrão de **MSSQLSERVER** na página **Configuração da Instância** e clique em **Avançar**.  
  
     ![Observação](../../../2014/reporting-services/media/rs-fyinote.png "observação") A arquitetura de serviço do Reporting Services SharePoint não se baseia em um SQL Server "instância", como era a arquitetura de Reporting Services anterior.  
  
13. Examine a página **Requisitos de Espaço em Disco** e clique em **Avançar**.  
  
14. Se você vir a página **Configuração do Servidor** , digite as credenciais apropriadas. Se você usar os recursos de alerta de dados ou de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , será necessário alterar o **Tipo de Inicialização** do SQL Server Agent para **Automática**. Você pode não ver a página de **Configuração do Servidor** , dependendo do que já esteja instalado no computador.  
  
     Clique em **Próximo**.  
  
15. Se você selecionou os serviços do Mecanismo de Banco de Dados, a página **Configuração do Mecanismo de Banco de Dados** será exibida. Adicione contas apropriadas à lista de Administradores SQL e clique em **Avançar**.  
  
16. Na página **Configuração do Reporting Services** , você deverá verificar se a opção **Instalar somente** está selecionada. Esta opção instala os arquivos do servidor de relatório e não configura o ambiente do SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    > [!NOTE]  
    >  Quando a instalação do SQL Server estiver concluída, siga as outras seções deste tópico para configurar o ambiente do SharePoint. Isso inclui a instalação do serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a criação dos aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![Assistente de instalação do SQL Server - Página de configuração do SSRS](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "Assistente de instalação do SQL Server - Página de configuração do SSRS")  
  
17. Ajude a Microsoft a aperfeiçoar os recursos e os serviços do SQL Server clicando na caixa de seleção para enviar relatórios de erros na página **Relatórios de Erros** .  
  
     Clique em **Próximo**.  
  
18. Revise os avisos e clique em **Avançar** na página **Regras de Configuração da Instalação** .  
  
19. Na página **Pronto para Instalar** , analise o resumo da instalação e clique em **Avançar**. O resumo incluirá um nó filho do **Modo SharePoint do Reporting Services** que mostra um valor de **SharePointFilesOnlyMode**. Clique em **Instalar**.  
  
20. A instalação levará vários minutos. Você verá a página de **Concluído** com os recursos listados e o status de cada recurso. Você pode ver uma caixa de diálogo de informações indicando que o computador precisa ser reiniciado.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a>Etapa 2: registrar e iniciar o Reporting Services o serviço SharePoint  
 ![Conteúdo relacionado ao PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
> [!NOTE]  
>  Se você estiver executando a instalação em um farm existente do SharePoint, não será necessário concluir as etapas nesta seção. O serviço do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi instalado e iniciado durante a execução do assistente de instalação do SQL Server como parte da seção anterior deste documento.  
  
 Estes são os motivos comuns pelos quais você precisa registrar manualmente o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Você instalou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes do SharePoint ter sido instalado.  
  
-   A conta usada para instalar o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não era um membro do grupos de administradores do farm do SharePoint. Para obter mais informações, consulte a seção [Setup accounts](#bkmk_setupaccounts).  
  
 Os arquivos necessários foram instalados como parte do assistente de instalação do SQL Server, mas os serviços precisam ser registrados no farm do SharePoint. A versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] introduz suporte ao PowerShell para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.  
  
 As etapas a seguir orientam você durante a abertura do Shell de Gerenciamento do SharePoint e dos cmdlets de execução:  
  
1.  Clique no botão **Iniciar**  
  
2.  Clique no grupo **Produtos do Microsoft SharePoint 2013** .  
  
3.  Clique com o botão direito do mouse em **Shell de Gerenciamento do SharePoint 2013** e clique em **Executar como administrador**. OBSERVAÇÃO: os comandos do SharePoint não são reconhecidos na janela padrão do Windows PowerShell. Use o **Shell de Gerenciamento do SharePoint 2013**.  
  
4.  Execute o comando PowerShell a seguir para instalar o serviço do SharePoint. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. **Nenhuma mensagem é retornada** ao Shell de gerenciamento quando o comando é concluído com êxito:  
  
    ```powershell
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  Se uma mensagem de erro semelhante à seguinte for exibida:  
    >   
    >  Install-SPRSService: o termo ' Install-SPRSService ' **não é reconhecido** como o  
    > nome de cmdlet, função, arquivo de script ou programa operável. Verifique o  
    > ortografia do nome ou, se um caminho tiver sido incluído, verifique se ele está  
    > correto e tente novamente.  
  
5.  Execute o comando PowerShell a seguir para instalar o proxy de serviço. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. **Nenhuma mensagem é retornada** ao Shell de gerenciamento quando o comando é concluído com êxito:  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  Execute o comando PowerShell a seguir para iniciar o serviço ou visualizar as anotações abaixo para obter instruções sobre como iniciar o serviço a partir da Administração central do SharePoint:  
  
    ```powershell
    Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 Você está no Windows Powershell, e não no Shell de Gerenciamento do SharePoint, ou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não está instalado. Para obter mais informações sobre o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o PowerShell, veja [Cmdlets do PowerShell para Modo do SharePoint do Reporting Services](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
 Também é possível iniciar o serviço a partir da Administração Central do SharePoint, em vez de executar o terceiro comando PowerShell. As etapas a seguir também são úteis para verificar se o serviço está sendo executado.  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Serviços no Servido** no grupo **Configurações do Sistema** .  
  
2.  Encontre o **Serviço SQL Server Reporting Services** e clique em **Iniciar** na coluna Ação.  
  
3.  O status do serviço Reporting Services será alterado de **Interrompido** para **Iniciado**. Se o serviço Reporting Services não estiver na lista, use o PowerShell para instalar o serviço.  
  
    > [!NOTE]  
    >  Se o serviço Reporting Services permanecer com o status **Iniciando** e não for alterado para **Iniciado**, verifique se o serviço "Administração do SharePoint 2013" foi iniciado no Gerenciador do Servidor do Windows.  
  
##  <a name="bkmk_create_serrviceapplication"></a>Etapa 3: criar um aplicativo de serviço de Reporting Services  
 Esta seção fornece as etapas para criar um aplicativo de serviço e uma descrição das propriedades, se você estiver analisando um aplicativo de serviço existente.  
  
1.  Na administração central do SharePoint, no grupo **Gerenciamento de aplicativos** , clique em **gerenciar aplicativos de serviço**.  
  
2.  Na faixa de opções do SharePoint, clique no botão **Novo** .  
  
3.  No menu Novo, clique em **Aplicativo de Serviço SQL Server Reporting Services**.  
  
    > [!IMPORTANT]  
    >  Se a opção do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não aparecer na lista, isso será uma **indicação de que o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não está instalado**. Analise a seção anterior sobre como usar cmdlts de PowerShell para instalar o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Na página **Criar Aplicativo de Serviço SQL Server Reporting Services** , insira um nome para o aplicativo. Se você estiver criando vários aplicativos de serviço Reporting Services, um nome descritivo ou uma convenção de nomenclatura ajudará a organizar suas operações de administração e gerenciamento.  
  
5.  Na seção **Pool de Aplicativos** , crie um novo pool de aplicativos para o aplicativo (recomendável). Se você usar o mesmo nome para o pool de aplicativos e o aplicativo de serviço, isso poderá facilitar a administração contínua. Isso também poderá ser afetado por quantos aplicativos de serviço você criará e se você precisar usar vários em um único pool de aplicativos. Consulte a documentação do SharePoint sobre recomendações e práticas recomendadas para o gerenciamento do pool de aplicativos.  
  
     Selecione ou crie uma conta de segurança para o pool de aplicativos. Não se esqueça de especificar uma conta de usuário do domínio. Uma conta de usuário de domínio habilita o uso do recurso de conta gerenciado do SharePoint que o deixa atualizar senhas e informações de conta em um único local. Contas de domínio também serão obrigatórias se você pretender diminuir a implantação para incluir instâncias de serviço adicionais a serem executadas sob a mesma identidade.  
  
6.  No **Servidor de Banco de Dados**, você pode usar o servidor atual ou escolher outro SQL Server.  
  
7.  Em **Nome do Banco de Dados** , o valor padrão é `ReportingService_<guid>`, que é o nome de um banco de dados exclusivo. Se você digitar um novo valor, digite um valor exclusivo. Este é o novo banco de dados a ser criado especificamente para o aplicativo de serviços.  
  
8.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher **Autenticação SQL**, consulte a documentação do SharePoint para conhecer as práticas recomendadas sobre como usar esse tipo de autenticação em uma implantação do SharePoint.  
  
9. Na seção **Associação de Aplicativo Web** , selecione o Aplicativo Web a ser provisionado para acesso pelo Aplicativo de Serviço do Reporting Services atual. Você pode associar um aplicativo de serviço do Reporting Services a um aplicativo Web. Se todos os aplicativos Web atuais já estiverem associados a um aplicativo de serviço do Reporting Services, uma mensagem de aviso será exibida.  
  
10. Clique em **OK**.  
  
11. O processo para criar um aplicativo de serviço poderá demorar vários minutos para ser concluído. Quando for concluído, você verá uma mensagem de confirmação e um link para uma página **Provisionar Assinaturas e Alertas** . Conclua a etapa de provisionamento se quiser usar os recursos de assinaturas ou alertas de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Provisionar assinaturas e alertas para aplicativos de serviço do SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Conteúdo relacionado ao PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell") Para obter informações sobre como usar o PowerShell [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar um aplicativo de serviço, consulte:  
  
-   Confira a seguinte seção [Script do Windows PowerShell para as etapas 1 a 4](#bkmk_full_script).  
  
-   Tópico [Para criar um aplicativo do serviço Reporting Services usando o PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  
##  <a name="bkmk_powerview"></a>Etapa 4: ativar o Power View o recurso de conjunto de sites.  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] produtos do SharePoint, é um recurso de conjunto de sites. O recurso é ativado automaticamente para coleções de sites raiz e coleções de sites criadas depois que o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado. Se você planejar usar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], verifique se o recurso está ativado.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Produtos do SharePoint depois da instalação do SharePoint Server, o recurso de integração de Servidor de relatório e o recurso de integração do Power View só será ativado para coleções de sites de raiz. Para outras coleções de sites, ative manualmente os recursos.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Para ativar ou verificar o recurso de coleção de sites do Power View.  
  
1.  As etapas a seguir pressupõem que o site do SharePoint esteja configurado para **versão da experiência**2013.  
  
     Abra o navegador para o site do SharePoint desejado. Por exemplo, http://\<servername>/sites/bi  
  
2.  Clique em **configurações**![configurações do SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configurações do SharePoint").  
  
3.  Clique em **configurações do site**.  
  
4.  No grupo **Administração do Conjunto de Sites** , clique em **Recursos do conjunto de sites**.  
  
5.  Localize **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**. O status dos recursos será alterado para **Ativo**.  
  
 Este procedimento é concluído para cada coleção de sites. Para obter mais informações, consulte [Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md).  
  
##  <a name="bkmk_full_script"></a>Script do Windows PowerShell para as etapas 1-4  
 O script do PowerShell nesta seção é o equivalente a concluir as etapas de 1 a 4 nas seções anteriores. O script conclui o seguinte:  
  
-   Instala o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o proxy do serviço, e inicia o serviço.  
  
-   Cria um proxy de serviço chamado "Reporting Services".  
  
-   Cria um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo de serviço chamado "Reporting Services aplicativo".  
  
-   Habilita o recurso do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para um conjunto de sites.  
  
 parâmetros  
  
-   Atualizar o parâmetro **-Account** para o proxy de serviço. A conta deve ser uma conta de serviço gerenciada no farm do SharePoint. Para obter mais informações, consulte o tópico do SharePoint [Plano para as contas administrativas e de serviço no SharePoint 2013](https://technet.microsoft.com/library/cc263445.aspx).  
  
-   Atualizar o parâmetro **-DatabaseServer** para o aplicativo de serviço. Esse parâmetro é a instância do mecanismo de banco de dados  
  
-   Atualiza o parâmetro **-url** do site para o qual você deseja o recurso do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] habilitado.  
  
 **Para usar o script:**  
  
1.  Abra o Windows PowerShell com privilégios administrativos.  
  
2.  Copie o seguinte código para a janela de script.  
  
3.  Atualize os três parâmetros descritos na seção anterior e execute o script.  
  
```powershell
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
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
  
$time = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
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
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
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
  
##  <a name="bkmk_additional_config"></a>Configuração adicional  
 Esta seção descreve as etapas de configuração adicionais que são importantes na maioria das implantações do SharePoint.  
  
###  <a name="bkmk_configure_ECS"></a>Configurar os serviços do Excel e PowerPivot  
 Se você quiser exibir os relatórios do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] em uma pasta de trabalho do Excel 2013 no SharePoint, um aplicativo de Serviços do Excel no farm precisa ser configurado para usar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint. Além disso, a conta de segurança do pool de aplicativos usada pelo aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deve ser um administrador no servidor do Analysis Services. Para saber mais, consulte o seguinte:  
  
-   A seção "configurar os serviços do Excel para Analysis Services integração" na [instalação do PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
-   [Gerenciar configurações do modelo de dados dos serviços do Excel (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx).  
  
###  <a name="bkmk_provision_agent"></a>Provisionar assinaturas e alertas  
 As assinaturas e os recursos de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem exigir a configuração de permissões do SQL Server Agent. Se você vir uma mensagem de erro indicando que um SQL Server Agent é necessário e tiver verificado que o SQL Server Agent está em execução, atualize as permissões. Você pode clicar no link **Provisionar Assinaturas e Alertas** na página de criação do aplicativo de serviço bem-sucedida para ir para outra página para provisionamento do SQL Server Agent. A etapa de provisionamento será necessária se a sua implantação for cruzar os limites dos computadores, por exemplo, quando a instância de banco de dados do SQL Server estiver em um computador diferente. Para obter mais informações, consulte [provisionar assinaturas e alertas para aplicativos de serviço do SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Configurar o email para aplicativos de serviço SSRS  
 O recurso de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envia alertas de dados em mensagens de email. Para enviar um email, talvez seja necessário configurar o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e modificar a extensão de entrega de email do aplicativo de serviço. Se você estiver planejando usar a extensão de entrega de email do recurso de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , as configurações de email serão necessárias. Para obter mais informações, veja [Configurar o email para um serviço de aplicativo do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Adicione os tipos de conteúdo do Reporting Services para bibliotecas de conteúdo  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece tipos de conteúdo predefinidos usados para gerenciar arquivos de fonte de dados compartilhada (.rsds), modelos de relatórios (.smdl) e arquivos de definição de relatório (.rdl) do Construtor de Relatórios. A adição de um tipo de conteúdo do **Construtor de Relatórios**, do **Modelo de Relatório**ou da **Fonte de Dados de Relatório** a uma biblioteca ativa o comando **Novo** para que você possa criar novos documentos desse tipo. Para obter mais informações, consulte [adicionar tipos de conteúdo do servidor de relatório a uma biblioteca &#40;Reporting Services no modo integrado do SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Ativar o recurso de sincronização de arquivo do Servidor de Relatório  
 Se os usuários forem carregar com frequência itens de relatório publicados diretamente nas bibliotecas de documentos do SharePoint, o recurso no nível de site **Sincronização de arquivos do Servidor de Relatório** será útil. O recurso de sincronização de arquivo sincronizará o catálogo do servidor de relatório com itens nas bibliotecas de documentos mais frequentemente. Para obter mais informações, consulte [Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
##  <a name="bkmk_verify_installation"></a>Verificar a instalação  
 Veja a seguir as etapas e os procedimentos sugeridos para verificar a implantação do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Consulte a seção do SharePoint no tópico de verificação [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   Em uma biblioteca de documentos do SharePoint, crie um relatório básico do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que contém somente uma caixa de texto, por exemplo, um título. O relatório não contém fonte de dados ou conjunto de dados. A meta é verificar se você pode abrir o Construtor de Relatórios, criar um relatório básico e visualizar o relatório.  
  
     Salve o relatório em uma biblioteca de documentos e execute o relatório da biblioteca. Para obter mais informações sobre como criar relatórios com o Construtor de Relatórios, veja [Iniciar o Construtor de Relatórios (Construtor de Relatórios)](https://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="see-also"></a>Consulte Também  
 [Cmdlets do PowerShell para o modo do Reporting Services SharePoint](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Roteiro de conteúdo: configurar e configurar o SharePoint Server e o SQL Server BI](https://technet.microsoft.com/library/dn205112.aspx)   
 [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Serviços do Reporting Services SharePoint e aplicativos de serviço](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)
