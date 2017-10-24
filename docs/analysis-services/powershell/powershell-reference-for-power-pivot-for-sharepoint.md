---
title: "Referência do PowerShell para PowerPivot para SharePoint | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c01735a8-f919-48ad-8d74-35d75a18f821
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39567e2b212761ac2dd726a1f8f33893a83f245c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>Referência do PowerShell para Power Pivot para SharePoint

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Esta seção lista os cmdlets PowerShell usados para configurar ou administrar uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obter mais informações sobre como habilitar os cmdlets e exibir a ajuda interna, consulte [Configuração do Power Pivot usando o Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="cmdlet-list"></a>Lista de cmdlets  
 Para ver uma lista de cmdlets do prompt do PowerShell:  
  
1.  Abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador** .  
  
2.  Insira o seguinte comando: `Get-help *powerpivot*`  
  
|Cmdlet|Versões com suporte|  
|------------|------------------------|  
|[Cmdlet Get-PowerPivotServiceApplication](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Get-PowerPivotSystemService](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Get-PowerPivotSystemServiceInstance](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet New-PowerPivotServiceApplication](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet New-PowerPivotSystemServiceInstance](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Remove-PowerPivotServiceApplication](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Remove-PowerPivotSystemServiceInstance](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Set-PowerPivotServiceApplication](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Set-PowerPivotSystemService](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Cmdlet Update-PowerPivotSystemService](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
  
 Observação: os Cmdlets a seguir só trabalham com o SharePoint 2010, ao qual o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] não dá suporte.  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  

