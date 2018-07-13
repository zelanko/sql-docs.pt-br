---
title: Gerenciando Caches (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da13c86e86a2f51719a9d4f0aedfda33935766ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180796"
---
# <a name="managing-caches-xmla"></a>Gerenciando caches (XMLA)
  Você pode usar o [ClearCache](../xmla/xml-elements-commands/clearcache-element-xmla.md) no XML for Analysis (XMLA) para limpar o cache de uma dimensão ou partição especificada. Limpeza do cache força [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para recriar o cache para esse objeto.  
  
## <a name="specifying-objects"></a>Especificando objetos  
 O [objeto](../xmla/xml-elements-properties/object-element-xmla.md) propriedade do `ClearCache` comando pode conter uma referência de objeto somente para um dos seguintes objetos. Haverá um erro se uma referência de objeto for destinada a um objeto diferente de um dos seguintes objetos:  
  
 banco de dados  
 Limpa o cache para todas as dimensões e partições contidas no banco de dados.  
  
 Dimensão  
 Limpa o cache para a dimensão especificada.  
  
 Cube  
 Limpa o cache para todas as partições contidas nos grupos de medidas para o cubo.  
  
 Grupo de medidas  
 Limpa o cache para todas as partições contidas no grupo de medidas.  
  
 Partition  
 Limpa o cache para a partição especificada.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
