---
title: Solucionar problemas de um PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 26ed6e178e6aea91aa3b0fa5aaedf3926f5d908a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161747"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Solução de problemas da instalação do PowerPivot para SharePoint
  Se você obtiver erros em vez das páginas e recursos que você esperava, faça o seguinte.  
  
-   Revise as notas de versão do SharePoint e do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para obter soluções alternativas para problemas de instalação conhecidos. As notas de versão são fornecidas com a mídia de instalação ou no site da Microsoft do qual você baixou o software.  
  
    -   [Notas de Versão do SQL Server 2014](http://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Consulte o tópico de wiki do Technet, [Solução de problemas de instalações do PowerPivot (e outros suplementos)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Problemas  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>As imagens em miniatura para Galeria PowerPivot são exibidas como um X vermelho  
 Uma causa possível é que a **Integração de recursos do PowerPivot para coleções de sites** não está ativa. Preencha o seguinte:  
  
1.  Na biblioteca da Galeria PowerPivot, clique em **configurações de Site** no ícone de engrenagem ![configurações do SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Settings") ou o **Home** lista.  
  
2.  Na seção **Administração do Conjunto de Sites** , clique em **Recursos do Conjunto de Sites**.  
  
3.  Clique em **Recursos do Conjunto de Sites**.  
  
4.  Verifique se a **Integração de recursos do PowerPivot para coleções de sites** está **Ativa**.  
  
 Para obter as causas adicionais desse problema, consulte [Galeria do PowerPivot mostra Xs vermelhos em vez de ícones](http://support.microsoft.com/kb/2361559) (http://support.microsoft.com/kb/2361559).  
  
  
