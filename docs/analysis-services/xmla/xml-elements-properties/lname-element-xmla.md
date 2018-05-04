---
title: Elemento LName (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LName Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#LName
- http://schemas.microsoft.com/analysisservices/2003/engine#LName
- microsoft.xml.analysis.lname
helpviewer_keywords:
- LName element
ms.assetid: 2c8c2fa9-cb2d-44ea-b253-5e6ff61f1b66
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 80457ad8055ea2c69b75f578a7e5fcb486461ef4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lname-element-xmla"></a>Elemento LName (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém informações sobre nomes de nível exclusivos para o pai [HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md) ou [membro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LName>...</LName>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md), [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para **HierarchyInfo** elementos, esse elemento contém o nome da propriedade que fornece os nomes exclusivos de nível da hierarquia. O valor é equivalente à propriedade LEVEL_UNIQUE_NAME definida para conjuntos de linhas de eixo no comando OLE DB para a especificação OLAP.  
  
 Para **membro** elementos, esse elemento contém o nome exclusivo do nível na hierarquia que contém o membro representado pelo pai **membro** elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
