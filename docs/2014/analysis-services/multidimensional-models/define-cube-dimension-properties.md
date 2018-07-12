---
title: Definir propriedades de dimensão de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4bda79152cc17ef8f9e94afde2f8166ecd73ba4b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157057"
---
# <a name="define-cube-dimension-properties"></a>Definir propriedades de dimensão de cubo
  Uma dimensão de cubo é uma instância de uma dimensão do banco de dados dentro de um cubo. A dimensão do banco de dados pode ser usada em vários cubos e várias dimensões de cubo podem basear-se em uma única dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma dimensão de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|`AllMemberAggregationUsage`|Controla como as agregações são criadas pelo Designer de Agregação no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa propriedade pode ter os seguintes valores:<br /><br /> **Completo**: todas as agregações do cubo devem incluir o membro All.<br /><br /> **Nenhum**: nenhuma agregação do cubo pode incluir o membro All. Este é o valor padrão.<br /><br /> **Unrestricted**: nenhuma restrição é imposta pelo Designer de Agregação.<br /><br /> **Default**: a mesma funcionalidade que Unrestricted.|  
|`Description`|Fornece um nome descritivo para o nível.|  
|`DimensionID`|Contém o identificador exclusivo (ID) da dimensão do banco de dados.|  
|`HierarchyUniqueNameStyle`|Determina como são gerados os nomes exclusivos para hierarquias contidas na dimensão de cubo. Essa propriedade pode ter os seguintes valores:<br /><br /> `IncludeDimensionName`: O nome da dimensão é incluído como parte do nome da hierarquia. Este é o valor padrão.<br /><br /> `ExcludeDimensionName`: O nome da dimensão não é incluído como parte do nome da hierarquia.|  
|`ID`|Contém o identificador exclusivo (ID) da dimensão de cubo.|  
|`MemberUniqueNameStyle`|Determina como são gerados os nomes exclusivos para membros das hierarquias contidas na dimensão de cubo. Essa propriedade pode ter os seguintes valores:<br /><br /> `Native`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automaticamente os nomes exclusivos de membros. Este é o valor padrão.<br /><br /> `NamePath`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera um nome composto formado pelo nome de cada nível e a legenda do membro.|  
|`Name`|Contém o nome amigável da dimensão de cubo. Por padrão, o nome de uma dimensão de cubo é igual ao da dimensão do banco de dados, exceto se existir uma outra dimensão definida com o mesmo nome.|  
|`Visible`|Determina se a dimensão de cubo é visível. O valor padrão é `True`.|  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões &#40;Analysis Services - dados multidimensionais&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
