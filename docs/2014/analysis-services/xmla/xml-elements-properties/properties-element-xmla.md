---
title: Elemento Properties (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Properties Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Properties
- microsoft.xml.analysis.properties
- urn:schemas-microsoft-com:xml-analysis#Properties
- Properties
helpviewer_keywords:
- Properties element
ms.assetid: 0b5468e5-bf23-4d22-862f-72e27a9fff2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83234d39c39ec4e52d387f074a3f2d753ef323d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054836"
---
# <a name="properties-element-xmla"></a>Elemento Properties (XMLA)
  Contém o XML para as propriedades do Analysis (XMLA) usadas pelo [Discover](../xml-elements-methods-discover.md) e [Execute](../xml-elements-methods-execute.md) métodos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Discover> <!-- or Execute -->  
...  
   <Properties>  
      <PropertyList>...</PropertyList>  
   </Properties>  
...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Descubra](../xml-elements-methods-discover.md), [executar](../xml-elements-methods-execute.md)|  
|Elementos filho|[PropertyList](propertylist-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento `Properties` representa as propriedades XMLA usadas para controlar os aspectos dos métodos `Discover` e `Execute`, como a definição de informações obrigatórias para estabelecer conexão com a fonte de dados, a especificação do formato de retorno do conjunto de resultados ou a especificação da localidade na qual os dados devem ser formatados.  
  
 As propriedades disponíveis e seus valores podem ser obtidos usando o tipo de solicitação DISCOVER_PROPERTIES com o `Discover` método.  
  
## <a name="example"></a>Exemplo  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
