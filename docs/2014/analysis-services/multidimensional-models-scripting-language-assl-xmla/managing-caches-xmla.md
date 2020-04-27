---
title: Gerenciando caches (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 72e36e7d8f0efc9880d0dd164a253030712ee120
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727582"
---
# <a name="managing-caches-xmla"></a>Gerenciando caches (XMLA)
  Você pode usar o comando [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) no XML for Analysis (XMLA) para limpar o cache de uma dimensão ou partição especificada. Limpar as forças [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de cache para recriar o cache para esse objeto.  
  
## <a name="specifying-objects"></a>Especificando objetos  
 A propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `ClearCache` comando pode conter uma referência de objeto somente para um dos objetos a seguir. Haverá um erro se uma referência de objeto for destinada a um objeto diferente de um dos seguintes objetos:  
  
 Banco de dados  
 Limpa o cache para todas as dimensões e partições contidas no banco de dados.  
  
 Dimensão  
 Limpa o cache para a dimensão especificada.  
  
 Cube  
 Limpa o cache para todas as partições contidas nos grupos de medidas para o cubo.  
  
 Grupo de medidas  
 Limpa o cache para todas as partições contidas no grupo de medidas.  
  
 Partition  
 Limpa o cache para a partição especificada.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
