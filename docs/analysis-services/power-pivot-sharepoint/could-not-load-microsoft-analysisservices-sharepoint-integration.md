---
title: "N&#227;o foi poss&#237;vel carregar arquivo ou assembly &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 7
---
# N&#227;o foi poss&#237;vel carregar arquivo ou assembly &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39;
  Em ambientes do SharePoint 2010 com o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, este erro ocorrerá se a solução no nível de aplicativo para o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não tiver sido implantada corretamente.  
  
## Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|A solução Powerpivotwebapp não está implantada ou não foi implantada corretamente.|  
|Texto da mensagem|Não foi possível carregar arquivo ou assembly 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## Explicação  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa pacotes de solução para implantar seus recursos em um servidor do SharePoint. Uma das soluções não está implantada corretamente. Como resultado, esse erro aparece sempre que você tenta abrir a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou outras páginas de aplicativo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um site do SharePoint.  
  
## Ação do usuário  
 Implantar o pacote de solução.  
  
1.  Na Administração Central, em Configurações do Sistema, clique em **Gerenciar soluções de farm**.  
  
2.  Clique em **Powerpivotwebapp**.  
  
3.  Clique em **Implantar Solução**.  
  
4.  Escolha o aplicativo Web para o qual este erro está ocorrendo. Se houver mais de um aplicativo Web, reimplante a solução para todos eles.  
  
5.  Clique em **OK**.  
  
## Consulte também  
 [Implantar soluções Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  