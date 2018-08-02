---
title: Elemento NamingTemplate (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f6b25e36c78d8e03afd0c4a3ebb4ef9a96d2c9f8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040486"
---
# <a name="namingtemplate-element-assl"></a>Elemento NamingTemplate (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define como os níveis são nomeados em uma hierarquia pai-filho construída a partir de [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
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
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor da **NamingTemplate** elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento do **DimensionAttribute** elemento pai é definido como *pai*).  
  
 Quando um atributo pai é usado para construir uma hierarquia, os níveis da hierarquia são determinados pelas relações pai-filho entre os membros contidos no atributo pai. Entretanto, ao contrário de outras dimensões, os nomes de nível não podem ser formulados a partir dos nomes de atributo usados para a hierarquia.  
  
 Em vez disso, um modelo de nomeação é usado para gerar os nomes de nível para hierarquias pai-filho. O elemento **NamingTemplate** , definido no atributo pai, contém uma expressão de cadeia de caracteres usada para definir os nomes de nível. Existem duas formas para definir um modelo de nomeação para um atributo pai. Você pode projetar um padrão de nomeação ou pode especificar uma lista de nomes.  
  
 Um padrão de nomeação contém um asterisco (`*`) como um caractere de espaço reservado para um contador que é incrementado e inserido no nome de cada nível novo e que vai mais adiante. Por exemplo, o uso de `Level *` resulta em nomes de nível como `Level 01`, `Level 02`, `Level 03`e assim por diante, no caso de nenhum (Todos) nível ter sido definido. Se um padrão de nomeação não tiver o caractere de espaço reservado, a primeira ocorrência será usada conforme seu nome original, e aos nomes de nível subsequentes serão anexados um espaço e um número no final do padrão. Por exemplo, o uso de `Level` resulta em nomes de nível como `Level`, `Level 01`, `Level 02`e assim por diante.  
  
 Para usar um conjunto de nomes específico para a nomeação, o valor do elemento **NamingTemplate** é definido como uma lista de nomes de nível delimitada por ponto-e-vírgula. Cada um dos nomes na lista é usado para um nome de nível subsequente. Se o número de níveis exceder o número de nomes na lista, o último nome na lista será usado como um modelo para os demais nomes de nível, e a eles serão aplicados um espaço e um número ordinal anexado ao último nome, conforme descrito anteriormente. Por exemplo, o uso de `Division;Group;Unit` resulta em nomes de nível como `Division`, `Group`, `Unit`, `Unit 01`, `Unit 02`e assim por diante. Em contrapartida, o uso de `Division;Group;Unit *` resulta em nomes de nível como `Division`, `Group`, `Unit 03`, `Unit 04`e assim por diante.  
  
 Cada nome na lista é tratado como um modelo para garantir a exclusividade dos nomes de nível. Por exemplo, o uso de `Manager;Team Lead;Manager;Team Lead;Worker *` resulta em nomes de nível como `Manager`, `Team Lead`, `Manager 01`, `Team Lead 01`, `Worker 05`, `Worker 06`.  
  
 Use dois asteriscos (*) para incluir o asterisco (\*) caractere em um nome de nível como parte de um modelo de nomeação.  
  
 O elemento que corresponde ao pai do **NamingTemplate** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento NamingTemplateTranslations &#40;ASSL&#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)   
 [Tipo de dados DimensionAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
