---
title: Atualizar PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
author: Minewiskan
ms.author: owend
ms.openlocfilehash: bebcfed02aa30ffc686b2a74807b6a4cc3955c90
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931977"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>Atualizar o PowerPivot para SharePoint
  Este tópico resume as etapas necessárias para atualizar uma implantação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para o [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]. As etapas específicas dependem da versão do SharePoint que seu ambiente estiver executando e inclui o suplemento PowerPivot para SharePoint (**spPowerPivot.msi**).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 Para obter notas de versão, consulte as [Notas de versão do SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  

  
## <a name="background"></a>Segundo plano  
  
-   Se estiver atualizando um farm com vários servidores do SharePoint 2010 que tenha duas ou mais instâncias do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , será necessário atualizar totalmente cada servidor **antes** de seguir para o próximo servidor. Uma atualização total inclui a execução da Instalação do SQL Server para atualizar arquivos de programas do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , seguida pelas ações de atualização do SharePoint que configuram os serviços atualizados. A disponibilidade do servidor ficará limitada até você executar as ações de atualização na Ferramenta de Configuração apropriada do PowerPivot ou do Windows PowerShell.  
  
-   Todas as instâncias do Analysis Services e do Serviço de Sistema PowerPivot em um farm do SharePoint 2010 devem ser da mesma versão. Para obter informações sobre como verificar a versão, consulte a seção [Verificar as versões de componentes e serviços do PowerPivot](#bkmk_verify_versions) neste tópico.  
  
-   As ferramentas de configuração do PowerPivot são um dos recursos compartilhados do SQL Server e todos os recursos compartilhados são atualizados ao mesmo tempo. Se, durante um processo de atualização, você selecionar outras instâncias do SQL Server ou recursos que exigem uma atualização de recurso compartilhado; em seguida, a ferramenta de configuração do PowerPivot também será atualizada. Você poderá ter problemas se a ferramenta de configuração do PowerPivot estiver atualizada, mas sua instância do PowerPivot não. Para obter mais informações sobre SQL Server recursos compartilhados, consulte [atualizar para o SQL Server 2014 usando o assistente de instalação &#40;&#41;de instalação ](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   O suplemento PowerPivot para SharePoint (**spPowerPivot.msi**) é instalada lado a lado com versões anteriores. Por exemplo, o suplemento [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é instalado na pasta `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`.  
  

  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> Pré-requisitos  
 **Permissões**  
  
-   Você deve ser um administrador do farm para atualizar a instalação do PowerPivot para SharePoint. Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
-   É necessário ter permissões de **db_owner** no banco de dados de configuração do farm.  
  
 **SQL Server:**  
  
-   Se a instalação existente do PowerPivot for [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Service Pack 2 (SP2) será necessário para uma atualização para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .  
  
-   Se a instalação existente do PowerPivot for [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (SP1) será necessário para uma atualização para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .  
  
 **SharePoint 2010:**  
  
-   Se a instalação existente estiver executando o SharePoint 2010, instale o SharePoint 2010 Service Pack 2 antes de atualizar para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Para obter mais informações, consulte [Service Pack 2 para Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672). Use o comando do PowerShell `(Get-SPfarm).BuildVersion.ToString()` para verificar a versão. Para fazer referência à versão de compilação até a data de lançamento, consulte [Números de compilação do SharePoint 2010](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224).  
  
 
  
##  <a name="upgrade-an-existing-sharepoint-2013-farm"></a><a name="bkmk_uprgade_sharepoint2013"></a> Atualizar um farm existente do SharePoint 2013  
 Para atualizar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] implantado no SharePoint 2013, faça o seguinte:  
  
 ![atualização do PowerPivot para SharePoint 2013](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "atualização do PowerPivot para SharePoint 2013")  
  
1.  Execute a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em servidores de back-end que executam o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint. Se o servidor hospedar várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atualize pelo menos a instância do **POWERPIVOT** . A lista a seguir é um resumo das etapas do assistente de instalação relacionadas à atualização do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
    1.  No assistente de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Instalação**.  
  
    2.  Clique em **Atualizar do SQL Server.....**.  
  
    3.  Na página **Selecionar Instância** , selecione o nome da instância **POWERPIVOT** e, em seguida, clique em **Avançar**.  
  
    4.  Para obter mais informações, consulte [atualizar para SQL Server 2014 usando o assistente de instalação &#40;instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
2.  Reinicie o servidor.  
  
3.  Execute o suplemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint (**spPowerPivot.msi**) em cada servidor no farm do SharePoint 2013 para instalar os provedores de dados. A exceção são os servidores em que você executou o assistente de instalação do SQL Server, que também atualiza os provedores de dados. Para obter mais informações, consulte [instalar ou desinstalar o suplemento de PowerPivot para SharePoint &#40;&#41;do SharePoint 2013 ](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  
  
4.  **Execute a ferramenta de configuração PowerPivot para SharePoint 2013** em um dos servidores de aplicativos do SharePoint para configurar o farm do SharePoint com os arquivos atualizados da solução que o suplemento instalou. Você não pode usar a Administração Central do SharePoint para essa etapa. Para saber mais, consulte o seguinte:  
  
    1.  Na página inicial do Windows, digite **PowerPivot** e, nos resultados da pesquisa de Aplicativos, clique em **Configuração do PowerPivot para SharePoint 2013**. Observe que a pesquisa pode retornar ambas as versões da ferramenta de configuração.  
  
         ![duas ferramentas de configuração do PowerPivot](../../analysis-services/media/as-powerpivot-configtools-bothicons.gif "duas ferramentas de configuração do PowerPivot")  
  
         Ou  
  
         No menu **Iniciar** , aponte para **Todos os Programas**, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], em **Ferramentas de Configuração**e em **Ferramenta de Configuração do PowerPivot para SharePoint 2013**. Observe que essa ferramenta será listada apenas quando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] estiver instalado no servidor local.  
  
    2.  Na inicialização, a ferramenta de configuração verifica o status da atualização da solução de farm do PowerPivot e das soluções de aplicativo Web PowerPivot. Se as versões mais antigas dessas soluções forem detectadas, você verá a mensagem "foram**detectadas versões mais recentes dos arquivos da solução PowerPivot. Selecione a opção de atualização para atualizar o farm**. " Clique em **OK** para fechar a mensagem de validação do sistema.  
  
    3.  Clique em **Atualizar Recursos, Serviços, Aplicativos e Soluções**e clique em **OK**.  
  
    4.  Reveja as ações na lista de tarefas do painel esquerdo e exclua as que você não deseja que a ferramenta execute. Por padrão, todas as ações são incluídas. Para remover uma ação, selecione-a na lista de tarefas à esquerda e, na página **Parameters** , desmarque a caixa de seleção **Inclua esta ação na lista de tarefas** na página Parâmetros.  
  
    5.  Opcionalmente, revise as informações detalhadas na guia **Script** ou na guia **Saída** .  
  
         A guia Saída é um resumo das ações que serão executadas pela ferramenta. Essas informações são salvas nos arquivos de log em `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`.  
  
         A guia Script mostra os cmdlets PowerShell ou referencia os arquivos de script PowerShell que serão executados pela ferramenta.  
  
    6.  Clique em **Validar** para verificar se cada ação é válida. Se **Validar** não estiver disponível, isso indicará que todas as ações são válidas para o sistema. Se **Validar** estiver disponível, talvez você tenha modificado o valor de entrada (por exemplo, o nome do aplicativo de serviço do Excel) ou a ferramenta tenha determinado que uma ação específica não pode ser executada. Se uma ação não puder ser executada, você deverá excluí-la ou corrigir as condições subjacentes que fazem com que a ação seja sinalizada como inválida.  
  
        > [!IMPORTANT]  
        >  A primeira ação, **Atualizar Solução de Farm**, sempre deve ser processada primeiro. Ela registra os cmdlets PowerShell que são usados para configurar o servidor. Se você obtiver um erro nessa ação, não continue. Em vez disso, use as informações fornecidas pelo erro para diagnosticar e resolver o problema antes de processar ações adicionais na lista de tarefas.  
  
    7.  Clique em **Executar** para executar todas as ações válidas para esta tarefa. **Executar** estará disponível apenas depois que a verificação da validação tiver sido aprovada. Quando você clica em **executar**, o seguinte aviso é exibido, lembrando que as ações são processadas no modo de lote: "**todos os parâmetros de configuração sinalizados como válidos na ferramenta serão aplicados ao farm do SharePoint. Deseja continuar?**".  
  
    8.  Clique em **Sim** para continuar.  
  
    9. A atualização de soluções e recursos no farm pode levar vários minutos para ser concluída. Durante esse tempo, as solicitações de conexão para dados PowerPivot **falharão** com erros semelhantes a "**não é possível atualizar os dados**" ou "**ocorreu um erro ao tentar executar a ação solicitada. Tente novamente**. " Depois que a atualização for concluída, o servidor ficará disponível e esses erros não ocorrerão mais.  
  
     Para saber mais, consulte o seguinte:  
  
    -   [PowerPivot Configuration Tools](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools)  
  
    -   [Configurar ou reparar a ferramenta de configuração do PowerPivot para SharePoint 2013 &#40;o PowerPivot&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013)  
  
    -   [Configuração do PowerPivot usando o Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)  
  
    -   [Referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  Verifique se a atualização teve êxito executando as etapas pós-atualização e verificando a versão dos servidores PowerPivot no farm. Para obter mais informações, consulte [Post-upgrade verification tasks](#verify) neste tópico e a seção a seguir.  
  
 
  
##  <a name="upgrade-an-existing-sharepoint-2010-farm"></a><a name="bkmk_uprgade_sharepoint2010"></a>Atualizar um farm existente do SharePoint 2010  
 Para atualizar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] implantado no SharePoint 2010, faça o seguinte:  
  
 ![atualização do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "atualização do PowerPivot para SharePoint 2010")  
  
1.  Baixe o [Service Pack 2 para Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672) e aplique-o em todos os servidores no farm. Verifique se a instalação do SharePoint SP2 foi bem-sucedida. Na Administração Central, na página Atualização e Migração, abra a página Verificar o status de instalação do produto e dos patches para exibir mensagens de status relacionadas ao SP2.  
  
2.  Verifique se o serviço Administração do Windows do SharePoint 2010 está em execução.  
  
    ```powershell
    Get-Service | Where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  Verifique se os serviços do **SharePoint** , **SQL Server Analysis Services** e **Serviço de Sistema SQL Server PowerPivot** estão iniciados na Administração Central do SharePoint ou use o seguinte comando do PowerShell.  
  
    ```powershell
    Get-SPServiceInstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  Verifique se o serviço do **Windows****SQL Server Analysis Services (PowerPivot)** está em execução.  
  
    ```powershell
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **Executar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Configuração** no primeiro servidor de aplicativos do SharePoint que executa o serviço do Windows **SQL Server Analysis Services (PowerPivot)** para atualizar a instância do PowerPivot. Na página de Instalação do Assistente de Configuração do SQL Server, escolha a opção de atualização. Para obter mais informações, consulte [atualizar para SQL Server 2014 usando o assistente de instalação &#40;&#41;de ](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)instalação.  
  
6.  **Reinicie o servidor** antes de executar a ferramenta de configuração. Essa etapa garante que todas as atualizações ou pré-requisitos instalados pela Instalação do SQL Server sejam configurados no sistema.  
  
7.  **Execute a ferramenta de configuração do PowerPivot** no primeiro servidor de aplicativos do SharePoint que executa o serviço SQL Server Analysis Services (PowerPivot) para atualizar as soluções e os serviços Web no SharePoint. Você não pode usar a Administração Central para essa etapa.  
  
    1.  No menu **Iniciar** , aponte para **Todos os Programas**, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], em **Ferramentas de Configuração**e em **Ferramenta de Configuração do PowerPivot**. Observe que essa ferramenta será listada apenas quando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] estiver instalado no servidor local.  
  
    2.  Na inicialização, a ferramenta de configuração verifica o status da atualização da solução de farm do PowerPivot e das soluções de aplicativo Web PowerPivot. Se as versões mais antigas dessas soluções forem detectadas, você verá a mensagem "foram detectadas versões mais recentes dos arquivos da solução PowerPivot. Selecione a opção de atualização para atualizar o farm.” Clique em **OK** para fechar a mensagem.  
  
    3.  Clique em **Atualizar Recursos, Serviços, Aplicativos e Soluções**e clique em **OK** para continuar.  
  
    4.  O seguinte aviso é exibido: "pastas de trabalho no painel de gerenciamento PowerPivot estão prestes a ser atualizadas para a versão mais recente. Quaisquer atualizações feitas nas pastas de trabalho existentes serão perdidas. Deseja continuar?"  
  
         Esse aviso refere-se às pastas de trabalho no Painel de Gerenciamento PowerPivot que relatam a atividade de atualização de dados. Se você tiver personalizado essas pastas de trabalho, quaisquer alterações feitas nessas pastas de trabalho serão perdidas quando os arquivos existentes forem substituídos por versões mais recentes.  
  
         Clique em **Sim** para substituir as pastas de trabalho por versões mais recentes. Caso contrário, clique em **Não** para retornar à home page. Salve as pastas de trabalho em um local diferente para que você tenha uma cópia e retorne a essa etapa quando estiver pronto para continuar.  
  
         Para obter mais informações sobre a personalização de pastas de trabalho usadas no painel, consulte o artigo sobre [personalização do Painel de Gerenciamento PowerPivot](https://go.microsoft.com/fwlink/?linkID=229639).  
  
    5.  Reveja as ações na lista de tarefas e exclua as que você não deseja que a ferramenta execute. Por padrão, todas as ações são incluídas. Para remover uma ação, selecione-a na lista de tarefas e desmarque a caixa de seleção **Inclua esta ação na lista de tarefas** na página Parâmetros.  
  
    6.  Opcionalmente, revise as informações detalhadas na guia **Saída** ou na guia **Script** .  
  
         A guia Saída é um resumo das ações que serão executadas pela ferramenta. Essas informações são salvas nos arquivos de log em `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`.  
  
         A guia Script mostra os cmdlets PowerShell ou referencia os arquivos de script PowerShell que serão executados pela ferramenta.  
  
    7.  Clique em **Validar** para verificar se cada ação é válida. Se **Validar** não estiver disponível, isso indicará que todas as ações são válidas para o sistema. Se **Validar** estiver disponível, talvez você tenha modificado o valor de entrada (por exemplo, o nome do aplicativo de serviço do Excel) ou a ferramenta tenha determinado que uma ação específica não pode ser executada. Se uma ação não puder ser executada, você deverá excluí-la ou corrigir as condições subjacentes que fazem com que a ação seja sinalizada como inválida.  
  
        > [!IMPORTANT]  
        >  A primeira ação, **Atualizar Solução de Farm**, sempre deve ser processada primeiro. Ela registra os cmdlets PowerShell que são usados para configurar o servidor. Se você obtiver um erro nessa ação, não continue. Em vez disso, use as informações fornecidas pelo erro para diagnosticar e resolver o problema antes de processar ações adicionais na lista de tarefas.  
  
    8.  Clique em **Executar** para executar todas as ações válidas para esta tarefa. **Executar** estará disponível apenas depois que a verificação da validação tiver sido aprovada. Quando você clica em **executar**, o seguinte aviso é exibido, lembrando que as ações são processadas no modo de lote: "todos os parâmetros de configuração sinalizados como válidos na ferramenta serão aplicados ao farm do SharePoint. Deseja continuar?"  
  
    9. Clique em **Sim** para continuar.  
  
    10. A atualização de soluções e recursos no farm pode levar vários minutos para ser concluída. Durante esse tempo, as solicitações de conexão para dados PowerPivot falharão com erros como "não foi possível atualizar os dados" ou "ocorreu um erro ao tentar executar a ação solicitada. Tente novamente.” Depois que a atualização for concluída, o servidor ficará disponível e esses erros não ocorrerão mais.  
  
8.  **Repita o processo** para cada serviço de SQL Server Analysis Services (PowerPivot) no farm: 1) Execute SQL Server Setup 2) execute a ferramenta de configuração do PowerPivot.  
  
9. Verifique se a atualização teve êxito executando as etapas pós-atualização e verificando a versão dos servidores PowerPivot no farm. Para obter mais informações, consulte [Post-upgrade verification tasks](#verify) neste tópico e a seção a seguir.  
  
10. **Solucionando erros**  
  
     Você pode exibir informações de erro no painel Parâmetros de cada ação.  
  
     Para problemas relacionados à implantação ou retração da solução, verifique se o serviço Administrador do SharePoint 2010 está iniciado. Esse serviço executa os trabalhos de timer que disparam alterações na configuração em um farm. Se o serviço não estiver em execução, a implantação ou a retração da solução apresentará falha. Erros persistentes indicam que um trabalho de implantação ou retração existente já está na fila e bloqueando ação adicional da ferramenta de configuração.  
  
    1.  Inicie o Shell de Gerenciamento do SharePoint 2010 como administrador e execute o comando a seguir para exibir os trabalhos na fila:  
  
        ```cmd
        stsadm -o enumdeployments  
        ```  
  
    2.  Reveja as implantações existentes para obter as seguintes informações: **Tipo** é Retração ou Implantação, **Arquivo** é powerpivotwebapp.wsp ou powerpivotfarm.wsp.  
  
    3.  Para implantações ou retração relacionadas a soluções PowerPivot, copie o valor de GUID para **JobID** e cole-o no comando a seguir (use os comandos marcar, copiar e colar no menu Editar do Shell para copiar o GUID):  
  
        ```cmd
        stsadm -o canceldeployment -id "<GUID>"  
        ```  
  
    4.  Tente a tarefa novamente na ferramenta de configuração clicando em **Validar** e, em seguida, em **Executar**.  
  
     Para todos os outros erros, verifique os logs ULS. Para obter mais informações, consulte [configurar e exibir arquivos de log do SharePoint e log de diagnóstico &#40;PowerPivot para SharePoint&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging).  
  

  
##  <a name="workbooks"></a><a name="bkmk_workbooks"></a>Pastas  
 A atualização de um servidor não necessariamente atualiza as pastas de trabalho PowerPivot executadas nele, mas as pastas de trabalho mais antigas criadas na versão anterior do PowerPivot para Excel continuarão funcionando como antes, usando os recursos disponíveis nessa versão. As pastas de trabalho permanecem funcionais porque um servidor atualizado tem a versão do provedor OLE DB do Analysis Services que fez parte da instalação anterior.  
  
  
  
##  <a name="data-refresh"></a><a name="bkmk_datarefresh"></a>Atualização de dados  
 A atualização afetará as operações de atualização de dados. A atualização de dados agendada no servidor está disponível somente para pastas de trabalho que correspondem à versão de servidor. Se você estiver hospedando pastas de trabalho da versão anterior, a atualização de dados não poderá funcionar mais para essas pastas de trabalho. Para reabilitar a atualização de dados, você deverá atualizar as pastas de trabalho. Você pode atualizar cada pasta de trabalho manualmente no PowerPivot para Excel, ou habilitar o recurso de atualização automática de dados no SharePoint 2010. A atualização automática atualizará uma pasta de trabalho para a versão atual antes de executar a atualização de dados, permitindo que as operações de atualização de dados sejam feitas.  
  

  
##  <a name="verify-the-versions-of-powerpivot-components-and-services"></a><a name="bkmk_verify_versions"></a>Verificar as versões dos componentes e serviços do PowerPivot  
 Todas as instâncias do Serviço do Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e do Analysis Services devem ser da mesma versão. Para verificar se todos os componentes de servidor têm a mesma versão, verifique informações do:  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>Verificar a versão de soluções do PowerPivot e o Serviço de Sistema PowerPivot  
 Execute o seguinte comando do PowerShell:  
  
```powershell
Get-PowerPivotSystemService  
```  
  
 Verifique a **CurrentSolutionVersion**. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]é a versão 12,0. \<major build> .\<minor build>  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>Verificar a versão do serviço Windows do Analysis Services  
 Se você só atualizou alguns dos servidores do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] em um farm do SharePoint 2010, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em servidores não atualizados será mais antiga do que a versão esperada no farm. Você precisará atualizar todos os seus servidores para a mesma versão para que eles sejam utilizáveis. Use um dos métodos a seguir para verificar a versão do serviço Windows do SQL Server Analysis Services (PowerPivot) em cada computador.  
  
 **Explorador de Arquivos do Windows**:  
  
1.  Navegue até a pasta **Bin** para a instância do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Por exemplo, `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`.  
  
2.  Clique com o botão direito do mouse em `msmdsrv.exe`e selecione **Propriedades**.  
  
3.  Clique em **Detalhes**.  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]a versão do arquivo deve ser 12, 0.. \<major build> \<minor build> .  
  
5.  Verifique se esse número é idêntico à versão da solução do PowerPivot e do serviço do sistema.  
  
 **Informações do início do serviço:**  
  
 Quando o serviço PowerPivot inicia, ele grava as informações de versão no log de eventos do Windows.  
  
1.  Execute o Windows `eventvwr`  
  
2.  Crie um filtro para o `MSOLAP$POWERPIVOT`de origem.  
  
3.  Procure um evento de nível de informações semelhante ao seguinte  
  
     Service iniciado. Avaliação do Microsoft SQL Server Analysis Services 64 Bits (x64) RTM **12.0.2000.8**.  
  
 **Use o PowerShell para verificar a versão do arquivo.**  
  
 Você pode usar o PowerShell para verificar a versão do produto. O PowerShell é uma boa opção se você quiser gerar um script ou automatizar a verificação de versão.  
  
```powershell
(Get-ChildItem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 O comando do PowerShell acima retorna informações semelhantes a estas:  
  
 VersãodoProduto   VersãodoArquivo           NomedoArquivo  
  
 **12.0.2000.8** 2014.0120.200    C:\Arquivos de Programas\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>Verificar a versão do provedor de dados MSOLAP no SharePoint  
 Use as instruções a seguir para verificar as versões dos provedores OLE DB do Analysis Services confiáveis pelos Serviços do Excel. Você deve ser um administrador de farm ou de aplicativo de serviço para verificar as configurações do provedor de dados confiável dos Serviços do Excel.  
  
1.  Na administração central, em gerenciamento de aplicativos, clique em **gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do aplicativo de serviço dos Serviços do Excel; por exemplo **ExcelServiceApp1**.  
  
3.  Clique em **Provedores de Dados Confiáveis**. Você deverá ver o MSOLAP.5 (Provedor Microsoft OLE DB para OLAP Services 11.0). Se você tiver atualizado sua instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , também verá o MSOLAP.4 da versão anterior.  
  
4.  Para obter mais informações, consulte [Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services).  
  
 O MSOLAP.4 é descrito como o Microsoft OLE DB Provider para OLAP Services 10.0. Essa versão pode ser a versão padrão do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] que é instalada com os Serviços do Excel ou pode ser a versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] . A versão padrão que o SharePoint instala não dá suporte ao acesso a dados PowerPivot. Você deve ter a versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] versão ou posterior para se conectar a pastas de trabalho PowerPivot no SharePoint. Para verificar se você tem a versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , siga as instruções na seção anterior que explicam como verificar a versão exibindo as propriedades do arquivo.  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>Verificar a versão do provedor de dados ADOMD.NET  
 Use as instruções a seguir para verificar qual versão do ADOMD.NET está instalada. Você deve ser um administrador de farm ou de aplicativo de serviço para verificar as configurações do provedor de dados confiável dos Serviços do Excel.  
  
1.  No seu servidor de aplicativos do SharePoint, navegue até `c:\Windows\Assembly`.  
  
2.  Classifique por nome do assembly e localize **Microsoft.Analysis Services.Adomd.Client**.  
  
3.  Verifique se você tem a versão 12,0. \<build number> .  
  

##  <a name="upgrading-multiple-powerpivot-for-sharepoint-servers-in-a-sharepoint-farm"></a><a name="geminifarm"></a>Atualizando vários servidores PowerPivot para SharePoint em um farm do SharePoint  
 Em uma topologia com vários servidores que conta com mais de um servidor do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , todas as instâncias e componentes de servidor devem estar na mesma versão. O servidor que executa a versão mais recente do software define o nível para todos os servidores no farm. Se você atualizar apenas alguns servidores, os que executam versões anteriores do software ficarão indisponíveis até que sejam atualizados também.  
  
 Depois que você atualizar o primeiro servidor, servidores adicionais que ainda não foram atualizados **continuarão indisponíveis**. A disponibilidade será restaurada depois que todos os servidores forem executados no mesmo nível.  
  
 A Instalação do SQL Server atualiza os arquivos de solução do PowerPivot existentes no computador físico, mas para atualizar as soluções em uso pelo farm, você deverá utilizar a Ferramenta de Configuração do PowerPivot descrita em uma seção anterior desse tópico.  

##  <a name="applying-a-qfe-to-a-powerpivot-instance-in-the-farm"></a><a name="qfe"></a>Aplicando um QFE a uma instância do PowerPivot no farm  
 Aplicar patches em um servidor PowerPivot para SharePoint atualiza os arquivos de programas existentes com uma versão mais recente que inclui uma correção para um problema específico. Ao aplicar um QFE em uma topologia multi-servidor, não há nenhum servidor primário com que você deva começar. Você pode iniciar com qualquer servidor, contanto que aplique o mesmo QFE aos outros servidores do PowerPivot no farm.  
  
 Quando você aplicar o QFE, deverá também executar a etapa de configuração que atualiza as informações de versão do servidor no banco de dados de configuração do farm. A versão do servidor que recebeu o patch passa a ser a nova versão esperada para o farm. Até que o QFE seja aplicado e configurado em todas as máquinas, as instâncias do PowerPivot para SharePoint que não têm o QFE não estarão disponíveis para tratar solicitações de dados PowerPivot.  
  
 Para assegurar que o QFE seja aplicado e configurado corretamente, siga estas instruções:  
  
1.  Instale o patch, seguindo as instruções apresentadas com o QFE.  
  
2.  Iniciar a Ferramenta de Configuração do PowerPivot.  
  
3.  Clique em **Atualizar Recursos, Serviços, Aplicativos e Soluções**e clique em **OK**.  
  
4.  Revise as ações que estão incluídas na tarefa de atualização e clique em **Validar**.  
  
5.  Clique em **Executar** para aplicar as ações.  
  
6.  Repita para instâncias adicionais do PowerPivot para SharePoint no farm.  
  
    > [!IMPORTANT]  
    >  Em uma implantação multisservidor, aplique o patch e configure cada instância antes de ir para o próximo computador. A Ferramenta de Configuração do PowerPivot deve concluir a tarefa de atualização para a instância atual antes de ir para a próxima instância.  
  
 Para verificar as informações de versão dos serviços no farm, use a página **Verificar o status de instalação do produto e dos patches** na seção Gerenciamento de Atualizações e Patches na Administração Central.  
  
##  <a name="post-upgrade-verification-tasks"></a><a name="verify"></a> Tarefas de verificação após a atualização  
 Quando a atualização for concluída, use as etapas a seguir para verificar se o servidor está funcionando.  
  
|Tarefa|Link|  
|----------|----------|  
|Verifique se o serviço está em execução em todos os computadores que executam o PowerPivot para SharePoint.|[Iniciar ou parar um PowerPivot para SharePoint Server](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server)|  
|Verifique a ativação de recurso no nível de coleção de sites.|[Ativar a integração de recursos do PowerPivot para coleções de sites na Administração Central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)|  
|Verifique se pastas de trabalho PowerPivot individuais estão sendo carregadas corretamente abrindo uma pasta de trabalho e clicando em filtros e segmentações de dados para iniciar uma consulta.|Verifique se há arquivos armazenados em cache na unidade de disco rígido. Um arquivo armazenado em cache confirma se o arquivo de dados foi carregado nesse servidor físico. Verifique se há arquivos armazenados em cache na pasta C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup.|  
|Teste a atualização de dados em algumas pastas de trabalho que estão configuradas para atualização de dados.|O modo mais fácil de atualizar dados de teste é modificar uma agenda de atualização de dados, marcando a caixa de seleção **Também atualizar o mais rápido possível** para que a atualização de dados seja executada imediatamente. Esta etapa determinará se a atualização de dados teve êxito na pasta de trabalho atual. Repita estas etapas para outras pastas de trabalho frequentemente usadas para verificar se a atualização de dados funciona. Para obter mais informações sobre agendamento de atualização de dados, consulte [agendar uma atualização de dados &#40;PowerPivot para SharePoint&#41;](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md).|  
|Com o tempo, monitore os relatórios atualizados de dados no Painel de Gerenciamento do PowerPivot para confirmar se não há erros de atualização de dados.|[Painel de Gerenciamento PowerPivot e dados de uso](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)|  
  
 Para obter mais informações sobre como definir as configurações e os recursos do PowerPivot, consulte [Administração e configuração do servidor PowerPivot na administração central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
 Para obter as instruções passo a passo que orientam você em todas as tarefas de configuração pós-instalação, consulte [configuração inicial &#40;PowerPivot para SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  

## <a name="see-also"></a>Consulte Também  
 [Recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
