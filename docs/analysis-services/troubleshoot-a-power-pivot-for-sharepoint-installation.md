---
title: "Solu&#231;&#227;o de problemas de instala&#231;&#227;o do Power Pivot para SharePoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Solu&#231;&#227;o de problemas de instala&#231;&#227;o do Power Pivot para SharePoint
  Se você obtiver erros em vez das páginas e recursos que você esperava, faça o seguinte.  
  
-   Revise as notas de versão do SharePoint e do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para obter soluções alternativas para problemas de instalação conhecidos. As notas de versão são fornecidas com a mídia de instalação ou no site da Microsoft do qual você baixou o software.  
  
    -   [Notas de Versão do SQL Server 2016.](../sql-server/sql-server-2016-release-notes.md)  
  
-   Consulte o tópico da wiki do TechNet, [Troubleshooting Installations of Power Pivot (and other add-ins)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx) [Solucionando problemas de instalações do Power Pivot (e outros suplementos)].  
  
## Problemas  
  
### As imagens em miniatura da Galeria do PowerPivot são exibidas como um X vermelho  
 Uma causa possível é que a Integração de Recursos do **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Coleções de Sites** não está ativa. Preencha o seguinte:  
  
1.  Na biblioteca da Galeria do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], clique em **Configurações do Site** por meio do ícone de engrenagem ![Configurações do SharePoint](../analysis-services/media/as-sharepoint2013-settings-gear.png "Configurações do SharePoint") ou da lista da **Página Inicial**.  
  
2.  Na seção **Administração do Conjunto de Sites** , clique em **Recursos do Conjunto de Sites**.  
  
3.  Clique em **Recursos do Conjunto de Sites**.  
  
4.  Verifique se a Integração de Recursos do **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Coleções de Sites** está **Ativa**.  
  
 Para saber as causas adicionais desse problema, consulte [Power Pivot Gallery shows Red X's for Icons](http://support.microsoft.com/kb/2361559) [A Galeria do PowerPivot mostra Xs vermelhos em vez de ícones] (http://support.microsoft.com/kb/2361559).  
  
  