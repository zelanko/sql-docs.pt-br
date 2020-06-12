---
title: Não foi possível carregar o arquivo ou assembly &#39;Microsoft. AnalysisServices. SharePoint. Integration&#39; | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9baec97f8d1e779a84f25e7ddbf437e0a40ef4b3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547488"
---
# <a name="could-not-load-file-or-assembly-39microsoftanalysisservicessharepointintegration39"></a>Não foi possível carregar o arquivo ou assembly &#39;Microsoft. AnalysisServices. SharePoint. Integration&#39;
  Em ambientes do SharePoint 2010 com o PowerPivot para SharePoint, este erro ocorrerá se a solução no nível de aplicativo para o PowerPivot não tiver sido implantada corretamente.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|A solução Powerpivotwebapp não está implantada ou não foi implantada corretamente.|  
|Texto da mensagem|Não foi possível carregar arquivo ou assembly 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## <a name="explanation"></a>Explicação  
 O PowerPivot para SharePoint usa pacotes de solução para implantar seus recursos em um servidor do SharePoint. Uma das soluções não está implantada corretamente. Como resultado, este erro aparece sempre que você tenta abrir a Galeria PowerPivot ou outras páginas de aplicativo do PowerPivot em um site do SharePoint.  
  
## <a name="user-action"></a>Ação do usuário  
 Implantar o pacote de solução.  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp**.  
  
3.  Clique em **Implantar Solução**.  
  
4.  Escolha o aplicativo Web para o qual este erro está ocorrendo. Se houver mais de um aplicativo Web, reimplante a solução para todos eles.  
  
5.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar soluções PowerPivot para SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
