---
title: "Implantar soluções Power Pivot para SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f202a2b7-34e0-43aa-90d5-c9a085a37c32
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 206b31adec86e7ea2213746687d535d56ca3b617
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="deploy-power-pivot-solutions-to-sharepoint"></a>Implantar soluções Power Pivot para SharePoint
  Use as instruções a seguir para implantar manualmente dois pacotes de solução que adicionam recursos do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a um ambiente do SharePoint Server 2010. Implantar as soluções é uma etapa necessária para configurar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint em um servidor do SharePoint 2010. Para exibir a lista completa de etapas necessárias, consulte [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 Como alternativa, você pode usar a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para implantar as soluções. Usar a ferramenta de configuração é mais fácil e mais eficiente para uma única instalação de servidor, mas você pode querer usar a Administração Central e o PowerShell se preferir usar uma ferramenta familiar ou se estiver configurando vários recursos ao mesmo tempo. Para obter mais informações sobre a ferramenta de configuração, consulte [Ferramentas de Configuração do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
 Antes de implantar as soluções, você deverá primeiro instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usando a mídia de instalação do SQL Server 2012. A instalação do SQL Server instala os pacotes de solução que você está prestes a implantar.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisito: verificar se o aplicativo Web usa a autenticação de modo clássico](#bkmk_classic)  
  
 [Etapa 1: implantar a solução de farm](#bkmk_farm)  
  
 [Etapa 2: implantar a solução de aplicativo Web do Power Pivot na Administração Central](#deployCA)  
  
 [Etapa 3: implantar a solução de aplicativo Web do Power Pivot em outros aplicativos Web](#deployUI)  
  
 [Reimplantar ou cancelar a solução](#retract)  
  
 [Sobre as soluções Power Pivot](#intro)  
  
##  <a name="bkmk_classic"></a> Pré-requisito: verificar se o aplicativo Web usa a autenticação de modo clássico  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint tem suporte apenas para aplicativos Web que utilizam a autenticação de modo clássico do Windows. Para verificar se o aplicativo usa o modo clássico, execute o seguinte cmdlet do PowerShell a partir de **Shell de gerenciamento do SharePoint 2010**, substituindo **http://\<nome do site de nível superior >** com o nome do seu site do SharePoint:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 O valor retornado deve ser **false**. Se ele for **true**, você não poderá acessar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] com este aplicativo Web.  
  
##  <a name="bkmk_farm"></a> Etapa 1: implantar a solução de farm  
 Esta seção mostra como implantar soluções usando o PowerShell, mas você também pode usar a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para concluir esta tarefa. Para obter mais informações, consulte [Configurar ou reparar o PowerPivot para SharePoint 2010 (Ferramenta de Configuração do Power Pivot)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Esta tarefa precisa ser executada somente uma vez, depois de você instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
1.  Em um servidor que tem uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, abra um Shell de Gerenciamento do SharePoint 2010 usando a opção **Executar como Administrador** .  
  
2.  Execute o cmdlet a seguir para adicionar a solução do farm.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.  
  
3.  Execute o cmdlet seguinte para implantar a solução do farm:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> Etapa 2: implantar a solução de aplicativo Web do Power Pivot na Administração Central  
 Depois de implantar a solução do farm, você deverá implantar a solução de aplicativo Web na Administração Central. Essa etapa adiciona o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] à Administração Central.  
  
1.  Abra um Shell de Gerenciamento do SharePoint 2010 usando a opção **Executar como Administrador** .  
  
2.  Execute o cmdlet a seguir para criar uma referência à Administração Central:  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  Execute o cmdlet a seguir para adicionar a solução do farm.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp”  
    ```  
  
     O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.  
  
4.  Execute o cmdlet seguinte para instalar a solução de aplicativo Web na Administração Central.  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 Agora que a solução de aplicativo Web está implantada na Administração Central, você poderá usar a Administração Central para concluir todas as etapas de configuração restantes.  
  
##  <a name="deployUI"></a> Etapa 3: implantar a solução de aplicativo Web do Power Pivot em outros aplicativos Web  
 Na tarefa anterior, você implantou o Powerpivotwebapp.wsp na Administração Central. Nesta seção, você implanta o powerpivotwebapp.wsp em cada aplicativo Web existente que dá suporte a acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se você adicionar mais aplicativos Web posteriormente, repita esta etapa para esses aplicativos.  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp.wsp**.  
  
3.  Clique em **Implantar Solução**.  
  
4.  Em **Implantar em?**, selecione o aplicativo Web do SharePoint ao qual você deseja adicionar suporte ao recurso [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
5.  Clique em **OK**.  
  
6.  Repita para outros aplicativos Web do SharePoint que também oferecerão suporte ao acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
##  <a name="retract"></a> Reimplantar ou cancelar a solução  
 Embora a Administração Central do SharePoint forneça o cancelamento da solução, você não precisa cancelar o arquivo powerpivotwebapp.wsp, a menos que esteja solucionando problemas sistematicamente de uma instalação ou um problema de implantação do patch.  
  
1.  Na Administração Central do SharePoint 2010, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp.wsp**.  
  
3.  Clique em **Cancelar Solução**.  
  
 Se você encontrar problemas de implantação de servidor rastreados desde a solução de farm, poderá reimplantá-lo executando a opção **Reparar** na Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . As operações de reparo pela ferramenta são preferíveis porque exigem menos etapas de sua parte. Para obter mais informações, consulte [Configurar ou reparar o PowerPivot para SharePoint 2010 (Ferramenta de Configuração do Power Pivot)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Se você ainda desejar reimplantar todas as soluções, siga esta ordem:  
  
1.  Cancele a solução de aplicativo Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de todos os aplicativos Web do SharePoint que o utilizam.  
  
2.  Cancele a solução de farm do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Reimplante a solução de farm do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
4.  Reimplante a solução de aplicativo Web do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para todos os aplicativos Web do SharePoint.  
  
##  <a name="intro"></a> Sobre as soluções Power Pivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa dois pacotes de soluções para implantar páginas de aplicativos e arquivos de programas no farm e em aplicativos Web individuais.  
  
-   A solução de farm é global. É implantada uma vez e permanece disponível automaticamente para qualquer servidor novo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint adicionado ao farm posteriormente.  
  
-   A solução de aplicativo Web é específica do aplicativo e deve ser implantada em cada aplicativo Web no farm, inclusive o aplicativo Web Administração Central.  
  
 Cada solução é implantada de maneira diferente.  A solução do farm é implantada uma vez, depois que a primeira instância do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint é instalada. Para implantar a solução do farm, use a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou os cmdlets do PowerShell.  
  
 A solução do aplicativo Web é implantada inicialmente na Administração Central, seguida por implantações subsequentes da solução em qualquer aplicativo Web adicional que dará suporte a solicitações para dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para implantar a solução de aplicativo Web da Administração Central, você deve usar a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou o cmdlet do PowerShell. Para todos os outros aplicativos Web, você pode implantar a solução de aplicativo Web manualmente usando a Administração Central ou PowerShell.  
  
|Solução|Description|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Adiciona o Microsoft.AnalysisServices.SharePoint.Integration.dll ao assembly global.<br /><br /> Adiciona o Microsoft.AnalysisServices.ChannelTransport.dll ao assembly global.<br /><br /> Instala recursos e arquivos de recurso e registra tipos de conteúdo.<br /><br /> Adiciona modelos de biblioteca para as bibliotecas de Feeds de Dados e da Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Adiciona páginas de aplicativos para configuração de aplicativos de serviço, Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , atualização de dados e Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Powerpivotwebapp.wsp|Adiciona arquivos de recursos Microsoft.AnalysisServices.SharePoint.Integration.dll à pasta de extensões no servidor Web front-end.<br /><br /> Adiciona serviço Web do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ao front-end da Web.<br /><br /> Adiciona geração de imagens em miniatura para a Galeria do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar Power Pivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configuração do Power Pivot usando o Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
  
