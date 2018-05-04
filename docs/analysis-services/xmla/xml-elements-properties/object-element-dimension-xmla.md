---
title: Objeto de elemento (dimensão) (XMLA) | Microsoft Docs
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
- Object Element (Dimension)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords:
- Object element
ms.assetid: db7feb39-7cc1-4b54-8979-77ce402ef71f
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: faf8544bfac0ed161276f6d5bb7352780af40545
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="object-element-dimension-xmla"></a>Elemento Object (Dimension) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém uma referência de objeto para a dimensão na qual o pai [inserir](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [atualização](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), ou [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) comando é executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Insert> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <Database>...</Database>  
      <Cube>...</Cube>  
      <Dimension>...</Dimension>  
   </Object>  
...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Descartar](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [inserir](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [atualização](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|Elementos filho|[Cubo](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md), [banco de dados](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md), [dimensão](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
