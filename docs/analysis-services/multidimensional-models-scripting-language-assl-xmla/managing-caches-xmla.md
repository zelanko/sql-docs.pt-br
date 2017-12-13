---
title: Gerenciando Caches (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6dad9f3bb8c577ea8fb975d4f8ba4eac054f0a3e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="managing-caches-xmla"></a>Gerenciando caches (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Você pode usar o [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) do XML for Analysis (XMLA) para limpar o cache de uma dimensão ou partição especificada. Limpeza do cache força [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para recriar o cache para esse objeto.  
  
## <a name="specifying-objects"></a>Especificando objetos  
 O [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade o **ClearCache** comando pode conter uma referência de objeto somente para um dos seguintes objetos. Haverá um erro se uma referência de objeto for destinada a um objeto diferente de um dos seguintes objetos:  
  
 Banco de Dados  
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
  
  
