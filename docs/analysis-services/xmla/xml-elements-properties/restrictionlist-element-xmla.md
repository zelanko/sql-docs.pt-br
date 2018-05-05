---
title: Elemento RestrictionList (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- RestrictionList Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 92ed6ac616035bd819c2e99bd869910f150845f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="restrictionlist-element-xmla"></a>Elemento RestrictionList (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma coleção de colunas de restrição e valores usados pelo método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Restrições](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|Elementos filho|Colunas e valores de restrição (consulte os Comentários).|  
  
## <a name="remarks"></a>Remarks  
 O elemento **RestrictionList** contém uma coleção de colunas de restrição na qual os dados retornados pelo método **Discover** podem ser filtrados. Cada coluna de restrição no elemento **RestrictionList** está definida por um elemento XML separado. O valor da coluna de restrição são os dados contidos pelo elemento XML e o nome da coluna de restrição corresponde ao nome do elemento XML.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
