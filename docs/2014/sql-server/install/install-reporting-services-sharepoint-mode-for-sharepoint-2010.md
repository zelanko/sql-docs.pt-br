---
title: Instalar o Reporting Services SharePoint Mode para SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 765713eba66f571e14328351413011762ec71a4b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122553"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>Instalar o Reporting Services no modo do SharePoint para SharePoint 2010
  Os procedimentos neste tópico guiam você por meio de uma instalação de servidor único de um servidor de relatório do Reporting Services no modo do SharePoint. As etapas incluem a execução do assistente de instalação do SQL Server, bem como as tarefas de configuração adicionais que usam a administração central do SharePoint 2010. O tópico também pode ser usado para procedimentos individuais para uma instalação existente, por exemplo, para criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter informações sobre como adicionar adicionais [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidores a um farm existente, consulte [adicionar um servidor de relatório a um Farm &#40;expansão do SSRS&#41; ](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [adicionar um adicionais Web do Reporting Services Front-end a um Farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 Uma instalação de servidor único é útil para cenários de desenvolvimento e teste, mas não é recomendável para ambientes de produção.  
  
> [!NOTE]  
>  Para obter informações sobre como atualizar existente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalação no modo do SharePoint para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  

  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
  
-   > [!IMPORTANT]  
    >  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager não é mais necessário ou aceito na configuração e administração do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Use a Administração Central do SharePoint para configurar um servidor de relatório em modo SharePoint. Para obter mais informações, consulte [gerenciar um aplicativo de serviço Reporting Services SharePoint](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
-   Analise os tópicos a seguir para requisitos, inclusive produtos do SharePoint 2010:  
  
    -   [Notas de versão online](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   Este tópico não aborda a instalação de Produtos do SharePoint 2010. Para obter mais informações, consulte [diretrizes para usar recursos de BI do SQL Server em um Farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md).  
  
-   Estes procedimentos são destinados para configurar um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e não funcionam para versões anteriores do servidor de relatório. Versões anteriores do servidor de relatório não usavam a arquitetura de Serviço Compartilhado do SharePoint. Por exemplo, os servidores de relatório do SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e do SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Verifique se o **administração do SharePoint 2010** serviço é iniciado no Windows Server Manager.  
  
 ![Componentes do SSRS em uma instalação de 1 servidor](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "componentes do SSRS em uma instalação de 1 servidor")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>Considerações sobre banco de dados para uma configuração de servidor único  
  
-   O Reporting Services e os produtos e as tecnologias do SharePoint usam os bancos de dados relacionais do SQL Server para armazenar dados de aplicativo.  
  
-   O [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] requer uma instância do SQL Engine compatível com o SQL Server Evaluation Edition.  
  
-   Os produtos do SharePoint poderão usar uma instância de banco de dados existente. Se uma instância do mecanismo de banco de dados não estiver instalada, o programa de instalação dos produtos do SharePoint instala o SQL Server Express Edition para os bancos de dados de aplicativo do SharePoint.  
  
-   A instância do servidor de relatório não pode usar o SQL Server Express Edition para seu banco de dados. No entanto, a instância do SQL Server Express Edition instalada pelo produto ou tecnologia do SharePoint pode existir lado a lado com outras edições do Mecanismo de Banco de Dados.  
  

  
##  <a name="bkmk_install_SSRS"></a> Instalar o servidor de relatório do Reporting Services no modo do SharePoint  
  
1.  Execute o SQL Server para executar o Assistente de Instalação.  
  
2.  Clique em **Instalação** no lado esquerdo do assistente e clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
3.  Clique em **OK** na página **Regras de Suporte à Instalação** , presumindo que todas as regras foram aprovadas.  
  
4.  Clique em **Instalar** na página **Arquivos de Suporte à Instalação** .  
  
5.  Clique em **próximo** depois que os arquivos de suporte tiverem concluído a instalação e as regras de suporte mostrarem um status de **passado**. Analise todos os avisos ou problemas de bloqueio.  
  
6.  Sobre o **chave do produto** página, digite sua chave ou aceite o padrão da 'Enterprise Evaluation' edition.  
  
     Clique em **Avançar**.  
  
7.  Examine e aceite os termos de licença. A Microsoft agradece se você clicar e concordar em enviar os dados de uso de recursos para ajudar a aprimorar os recursos de produto e o suporte.  
  
     Clique em **Avançar**.  
  
8.  Selecione **instalação de recurso do SQL Server** no **função de instalação** página.  
  
     Clique em **Avançar**.  
  
     ![Instalação de recurso do SQL Server para a função de instalação](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalação de recurso do SQL Server para a função de instalação")  
  
9. Selecione o seguinte na página **Seleção de Recurso** :  
  
    -   **Reporting Services – SharePoint**  
  
    -   **Reporting Services add-in para produtos do SharePoint 2010**. ![Observação](../../../2014/reporting-services/media/rs-fyinote.png "Observação")a opção do Assistente de instalação para instalar o suplemento é nova com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de versão.  
  
    -   Se você ainda não tiver uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)], também é possível selecionar **serviços de mecanismo de banco de dados** e **ferramentas de gerenciamento completo** para um ambiente completo.  
  
     Clique em **Avançar**.  
  
     ![Seleção de recursos SSRS no modo do SharePoint](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "seleção de recursos SSRS no modo do SharePoint")  
  
10. Clique em **próximo** no **regras de instalação** página. Analise todos os avisos ou problemas de bloqueio.  
  
11. Se você selecionou os serviços do Mecanismo de Banco de Dados, aceite a instância padrão de **MSSQLSERVER** na página **Configuração da Instância** e clique em **Avançar**. A arquitetura do serviço compartilhado do Reporting Services não se baseia em uma instância do SQL Server, como a arquitetura do Reporting Services anterior.  
  
12. Examine a página **Requisitos de Espaço em Disco** e clique em **Avançar**.  
  
13. Sobre o **configuração do servidor** página Digite as credenciais apropriadas. Se você usar os recursos de alerta de dados ou de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , será necessário alterar o **Tipo de Inicialização** do SQL Server Agent para **Automática**.  
  
     Clique em **Avançar**.  
  
14. Se você selecionou os serviços do Mecanismo de Banco de Dados, a página **Configuração do Mecanismo de Banco de Dados** será exibida. Adicione contas apropriadas à lista de Administradores SQL e clique em **Avançar**.  
  
15. Na página **Configuração do Reporting Services** , você deverá verificar se a opção **Instalar somente** está selecionada. Esta opção instalará os arquivos do servidor de relatório, ela não configurará o ambiente do SharePoint para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Quando a instalação do SQL Server for concluída, siga as outras seções deste tópico para configurar o ambiente do SharePoint. Isso inclui a instalação do serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a criação dos aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. Ajude a Microsoft a aperfeiçoar os recursos e os serviços do SQL Server clicando na caixa de seleção para enviar relatórios de erros na página **Relatórios de Erros** .  
  
     Clique em **Avançar**.  
  
17. Revise os avisos e clique em **Avançar** na página **Regras de Configuração da Instalação** .  
  
18. Na página **Pronto para Instalar** , analise o resumo da instalação e clique em **Avançar**. O resumo incluirá um **Reporting Services** nó que incluirá o valor do modo de instalação de **SharePointFilesOnlyMode** , bem como as informações da conta.  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a> Instalar e iniciar o serviço de SharePoint do Reporting Services  
 ![Conteúdo relacionado ao PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")  
  
> [!NOTE]  
>  Se você estiver instalando em um farm do SharePoint existente, **você não precisa** concluir as etapas nesta seção. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] serviço do SharePoint foi instalado e iniciado quando você executou o Assistente de instalação do SQL Server na seção anterior.  
  
 Os arquivos necessários foram instalados como parte do assistente de instalação do SQL Server, mas os serviços precisam ser registrados no farm do SharePoint. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão introduz o suporte ao PowerShell [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint. As etapas a seguir orientam você durante a abertura do Shell de Gerenciamento do SharePoint e dos cmdlets de execução:  
  
1.  Clique no botão **Iniciar**  
  
2.  Clique o **produtos Microsoft SharePoint 2010** grupo.  
  
3.  Clique com botão direito **Shell de gerenciamento do SharePoint 2010** clique **executar como administrador**.  
  
4.  Execute o comando PowerShell a seguir para instalar o serviço do SharePoint. Uma execução bem-sucedida do comando resultará em uma nova linha no shell de gerenciamento. Nenhuma mensagem será retornada ao shell de gerenciamento quando o comando for executado com êxito:  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  Execute o comando PowerShell a seguir para instalar o proxy de serviço.  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Execute o comando PowerShell a seguir para iniciar o serviço ou visualizar as anotações abaixo para obter instruções sobre como iniciar o serviço a partir da Administração central do SharePoint:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 Também é possível iniciar o serviço a partir da Administração Central do SharePoint, em vez de executar o terceiro comando PowerShell. As etapas a seguir também são úteis para verificar se o serviço está sendo executado.  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Serviços no Servido** no grupo **Configurações do Sistema** .  
  
2.  Encontre o **Serviço SQL Server Reporting Services** e clique em **Iniciar** na coluna Ação.  
  
3.  O status do serviço Reporting Services será alterado de **Interrompido** para **Iniciado**. Se o serviço Reporting Services não estiver na lista, use o PowerShell para instalar o serviço.  
  
    > [!NOTE]  
    >  Se o serviço do Reporting Services permanecer o **iniciando** status e não se altera para **iniciado**, verifique se o serviço 'Administração do SharePoint 2010' foi iniciado no Windows Server Manager.  
  

  
##  <a name="bkmk_create_serrviceapplication"></a> Criar um aplicativo de serviço do Reporting Services  
 Esta seção fornece as etapas para criar um aplicativo de serviço e uma descrição das propriedades, se você estiver analisando um aplicativo de serviço existente.  
  
1.  Na Administração Central do SharePoint, no grupo **Gerenciamento de Aplicativo** , clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Na faixa de opções do SharePoint, clique no botão **Novo** .  
  
3.  No menu Novo, clique em **Aplicativo de Serviço SQL Server Reporting Services**.  
  
    > [!WARNING]  
    >  Se o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] opção não será exibida na lista, é um **indicação de que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] compartilhados do serviço não está instalado**. Analise a seção anterior sobre como usar cmdlts de PowerShell para instalar o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Na página **Criar Aplicativo de Serviço SQL Server Reporting Services** , insira um nome para o aplicativo. Se você estiver criando vários aplicativos de serviço Reporting Services, um nome descritivo ou uma convenção de nomenclatura organizará suas operações de gerenciamento e administração.  
  
5.  Na seção **Pool de Aplicativos** , crie um novo pool de aplicativos para o aplicativo (recomendável). O uso do mesmo nome para o novo pool de aplicativos do aplicativo de serviço facilita sua administração contínua.  
  
     Selecione ou crie uma conta gerenciada para o pool de aplicativos. Não se esqueça de especificar uma conta de usuário do domínio. Uma conta de usuário de domínio habilita o uso do recurso de conta gerenciado do SharePoint que o deixa atualizar senhas e informações de conta em um único local. Contas de domínio também serão obrigatórias se você pretender diminuir a implantação para incluir instâncias de serviço adicionais a serem executadas sob a mesma identidade.  
  
6.  No **Servidor de Banco de Dados**, você pode usar o servidor atual ou escolher outro SQL Server.  
  
7.  Em **Nome do Banco de Dados** , o valor padrão é `ReportingService_<guid>`, que é o nome de um banco de dados exclusivo. Se você digitar um novo valor, digite um valor exclusivo.  
  
8.  Em **Autenticação de Banco de dados**, o padrão é Autenticação do Windows. Se você escolher **Autenticação SQL**, consulte o guia de práticas recomendadas do administrador do SharePoint para saber como usar esse tipo de autenticação em uma implantação do SharePoint.  
  
9. Na seção **Associação de Aplicativo Web** , selecione o Aplicativo Web a ser provisionado para acesso pelo Aplicativo de Serviço do Reporting Services atual. Você pode associar um aplicativo de serviço do Reporting Services a um aplicativo Web. Se todos os aplicativos Web atuais já estiverem associados a um aplicativo de serviço do Reporting Services, uma mensagem de aviso será exibida.  
  
10. Clique em **OK**.  
  
11. O processo para criar um aplicativo de serviço poderá demorar vários minutos para ser concluído. Quando for concluído, você verá uma mensagem de confirmação e um link para uma página **Provisionar Assinaturas e Alertas** . Conclua a etapa de provisionamento se quiser usar os recursos de assinaturas e alertas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Provisionar assinaturas e alertas para aplicativos de serviço do SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![Conteúdo relacionado ao PowerShell](../../../2014/reporting-services/media/rs-powershellicon.jpg "conteúdo relacionado ao PowerShell") para obter informações sobre como usar o PowerShell para criar um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo de serviço, consulte [para criar um aplicativo de serviço do Reporting Services usando o PowerShell](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp).  
  

  
##  <a name="bkmk_powerview"></a> Ative o recurso de coleção de sites do Power View.  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition, é um recurso de coleção de sites. O recurso é ativado automaticamente para coleções de sites raiz e coleções de sites criadas depois que o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado. Se você planejar usar o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], verifique se o recurso está ativado.  
  
 Se você instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Produtos SharePoint 2010 depois da instalação do produto SharePoint 2010, o recurso de integração de Servidor de Relatório e o recurso de integração do Power View serão ativados apenas para coleções de sites raiz. Para outras coleções de sites, ative manualmente os recursos.  
  
#### <a name="to-activate-the-power-view-feature"></a>Para ativar o recurso do Power View  
  
1.  Abra o navegador para o site do SharePoint desejado.  
  
2.  Clique em **Ações do Site**.  
  
3.  Clique em **Configurações de Site**.  
  
4.  Clique em **Recursos do Conjunto de Sites** no Grupo Administração do Conjunto de Sites.  
  
5.  Localize **Recurso de Integração do Power View** na lista.  
  
6.  Clique em **Ativar**.  
  
 Este procedimento é concluído para cada coleção de sites. Para obter mais informações, consulte [ativar o servidor de relatório e recursos de integração do Power View no SharePoint](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md) .  
  
##  <a name="bkmk_additional_config"></a> Configuração adicional  
 Esta seção descreve as etapas de configuração adicionais que são importantes na maioria das implantações do SharePoint.  
  
###  <a name="bkmk_provision_agent"></a> Provisionar Assinaturas e Alertas  
 As assinaturas e os recursos de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem exigir a configuração de permissões do SQL Server Agent. Se você vir uma mensagem de erro indicando que um SQL Server Agent é necessário e tiver verificado que o SQL Server Agent está em execução, atualize as permissões. Você pode clicar no link **Provisionar Assinaturas e Alertas** na página de criação do aplicativo de serviço bem-sucedida para ir para outra página para provisionamento do SQL Server Agent. A etapa de provisionamento será necessária se a sua implantação for cruzar os limites dos computadores, por exemplo, quando a instância de banco de dados do SQL Server estiver em um computador diferente. Para obter mais informações, veja [Provisionar assinaturas e alertas para aplicativos de serviço SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>Configurar o email para um aplicativo de serviço  
 O recurso de alerta de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envia alertas de dados em mensagens de email. Para enviar um email, talvez seja necessário configurar o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e modificar a extensão de entrega de email do aplicativo de serviço. Se você estiver planejando usar a extensão de entrega de email do recurso de assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , as configurações de email serão necessárias. Para obter mais informações, consulte [configurar o email para um aplicativo de serviço do Reporting Services &#40;do SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  

  
### <a name="add-reporting-services-content-types"></a>Adicionar tipos de conteúdo do Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece tipos de conteúdo predefinidos usados para gerenciar arquivos de fonte de dados compartilhada (.rsds), modelos de relatórios (.smdl) e arquivos de definição de relatório (.rdl) do Construtor de Relatórios. A adição de um tipo de conteúdo do **Construtor de Relatórios**, do **Modelo de Relatório**ou da **Fonte de Dados de Relatório** a uma biblioteca ativa o comando **Novo** para que você possa criar novos documentos desse tipo. Para obter mais informações, consulte [Adicionar relatório servidor tipos de conteúdo em uma biblioteca &#40;Reporting Services no modo integrado do SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  

  
### <a name="activate-the-file-sync-feature"></a>Ativar o recurso de sincronização de arquivos  
 Se os usuários forem carregar com frequência itens de relatório publicados diretamente nas bibliotecas de documentos do SharePoint, o recurso de sincronização de arquivo de servidor de relatório será benéfico. O recurso de sincronização de arquivo sincronizará o catálogo do servidor de relatório com itens nas bibliotecas de documentos mais frequentemente. Para obter mais informações, consulte [Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cmdlets do PowerShell para o Reporting Services no modo do SharePoint](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Recursos com suporte nas edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473)   
 [Serviço do Reporting Services do SharePoint e aplicativos de serviço](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  