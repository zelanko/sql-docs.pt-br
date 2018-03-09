---
title: "Definir propriedades de dimensão de cubo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f4f83f8225cc233b45bb3f4299a700992902995
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="define-cube-dimension-properties"></a>Definir propriedades de dimensão de cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Uma dimensão de cubo é uma instância de uma dimensão do banco de dados dentro de um cubo. A dimensão do banco de dados pode ser usada em vários cubos e várias dimensões de cubo podem basear-se em uma única dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma dimensão de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|Controla como as agregações são criadas pelo Designer de Agregação no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa propriedade pode ter os seguintes valores:<br /><br /> **Completo**: todas as agregações do cubo devem incluir o membro All.<br /><br /> **Nenhum**: nenhuma agregação do cubo pode incluir o membro All. Este é o valor padrão.<br /><br /> **Unrestricted**: nenhuma restrição é imposta pelo Designer de Agregação.<br /><br /> **Default**: a mesma funcionalidade que Unrestricted.|  
|**Description**|Fornece um nome descritivo para o nível.|  
|**DimensionID**|Contém o identificador exclusivo (ID) da dimensão do banco de dados.|  
|**HierarchyUniqueNameStyle**|Determina como são gerados os nomes exclusivos para hierarquias contidas na dimensão de cubo. Essa propriedade pode ter os seguintes valores:<br /><br /> **IncludeDimensionName**:<br />                    O nome da dimensão é incluído como parte do nome da hierarquia. Este é o valor padrão.<br /><br /> **ExcludeDimensionName**:<br />                    O nome da dimensão não é incluído como parte do nome da hierarquia.|  
|**ID**|Contém o identificador exclusivo (ID) da dimensão de cubo.|  
|**MemberUniqueNameStyle**|Determina como são gerados os nomes exclusivos para membros das hierarquias contidas na dimensão de cubo. Essa propriedade pode ter os seguintes valores:<br /><br /> **Native**:<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automaticamente os nomes exclusivos dos membros. Este é o valor padrão.<br /><br /> **NamePath**: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera um nome composto formado pelo nome de cada nível e a legenda do membro.|  
|**Nome**|Contém o nome amigável da dimensão de cubo. Por padrão, o nome de uma dimensão de cubo é igual ao da dimensão do banco de dados, exceto se existir uma outra dimensão definida com o mesmo nome.|  
|**Visível**|Determina se a dimensão de cubo é visível. O valor padrão é **True**.|  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões &#40; Analysis Services - dados multidimensionais &#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
