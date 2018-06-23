---
title: Configuração do PowerPivot usando o Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4f4feb016768a71ca3f90a8efaf69769cd2ae59c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119212"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>Configuração do PowerPivot usando o Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui cmdlets do Windows PowerShell que você pode usar para configurar uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. A configuração completa de uma instalação com o PowerShell exige o uso de cmdlets do SharePoint e do PowerPivot para SharePoint. A maior parte da configuração pode ser concluída usando uma das ferramentas do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações sobre as ferramentas, consulte [ferramentas de configuração do PowerPivot](power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  Para um farm do SharePoint 2010, o SharePoint 2010 SP1 deve ser instalado antes da configuração do PowerPivot para SharePoint ou de um farm do SharePoint que usa um servidor de banco de dados do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Se você ainda não instalou o service pack; instale-o antes de começar a configurar o servidor.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>Benefícios da configuração do PowerPivot para SharePoint usando o PowerShell  
 É possível criar arquivos de script do Windows PowerShell (.ps1) para automatizar tarefas de configuração. Essa abordagem será recomendada se você precisar de instalação e etapas de configuração controladas por script que possa ser executado em qualquer servidor. Você pode precisar desse script como parte de um plano de recuperação de desastre para reconstruir um servidor no caso de um problema de hardware.  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>Exibir uma lista de cmdlets do PowerPivot em um servidor  
 Para ver o conteúdo e exemplos do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cmdlets, consulte [referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
 Para usar o PowerShell para exibir uma lista de cmdlets do PowerPivot:  
  
1.  Abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador** .  
  
2.  Insira o seguinte comando:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Você deve ver uma lista de cmdlets que incluem PowerPivot no nome do cmdlet. Por exemplo, `Get-PowerPivotServiceApplication`. O número de cmdlets disponíveis depende da versão do Analysis Services que você está usando.  
  
    -   10 cmdlets com o servidor SQL Server 2012 SP1 Analysis Services configurados no modo do SharePoint e com o SharePoint 2013. A versão 2012 SP1 utiliza uma nova arquitetura que permite ao Analysis Server ser executado fora do farm do SharePoint e exige menos cmdlets do Windows PowerShell de gerenciamento.  
  
    -   17 cmdlets com o servidor SQL Server 2012 Analysis Services configurados no modo do SharePoint e com o SharePoint 2010.  
  
     Se nenhum comando é retornado na lista ou se você vir uma mensagem de erro semelhante a "`get-help could not find *powerpivot* in a help file in this session.`", consulte a próxima seção neste tópico para obter instruções sobre como habilitar os cmdlets do PowerPivot no servidor.  
  
     Todos os cmdlets têm ajuda online. O exemplo a seguir mostra como exibir a ajuda online para o cmdlet `New-PowerPivotServiceApplication`:  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     Como alternativa, para exibir apenas os exemplos, use a sintaxe a seguir:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>Habilitar cmdlets do PowerPivot em um servidor  
 Os cmdlets do PowerPivot estão disponíveis depois que você instala o PowerPivot para SharePoint e implanta a solução de farm. As soluções são implantadas quando você executa a ferramenta de Configuração do PowerPivot. Siga estas etapas para habilitar o uso de cmdlets:  
  
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
 [Administração e configuração de servidor do PowerPivot na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Ferramentas de Configuração do PowerPivot](power-pivot-configuration-tools.md)  
  
 [Referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
  
