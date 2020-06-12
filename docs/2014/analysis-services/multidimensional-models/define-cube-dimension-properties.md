---
title: Definir propriedades da dimensão do cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9c58cf6a2f55e57c9faa65ddec72fe1bda6000c2
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547012"
---
# <a name="define-cube-dimension-properties"></a>Definir propriedades de dimensão de cubo
  Uma dimensão de cubo é uma instância de uma dimensão do banco de dados dentro de um cubo. A dimensão do banco de dados pode ser usada em vários cubos e várias dimensões de cubo podem basear-se em uma única dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma dimensão de cubo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`AllMemberAggregationUsage`|Controla como as agregações são projetadas pelo designer de agregação no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essa propriedade pode ter os seguintes valores:<br /><br /> **Completo**: todas as agregações do cubo devem incluir o membro All.<br /><br /> **Nenhum**: nenhuma agregação do cubo pode incluir o membro All. Esse é o valor padrão.<br /><br /> **Unrestricted**: nenhuma restrição é imposta pelo Designer de Agregação.<br /><br /> **Default**: a mesma funcionalidade que Unrestricted.|  
|`Description`|Fornece um nome descritivo para o nível.|  
|`DimensionID`|Contém o identificador exclusivo (ID) da dimensão do banco de dados.|  
|`HierarchyUniqueNameStyle`|Determina como são gerados os nomes exclusivos para hierarquias contidas na dimensão de cubo. Essa propriedade pode ter os seguintes valores:<br /><br /> `IncludeDimensionName`: o nome da dimensão é incluído como parte do nome da hierarquia. Esse é o valor padrão.<br /><br /> `ExcludeDimensionName`: o nome da dimensão não é incluído como parte do nome da hierarquia.|  
|`ID`|Contém o identificador exclusivo (ID) da dimensão de cubo.|  
|`MemberUniqueNameStyle`|Determina como são gerados os nomes exclusivos para membros das hierarquias contidas na dimensão de cubo. Essa propriedade pode ter os seguintes valores:<br /><br /> `Native`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automaticamente os nomes exclusivos dos membros. Esse é o valor padrão.<br /><br /> `NamePath`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera um nome composto formado pelo nome de cada nível e a legenda do membro.|  
|`Name`|Contém o nome amigável da dimensão de cubo. Por padrão, o nome de uma dimensão de cubo é igual ao da dimensão do banco de dados, exceto se existir uma outra dimensão definida com o mesmo nome.|  
|`Visible`|Determina se a dimensão de cubo é visível. O valor padrão é `True`.|  
  
## <a name="see-also"></a>Consulte Também  
 [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
