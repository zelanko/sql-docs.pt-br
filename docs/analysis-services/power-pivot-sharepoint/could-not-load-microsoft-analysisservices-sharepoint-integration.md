---
title: "Não foi possível carregar o 'Microsoft.AnalysisServices.SharePoint.Integration' | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a69a219376c2a67b003eaa6769843dc23791d829
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="could-not-load-microsoftanalysisservicessharepointintegration"></a>Não foi possível carregar Microsoft.AnalysisServices.SharePoint.Integration
  Em ambientes do SharePoint 2010 com o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, este erro ocorrerá se a solução no nível de aplicativo para o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não tiver sido implantada corretamente.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|A solução Powerpivotwebapp não está implantada ou não foi implantada corretamente.|  
|Texto da mensagem|Não foi possível carregar arquivo ou assembly 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## <a name="explanation"></a>Explicação  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa pacotes de solução para implantar seus recursos em um servidor do SharePoint. Uma das soluções não está implantada corretamente. Como resultado, esse erro aparece sempre que você tenta abrir a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou outras páginas de aplicativo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um site do SharePoint.  
  
## <a name="user-action"></a>Ação do usuário  
 Implantar o pacote de solução.  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp**.  
  
3.  Clique em **Implantar Solução**.  
  
4.  Escolha o aplicativo Web para o qual este erro está ocorrendo. Se houver mais de um aplicativo Web, reimplante a solução para todos eles.  
  
5.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar soluções Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  

