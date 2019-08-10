---
title: Solucionar problemas de instalação de PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 797405386e8a6c0b9e62328699f3a73a6d845313
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892439"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Solução de problemas da instalação do PowerPivot para SharePoint
  Se você obtiver erros em vez das páginas e recursos que você esperava, faça o seguinte.  
  
-   Revise as notas de versão do SharePoint e do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para obter soluções alternativas para problemas de instalação conhecidos. As notas de versão são fornecidas com a mídia de instalação ou no site da Microsoft do qual você baixou o software.  
  
    -   [Notas de Versão do SQL Server 2014](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Consulte o tópico de wiki do Technet, [Solução de problemas de instalações do PowerPivot (e outros suplementos)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Problemas  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>As imagens em miniatura para Galeria PowerPivot são exibidas como um X vermelho  
 Uma causa possível é que a **Integração de recursos do PowerPivot para coleções de sites** não está ativa. Preencha o seguinte:  
  
1.  Na biblioteca da galeria do PowerPivot, clique ![](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "") em **configurações do site** no ícone de engrenagem configurações do SharePoint configurações ou na lista **inicial** .  
  
2.  Na seção **Administração do Conjunto de Sites** , clique em **Recursos do Conjunto de Sites**.  
  
3.  Clique em **Recursos do Conjunto de Sites**.  
  
4.  Verifique se a **Integração de recursos do PowerPivot para coleções de sites** está **Ativa**.  
  
 Para obter as causas adicionais desse problema, consulte a [Galeria PowerPivot mostra os ícones de X vermelho](https://support.microsoft.com/kb/2361559) (https://support.microsoft.com/kb/2361559).  
  
  
