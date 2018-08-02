---
title: Nome de elemento (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: aa5073bd0728035ff4940b66fd2593eaf13cfd44
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044040"
---
# <a name="name-element-assl"></a>Elemento Name (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (até 100 caracteres)|  
|Valor padrão|Varia|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md), [agregação](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [anotação](../../../analysis-services/scripting/objects/annotation-element-assl.md), [ Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md), [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [Grupo](../../../analysis-services/scripting/objects/group-element-assl.md), [hierarquia](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [nível](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [ Medida](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [partição](../../../analysis-services/scripting/objects/partition-element-assl.md), [permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [ Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md), [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md), [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md), [ Função](../../../analysis-services/scripting/objects/role-element-assl.md), [servidor](../../../analysis-services/scripting/objects/server-element-assl.md), [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md), [rastreamento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Cada elemento que é usado para definir um objeto (uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], uma hierarquia, um atributo e assim por diante) tem um **nome** elemento como uma propriedade. O valor de um **nome** elemento tem as seguintes restrições:  
  
-   O valor não pode conter espaços à esquerda ou direita. Se os espaços à esquerda ou à direita serão incluídos no valor de um **nome** elemento, os espaços serão implicitamente removidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   O valor não deve conter caracteres de controle. A presença de caracteres de controle em um nome não é recomendada, podendo, algumas vezes, resultar em erros de validação do XML.  
  
     Para os objetos criados com o **GetNewName** método [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], AMO procura e descarta subsequentemente caracteres de controle, espaços à esquerda ou à direita de espaços no nome do. Para este motivo, usando **GetNewName** é a abordagem recomendada para nomes de objeto de configuração.  
  
     No entanto, se você definir o **nome** propriedade diretamente, a mesma validação verificações não são executadas, possivelmente resultando em erros de validação de XML. A geração de um erro dependerá de qual caractere de controle aparece no nome.  
  
     Embora os caracteres de controle nunca devam ser usados em um nome de objeto, o Analysis Services não os evita expressamente. As versões anteriores do Analysis Services às vezes aceitavam caracteres de controle em um nome de objeto. Para este motivo, o SQL Server 2016 Analysis Services e posterior irá ignorar os caracteres de controle em um nome de objeto para evitar quebrar soluções antigas.  
  
-   Os valores reservados a seguir não podem ser usados:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 a COM9 (COM1, COM2, COM3 e assim por diante)  
  
    -   CON  
  
    -   LPT1 a LPT9 (LPT1, LPT2, LPT3 e assim por diante)  
  
    -   NUL  
  
    -   PRN  
  
 A tabela a seguir lista os caracteres adicionais que não podem ser usados dentro do valor de um **nome** elemento, dependendo do elemento pai.  
  
|Elemento pai|Caracteres inválidos|  
|--------------------|------------------------|  
|[Servidor](../../../analysis-services/scripting/objects/server-element-assl.md)|O nome deve seguir as regras para nomes do computador Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Os endereços IP não são válidos.|  
|[Fonte de dados](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?" [()]{}<>|  
|[Nível de](../../../analysis-services/scripting/objects/level-element-assl.md), [atributo do elemento](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! [] de + ={}<>|  
|Todos os outros elementos pai|.,;' `:/\\*&#124;?" & % $! [] () de + ={}<>|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ID &#40;ASSL&#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
