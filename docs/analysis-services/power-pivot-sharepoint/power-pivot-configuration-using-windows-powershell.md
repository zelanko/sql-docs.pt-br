---
title: "Power Pivot configuração usando o Windows PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e25460598e99163c4866b14741bf020208de902b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-configuration-using-windows-powershell"></a>Configuração do Power Pivot usando o Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui cmdlets do Windows PowerShell que você pode usar para configurar uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. A configuração completa de uma instalação com o PowerShell requer o uso de cmdlets do SharePoint e do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para os cmdlets do SharePoint. A maior parte da configuração pode ser concluída usando uma das ferramentas do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações sobre as ferramentas, consulte [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  Para um farm do SharePoint 2010, o SharePoint 2010 SP1 deve ser instalado antes da configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou de um farm do SharePoint que usa um servidor do banco de dados do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . Se você ainda não instalou o service pack; instale-o antes de começar a configurar o servidor.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-powershell"></a>Benefícios da Configuração do Power Pivot para SharePoint Usando o PowerShell  
 É possível criar arquivos de script do Windows PowerShell (.ps1) para automatizar tarefas de configuração. Essa abordagem será recomendada se você precisar de instalação e etapas de configuração controladas por script que possa ser executado em qualquer servidor. Você pode precisar desse script como parte de um plano de recuperação de desastre para reconstruir um servidor no caso de um problema de hardware.  
  
## <a name="view-a-list-of-the-power-pivot-cmdlets-on-a-server"></a>Exibir uma lista de Cmdlets do Power Pivot em um Servidor  
 Para ver o conteúdo e exemplos de cmdlets do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , consulte [Referência do PowerShell para PowerPivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).  
  
 Para usar o PowerShell para exibir uma lista de cmdlets do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
1.  Abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador** .  
  
2.  Insira o seguinte comando:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Você deve ver uma lista de cmdlets que incluem o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no nome do cmdlet. Por exemplo, `Get-PowerPivotServiceApplication`. O número de cmdlets disponíveis depende da versão do Analysis Services que você está usando.  
  
    -   10 cmdlets com o servidor SQL Server 2012 SP1 Analysis Services configurados no modo do SharePoint e com o SharePoint 2013. A versão 2012 SP1 utiliza uma nova arquitetura que permite ao Analysis Server ser executado fora do farm do SharePoint e exige menos cmdlets do Windows PowerShell de gerenciamento.  
  
    -   17 cmdlets com o servidor SQL Server 2012 Analysis Services configurados no modo do SharePoint e com o SharePoint 2010.  
  
     Se nenhum comando for retornado na lista ou se você vir uma mensagem de erro semelhante a "`get-help could not find *powerpivot* in a help file in this session.`", consulte a próxima seção neste tópico para obter instruções sobre como habilitar os cmdlets do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no servidor.  
  
     Todos os cmdlets têm ajuda online. O exemplo a seguir mostra como exibir a ajuda online para o cmdlet **New-PowerPivotServiceApplication** :  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     Como alternativa, para exibir apenas os exemplos, use a sintaxe a seguir:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-power-pivot-cmdlets-on-a-server"></a>Habilitar os Cmdlets do Power Pivot em um Servidor  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] estão disponíveis depois que você instala o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint e implanta a solução de farm. As soluções são implantadas quando você executa a ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Siga estas etapas para habilitar o uso de cmdlets:  
  
1.  Abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador** .  
  
2.  Execute o primeiro cmdlet:  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.  
  
3.  Execute o segundo cmdlet para implantar a solução:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
4.  Feche a janela. Abra-a novamente usando a opção **Executar como Administrador** .  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
 [Referência do PowerShell para PowerPivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
  
