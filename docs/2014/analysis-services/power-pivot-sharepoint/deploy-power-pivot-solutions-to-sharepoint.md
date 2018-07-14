---
title: Implantar soluções do PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f202a2b7-34e0-43aa-90d5-c9a085a37c32
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce0863ef023f96580eb809b6562cfc54b0de5b60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243656"
---
# <a name="deploy-powerpivot-solutions-to-sharepoint"></a>Implantar soluções PowerPivot para SharePoint
  Use as instruções a seguir para implantar manualmente dois pacotes de solução que adicionam recursos do PowerPivot a um ambiente do SharePoint Server 2010. Implantar as soluções é uma etapa necessária para configurar o PowerPivot para SharePoint em um servidor do SharePoint 2010. Para exibir a lista completa de etapas necessárias, consulte [administração de servidor do PowerPivot e a configuração na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 Como alternativa, você pode usar a Ferramenta de Configuração do PowerPivot para implantar as soluções. Usar a ferramenta de configuração é mais fácil e mais eficiente para uma única instalação de servidor, mas você pode querer usar a Administração Central e o PowerShell se preferir usar uma ferramenta familiar ou se estiver configurando vários recursos ao mesmo tempo. Para obter mais informações sobre como usar a ferramenta de configuração, consulte [PowerPivot Configuration Tools](power-pivot-configuration-tools.md).  
  
 Antes de implantar as soluções, você deverá primeiro instalar o PowerPivot para SharePoint usando a mídia de instalação do SQL Server 2012. A instalação do SQL Server instala os pacotes de solução que você está prestes a implantar.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisito: verificar se o aplicativo Web usa a autenticação de modo clássico](#bkmk_classic)  
  
 [Etapa 1: implantar a solução de farm](#bkmk_farm)  
  
 [Etapa 2: Implantar a solução de aplicativo Web do PowerPivot em Administração Central](#deployCA)  
  
 [Etapa 3: Implantar a solução de aplicativo Web do PowerPivot em outros aplicativos Web](#deployUI)  
  
 [Reimplantar ou cancelar a solução](#retract)  
  
 [Sobre as soluções do PowerPivot](#intro)  
  
##  <a name="bkmk_classic"></a> Pré-requisito: verificar se o aplicativo Web usa a autenticação de modo clássico  
 O PowerPivot para SharePoint tem suporte apenas para aplicativos Web que utilizam a autenticação de modo clássico do Windows. Para verificar se o aplicativo utiliza o modo clássico, execute o seguinte cmdlet do PowerShell a partir de **Shell de gerenciamento do SharePoint 2010**, substituindo `http://<top-level site name>` com o nome do seu site do SharePoint:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 O valor retornado deve ser **false**. Se ele estiver **verdadeira**, você não pode acessar dados do PowerPivot com este aplicativo web.  
  
##  <a name="bkmk_farm"></a> Etapa 1: implantar a solução de farm  
 Esta seção mostra como implantar soluções usando o PowerShell, mas você também pode usar a Ferramenta de Configuração do PowerPivot para concluir esta tarefa. Para obter mais informações, consulte [configurar ou reparar o PowerPivot para SharePoint 2010 &#40;ferramenta de configuração do PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md).  
  
 Esta tarefa somente precisa ser executada uma vez, depois de instalar o PowerPivot para SharePoint.  
  
1.  Em um servidor que tem uma instalação do PowerPivot para SharePoint, abra um Shell de gerenciamento do SharePoint 2010 usando o **executar como administrador** opção.  
  
2.  Execute o cmdlet a seguir para adicionar a solução do farm.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.  
  
3.  Execute o cmdlet seguinte para implantar a solução do farm:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> Etapa 2: Implantar a solução de aplicativo Web do PowerPivot em Administração Central  
 Depois de implantar a solução do farm, você deverá implantar a solução de aplicativo Web na Administração Central. Essa etapa adiciona o Painel de Gerenciamento do PowerPivot à Administração Central.  
  
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
  
##  <a name="deployUI"></a> Etapa 3: Implantar a solução de aplicativo Web do PowerPivot em outros aplicativos Web  
 Na tarefa anterior, você implantou o Powerpivotwebapp.wsp na Administração Central. Nesta seção, você implanta o powerpivotwebapp.wsp em cada aplicativo Web existente que dá suporte a acesso a dados PowerPivot. Se você adicionar mais aplicativos Web posteriormente, repita esta etapa para esses aplicativos.  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp.wsp**.  
  
3.  Clique em **Implantar Solução**.  
  
4.  Na **implantar em?**, selecione o aplicativo web do SharePoint para o qual você deseja adicionar suporte ao recurso PowerPivot.  
  
5.  Clique em **OK**.  
  
6.  Repita para outros aplicativos Web do SharePoint que também oferecerão suporte ao acesso a dados PowerPivot.  
  
##  <a name="retract"></a> Reimplantar ou cancelar a solução  
 Embora a Administração Central do SharePoint forneça o cancelamento da solução, você não precisa cancelar o arquivo powerpivotwebapp.wsp, a menos que esteja solucionando problemas sistematicamente de uma instalação ou um problema de implantação do patch.  
  
1.  Na Administração Central do SharePoint 2010, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp.wsp**.  
  
3.  Clique em **Cancelar Solução**.  
  
 Se você encontrar problemas de implantação de servidor rastreados para solução de farm, poderá reimplantá-lo executando o **reparo** opção na ferramenta de configuração do PowerPivot. As operações de reparo pela ferramenta são preferíveis porque exigem menos etapas de sua parte. Para obter mais informações, consulte [configurar ou reparar o PowerPivot para SharePoint 2010 &#40;ferramenta de configuração do PowerPivot&#41;](../configure-repair-powerpivot-sharepoint-2010.md).  
  
 Se você ainda desejar reimplantar todas as soluções, siga esta ordem:  
  
1.  Cancele a solução de aplicativo Web PowerPivot de todos os aplicativos Web do SharePoint que o utilizam.  
  
2.  Cancele a solução de farm PowerPivot.  
  
3.  Reimplante a solução de farm PowerPivot.  
  
4.  Reimplante a solução de aplicativo Web PowerPivot para todos os aplicativos Web do SharePoint.  
  
##  <a name="intro"></a> Sobre as soluções do PowerPivot  
 O PowerPivot para SharePoint usa dois pacotes de soluções para implantar páginas de aplicativos e arquivos de programas no farm e em aplicativos Web individuais.  
  
-   A solução de farm é global. É implantada uma vez e permanece disponível automaticamente para qualquer servidor novo do PowerPivot para SharePoint adicionado ao farm posteriormente.  
  
-   A solução de aplicativo Web é específica do aplicativo e deve ser implantada em cada aplicativo Web no farm, inclusive o aplicativo Web Administração Central.  
  
 Cada solução é implantada de maneira diferente.  A solução do farm é implantada uma vez, depois que a primeira instância do PowerPivot para SharePoint é instalada. Para implantar a solução do farm, use a Ferramenta de Configuração do PowerPivot ou os cmdlets do PowerShell.  
  
 A solução do aplicativo Web é implantada inicialmente na Administração Central, seguida por implantações subsequentes da solução em qualquer aplicativo Web adicional que dará suporte a solicitações para dados PowerPivot. Para implantar a solução de aplicativo Web da Administração Central, você deve usar a Ferramenta de Configuração do PowerPivot ou cmdlet do PowerShell. Para todos os outros aplicativos Web, você pode implantar a solução de aplicativo Web manualmente usando a Administração Central ou PowerShell.  
  
|Solução|Description|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Adiciona o Microsoft.AnalysisServices.SharePoint.Integration.dll ao assembly global.<br /><br /> Adiciona o Microsoft.AnalysisServices.ChannelTransport.dll ao assembly global.<br /><br /> Instala recursos e arquivos de recurso e registra tipos de conteúdo.<br /><br /> Adiciona modelos de biblioteca para bibliotecas da Galeria PowerPivot e do Feed de Dados.<br /><br /> Adiciona páginas de aplicativos para configuração de aplicativos de serviço, Painel de Gerenciamento PowerPivot, atualização de dados e Galeria PowerPivot.|  
|Powerpivotwebapp.wsp|Adiciona arquivos de recursos Microsoft.AnalysisServices.SharePoint.Integration.dll à pasta de extensões no servidor Web front-end.<br /><br /> Adiciona serviço Web do PowerPivot ao front-end Web.<br /><br /> Adiciona geração de imagens em miniatura para Galeria PowerPivot.|  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar o PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Administração de servidor do PowerPivot e a configuração na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configuração do PowerPivot usando o Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
  
