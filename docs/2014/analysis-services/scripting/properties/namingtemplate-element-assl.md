---
title: Elemento NamingTemplate (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplate
helpviewer_keywords:
- NamingTemplate element
ms.assetid: d68d765c-f012-40c1-acd4-32741ee2eadf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b1a167ffc7418d69b28e8436bb67238acc3284b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106306"
---
# <a name="namingtemplate-element-assl"></a>Elemento NamingTemplate (ASSL)
  Define como os níveis são nomeados em uma hierarquia pai-filho construída a partir de [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor da `NamingTemplate` elemento é usado somente por atributos pai (em outras palavras, o valor da [uso](usage-element-dimensionattribute-assl.md) elemento do `DimensionAttribute` elemento pai é definido como *pai*).  
  
 Quando um atributo pai é usado para construir uma hierarquia, os níveis da hierarquia são determinados pelas relações pai-filho entre os membros contidos no atributo pai. Entretanto, ao contrário de outras dimensões, os nomes de nível não podem ser formulados a partir dos nomes de atributo usados para a hierarquia.  
  
 Em vez disso, um modelo de nomeação é usado para gerar os nomes de nível para hierarquias pai-filho. O elemento `NamingTemplate`, definido no atributo pai, contém uma expressão de cadeia de caracteres usada para definir os nomes de nível. Existem duas formas para definir um modelo de nomeação para um atributo pai. Você pode projetar um padrão de nomeação ou pode especificar uma lista de nomes.  
  
 Um padrão de nomeação contém um asterisco (`*`) como um caractere de espaço reservado para um contador que é incrementado e inserido no nome de cada nível novo e que vai mais adiante. Por exemplo, o uso de `Level *` resulta em nomes de nível como `Level 01`, `Level 02`, `Level 03`e assim por diante, no caso de nenhum (Todos) nível ter sido definido. Se um padrão de nomeação não tiver o caractere de espaço reservado, a primeira ocorrência será usada conforme seu nome original, e aos nomes de nível subsequentes serão anexados um espaço e um número no final do padrão. Por exemplo, o uso de `Level` resulta em nomes de nível como `Level`, `Level 01`, `Level 02`e assim por diante.  
  
 Para usar um conjunto de nomes específico para a nomeação, o valor do elemento `NamingTemplate` é definido como uma lista de nomes de nível delimitada por ponto-e-vírgula. Cada um dos nomes na lista é usado para um nome de nível subsequente. Se o número de níveis exceder o número de nomes na lista, o último nome na lista será usado como um modelo para os demais nomes de nível, e a eles serão aplicados um espaço e um número ordinal anexado ao último nome, conforme descrito anteriormente. Por exemplo, o uso de `Division;Group;Unit` resulta em nomes de nível como `Division`, `Group`, `Unit`, `Unit 01`, `Unit 02`e assim por diante. Em contrapartida, o uso de `Division;Group;Unit *` resulta em nomes de nível como `Division`, `Group`, `Unit 03`, `Unit 04`e assim por diante.  
  
 Cada nome na lista é tratado como um modelo para garantir a exclusividade dos nomes de nível. Por exemplo, o uso de `Manager;Team Lead;Manager;Team Lead;Worker *` resulta em nomes de nível como `Manager`, `Team Lead`, `Manager 01`, `Team Lead 01`, `Worker 05`, `Worker 06`.  
  
 Use dois asteriscos (*) para incluir o asterisco (\*) caractere em um nome como parte de um modelo de nomeação de nível.  
  
 O elemento que corresponde ao pai de `NamingTemplate` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento NamingTemplateTranslations &#40;ASSL&#41;](../collections/translations-element-assl.md)   
 [Tipo de dados DimensionAttribute &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
