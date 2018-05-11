---
title: Migrar o Power Pivot para SharePoint 2013 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7ae2eacd512e2c268d9102ac874b1edc50408c9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="migrate-power-pivot-to-sharepoint-2013"></a>Migrar o Power Pivot para o SharePoint 2013
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  
  
 O SharePoint 2013 não oferece suporte a atualização in-loco. De qualquer modo, o procedimento de **atualização da anexação do banco de dados tem suporte**. O comportamento é diferente de atualizar para o SharePoint 2010, onde um cliente pode escolher entre as duas abordagens básicas de atualização, atualização in-loco e atualizações de anexação do banco de dados.  
  
 Se você tiver uma instalação do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] integrada com o SharePoint 2010, não poderá atualizar o servidor do SharePoint in-loco. No entanto, você pode migrar bancos de dados de conteúdo e bancos de dados de aplicativo de serviço do farm do SharePoint 2010 para um farm do SharePoint 2013. Este tópico é uma visão geral das etapas necessárias para concluir uma atualização de anexação de banco de dados e uma migração relacionada ao [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]:  
  
### <a name="migration-overview"></a>Visão geral da migração  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|Preparar o farm do SharePoint 2013|Fazer backup, cópia e restauração de bancos de dados.|Montar bancos de dados de conteúdo|Migrar agendas do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|- Administração Central do SharePoint<br /><br /> - Windows PowerShell|- Páginas do aplicativo do SharePoint<br /><br /> - Windows PowerShell|  
  
##  <a name="bkmk_prepare_sharepoint2013"></a>Preparar o Farm do SharePoint 2013  
  
  > [!TIP]  
    >  Revise o método de autenticação para os quais seus aplicativos Web existentes estão configurados. Os aplicativos Web do SharePoint 2013 assumem como padrão a autenticação baseada em declarações. Os aplicativos Web do SharePoint 2010 configurados para a autenticação de modo clássico exigem etapas adicionais para migrar bancos de dados do SharePoint 2010 para o SharePoint 2013. Se seus aplicativos Web são configurados para autenticação de modo clássica, revise a documentação do SharePoint 2013.  
  
1.  Instalar um novo farm do SharePoint Server 2013.  
  
2.  Instalar uma instância de um servidor do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo do SharePoint. Para saber mais, veja [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
3.  Executar o pacote de instalação do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 **spPowerPivot.msi** em cada farm do SharePoint Server. Para obter informações, veja [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
4.  Na Administração Central do SharePoint 2013, configure o aplicativo de serviço dos Serviços do Excel para usar o servidor do modo do SharePoint do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] criado na etapa anterior. Para obter mais informações, consulte a seção “Configure a integração básica do Analysis Services SharePoint” de [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
##  <a name="bkmk_backup_restore"></a>Fazer backup, cópia e restauração de bancos de dados  
 O processo “Atualização da anexação do banco de dados do SharePoint” é uma sequência de etapas para fazer backup, copiar e restaurar conteúdo relacionado ao [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e bancos de dados de aplicativo de serviço para o farm do SharePoint 2013.  
  
1.  **Definir banco de dados como somente leitura:** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no nome do banco de dados e clique em **Propriedades**. Na página **Opções** , defina a propriedade **Banco de Dados Somente Leitura** como **True**.  
  
2.  **Backup:** faça backup de todos os bancos de dados de conteúdo e banco de dados de aplicativo de serviço que você desejar migrar para o farm do SharePoint 2013. No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no nome do banco de dados, clique em **Tarefas**e clique em **Fazer backup**.  
  
3.  Faça cópia dos arquivo de backup de banco de dados (.bak) para o servidor de destino desejado.  
  
4.  **Restaurar:** restaure os bancos de dados para o [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]de destino. Essa etapa pode ser concluída usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
5.  **Definir banco de dados para leitura e gravação:** defina o **Banco de Dados Somente Leitura** como **False**.  
  
##  <a name="bkmk_prepare_mount_databases"></a>Preparar aplicativos Web e bancos de dados de conteúdo de montagem  
 Para obter uma explicação mais detalhada dos procedimentos a seguir, consulte [atualizar bancos de dados do SharePoint 2010 para o SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
1.  **Colocar o banco de dados offline:**  
  
     Coloque cada banco de dados de conteúdo do SharePoint 2013 offline, usando a Administração Central do SharePoint. Os bancos de dados de conteúdo são substituídos pelos bancos de dados que você copiou. Considere qual é a melhor sequência para seu ambiente. Coloque cada banco de dados offline e monte seu banco de dados de substituição correspondente antes de colocar offline o próximo banco de dados de conteúdo. Outra opção é colocar todos os bancos de dados de conteúdo offline como um grupo.  
  
    1.  Na Administração Central do SharePoint, clique em **Gerenciamento de Aplicativos**.  
  
    2.  Clique em **Gerenciar Bancos de Dados de Conteúdo**.  
  
    3.  Clique no nome do usuário do banco de dados.  
  
    4.  Em **Gerenciar Configurações de Banco de Dados de Conteúdo**, defina **Status do Banco de Dados** como **Offline**.  
  
    5.  Selecione **Remover o Banco de Dados de Conteúdo**. Observe o aviso de que os sites armazenadas no banco de dados de conteúdo não estarão mais acessíveis.  
  
-   **Montar bancos de dados de conteúdo:**  
  
     Use os cmdlets do PowerShell no Shell de Gerenciamento do SharePoint 2013 para montar o banco de dados de conteúdo migrado. O banco de dados do aplicativo de serviço não precisa ser montado, somente os bancos de dados: ![conteúdo relacionado ao PowerShell](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "conteúdo relacionado ao PowerShell")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     Para obter mais informações, consulte [anexar ou desanexar bancos de dados de conteúdo (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628582.aspx) (http://technet.microsoft.com/library/ff628582.aspx).  
  
     **Status quando a etapa está concluída:**  quando a operação de montagem estiver concluída, os usuários podem ver os arquivos que estavam no banco de dados de conteúdo antigo. Portanto os usuários podem ver e abrir as pastas de trabalho na biblioteca de documentos.  
  
    -   > [!TIP]  
        >  É possível nesse momento do processo de migração criar novas agendas para as pastas de trabalho migradas. No entanto, as agendas são criadas no novo banco de dados do aplicativo do serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , e não no banco de dados que você copiou do farm do SharePoint anterior. Portanto, ele não conterá nenhuma das agendas antigas. Depois que você concluir as seguintes etapas para usar o banco de dados antigo e migrar as agendas antigas, as novas agendas não estarão disponíveis.  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>Solucionar problemas ao tentar montar bancos de dados  
 Esta seção resume os possíveis problemas encontrados ao montar o banco de dados.  
  
1.  **Erros de autenticação:** se você encontrar erros relacionados à autenticação, revise qual modo de autenticação os aplicativos Web de origem estão usando. O erro pode ser causado por uma incompatibilidade na autenticação entre o aplicativo Web do SharePoint 2013 e o aplicativo Web do SharePoint 2010. Consulte [1) Preparar o farm do SharePoint 2013](#bkmk_prepare_sharepoint2013) para obter mais informações.  
  
2.  **PowerPivot.Files ausentes:** se você encontrar erros relacionados a DLLs ausentes do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , isso significa que o **spPowerPivot.msi** não foi instalado ou que a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] não foi usada para configurar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a>Atualizar agendas do Power Pivot  
 Esta seção descreve os detalhes e as opções para migrar agendas do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . A migração da agenda é um processo de duas etapas. Primeiro configure o aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para usar o banco de dados do aplicativo de serviço migrado. Em seguida, escolha uma destas opções para migração da agenda.  
  
 **Configure o aplicativo de serviço para usar o banco de dados do aplicativo de serviço migrado.**  
  
 Na Administração Central do SharePoint, configure o aplicativo de serviços do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para usar o banco de dados do aplicativo de serviço anterior que você copiou. O serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] atualiza o banco de dados do aplicativo de serviço para o novo esquema.  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Localize o aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , por exemplo “Aplicativo de Serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Padrão”, clique no nome do aplicativo de serviço e clique em **Propriedades** na faixa de opções do SharePoint.  
  
3.  Atualize a instância do nome do servidor de banco de dados e o nome do banco de dados. Para os nomes corretos para o banco de dados que você fez backup, copiou e restaurou. Quando você clicar em **OK**, o banco de dados do aplicativo de serviço será atualizado. Os erros estarão no log do ULS.  
  
 **Atualizar agendas do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]**  
  
 Configurar o aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para migrar agendas de atualização.  
  
-   **Opção 1 para migrar agendas: administrador de farm do SharePoint**  
  
    1.  No gerenciamento do SharePoint 2013 execute o `Set-PowerPivotServiceApplication` cmdlet com o `-StartMigratingRefreshSchedules` chave para ativar a demanda agenda migração automática sob ![conteúdo relacionado ao PowerShell](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell relacionados ao conteúdo"). O script do Windows PowerShell a seguir supõe que haja apenas um aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         Depois que o script do Windows PowerShell for executado, as agendas estarão ativas e as agendas serão executadas no próximo momento apropriado. No entanto, o status da página de atualização da agenda não está habilitado. Quando a agenda é executada pela primeira vez, ela será migrada e, na página de atualização da agenda, **Habilitado**  será verdadeiro.  
  
    2.  Se você desejar verificar o valor atual da propriedade StartMigratingRefreshSchedules, execute o seguinte script do PowerShell. O script executa um loop em todos os objetos de aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e exibe o nome e os valores de propriedades:  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **Opção 2 para migrar agendas opção: o usuário atualiza cada pasta de trabalho**  
  
    1.  Outra opção para migrar agendas é habilitar a atualização agendada para cada pasta de trabalho. Navegue até a biblioteca de documentos que contém as pastas de trabalho.  
  
    2.  Abra o menu de contexto e clique em **Gerenciar Atualização de Dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]**.  
  
    3.  Na seção **atualização da agenda** , clique em **Habilitar**.  
  
    4.  Você pode selecionar **Também atualizar o mais rápido possível**. Esta opção adiciona uma instância da atualização à fila assim que você clica em ok. A agenda de atualização normal ainda é ativada no momento apropriado.  
  
    5.  Clique em **OK**. O histórico de atualização agora está visível na página de atualização, a agenda será acionada no horário normal.  
  
 **Pastas de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] do SQL Server 2008 R2**  
  
-   Pastas de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] do SQL Server 2008 R2 não são atualizadas automaticamente quando são usadas no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. Depois de migrar um banco de dados de conteúdo que contém as pastas de trabalho do 2008 R2, você poderá usar as pastas de trabalho, mas as agendas não serão atualizadas.  
  
-   Para obter mais informações, veja [Atualizar pastas de trabalho e a atualização de dados agendada &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_additional_resources"></a> Recursos adicionais  
  
> [!NOTE]  
>  Para obter mais informações sobre a atualização da anexação do banco de dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e do SharePoint, consulte o seguinte:  
  
-   [Atualizar pastas de trabalho e a atualização de dados agendada &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
-   [Visão geral do processo de atualização para o SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688) (http://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpar preparações antes de uma atualização para o SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256689) (http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Atualizar bancos de dados do SharePoint 2010 para o SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690) (http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
  
