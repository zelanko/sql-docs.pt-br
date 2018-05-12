---
title: Definir propriedades de dimensão de cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4401055a15afe73a1f33ee43354f7ee45f887a96
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
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
 [Dimensões & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
