---
title: Gerenciando Caches (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e99be9f6a2af7dbbaab624ba592b2486cf807f2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048156"
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
  
  
