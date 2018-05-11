---
title: Elemento AggregationPrefix (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 224c954186bff2b8e08375bfccf43ad980209f87
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationprefix-element-assl"></a>Elemento AggregationPrefix (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define o prefixo comum a ser usado para nomes de agregação no elemento pai associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Prefixos de agregação geram os nomes de agregação em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e também gerar nomes de tabela no banco de dados relacional para agregações armazenadas em uma partição OLAP (ROLAP) relacional.  
  
 Um nome de agregação completamente expandido tem as partes a seguir:  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 As primeiras quatro partes do nome de agregação compõem o prefixo de agregação. O usuário fornece as primeiras quatro partes:  
  
-   *DatabasePrefix* representa o valor do elemento **AggregationPrefix** associado a um elemento **Database** .  
  
-   *CubePrefix* representa o valor do elemento **AggregationPrefix** associado a um elemento **Cube** .  
  
-   *MeasureGroupPrefix* representa o valor do elemento **AggregationPrefix** associado a um elemento **MeasureGroup** .  
  
-   *PartitionPrefix* representa o valor do elemento **AggregationPrefix** associado a um elemento **Partition** .  
  
 A quinta parte do nome, *AggregationID*, é uma ID definida pelo sistema, e os usuários não têm nenhum controle sobre essa parte do nome.  
  
 Os elementos que correspondem aos pais de **AggregationPrefix** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup>, e <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
