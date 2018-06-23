---
title: Nome de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Name
helpviewer_keywords:
- Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cb2185d9d2a87a2abc3ebb96ad8186fe288e6190
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020788"
---
# <a name="name-element-assl"></a>Elemento Name (ASSL)
  Contém o nome do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (até 100 caracteres)|  
|Valor padrão|Varia|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Action](../objects/action-element-assl.md), [Aggregation](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [Annotation](../objects/annotation-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md), [Cube](../objects/cube-element-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Group](../objects/group-element-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Measure](../objects/measure-element-assl.md), [MeasureGroup](../objects/measuregroup-element-assl.md), [MemberProperty](../objects/attributerelationship-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md), [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [Role](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md), [Trace](../objects/trace-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Cada elemento que é usado para definir um objeto (uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], uma hierarquia, um atributo e assim por diante) tem um `Name` elemento como uma propriedade. O valor de um elemento `Name` tem as seguintes restrições:  
  
-   O valor não pode conter espaços à esquerda ou direita. Se os espaços à esquerda ou direita forem incluídos no valor de um elemento `Name`, eles serão implicitamente removidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   O valor não deve conter caracteres de controle. A presença de caracteres de controle em um nome não é recomendada, podendo, algumas vezes, resultar em erros de validação do XML.  
  
     Para objetos criados através do método de `GetNewName` em [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], o AMO procura e descarta subsequentemente todos os caracteres de controle, espaços à esquerda ou espaços à direita no nome. Por isso, o uso de `GetNewName` é a abordagem recomendada para definir nomes de objeto.  
  
     No entanto, se você definir a propriedade `Name` diretamente, as mesmas verificações de validação não serão executadas, o que possivelmente resultará em erros de validação do XML. A geração de um erro dependerá de qual caractere de controle aparece no nome.  
  
     Embora os caracteres de controle nunca devam ser usados em um nome de objeto, o Analysis Services não os evita expressamente. As versões anteriores do Analysis Services às vezes aceitavam caracteres de controle em um nome de objeto. Por isso, o [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] ignorará os caracteres de controle em um nome de objeto para evitar o insucesso de soluções antigas.  
  
-   Os valores reservados a seguir não podem ser usados:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 a COM9 (COM1, COM2, COM3 e assim por diante)  
  
    -   CON  
  
    -   LPT1 a LPT9 (LPT1, LPT2, LPT3 e assim por diante)  
  
    -   NUL  
  
    -   PRN  
  
 A tabela a seguir lista os caracteres adicionais que não podem ser usados no valor de um elemento `Name`, dependendo do elemento pai.  
  
|Elemento pai|Caracteres inválidos|  
|--------------------|------------------------|  
|[Servidor](../objects/server-element-assl.md)|O nome deve seguir as regras para nomes do computador Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Os endereços IP não são válidos.|  
|[Fonte de dados](../objects/datasource-element-assl.md)|:/\\*&#124;?" [()]{}<>|  
|[Nível de](../objects/level-element-assl.md), [atributo do elemento](../objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! [] de + ={}<>|  
|Todos os outros elementos pai|.,;' `:/\\*&#124;?" & % $! [] () de + ={}<>|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ID &#40;ASSL&#41;](id-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  