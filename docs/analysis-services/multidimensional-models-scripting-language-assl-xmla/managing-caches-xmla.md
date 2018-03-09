---
title: Gerenciando Caches (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1b9c03bfa8c320eac3a3eb81b705f295122c337e
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="managing-caches-xmla"></a>Gerenciando caches (XMLA)
  Você pode usar o [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) do XML for Analysis (XMLA) para limpar o cache de uma dimensão ou partição especificada. Limpeza do cache força [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para recriar o cache para esse objeto.  
  
## <a name="specifying-objects"></a>Especificando objetos  
 O [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade o **ClearCache** comando pode conter uma referência de objeto somente para um dos seguintes objetos. Haverá um erro se uma referência de objeto for destinada a um objeto diferente de um dos seguintes objetos:  
  
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
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
