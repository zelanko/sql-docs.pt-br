---
title: Tipo de dados ColumnBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ColumnBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnBinding
helpviewer_keywords:
- ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 227801af8b66d66ebeba50d2713267720adffa9a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200106"
---
# <a name="columnbinding-data-type-assl"></a>Tipo de dados ColumnBinding (ASSL)
  Define um tipo de dados derivado que representa a associação de uma coluna em uma exibição da fonte de dados para um [DataItem](dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[ColumnID](../properties/columnid-element-eventcolumn-assl.md), [TableID](../properties/id-element-assl.md)|  
|Elementos derivados|Consulte [de associação](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para criar nomes de elemento XML válidos, [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] `DataSet` objetos codificam nomes de tabela à medida que são serializados para definição de esquema XML (XSD); por exemplo, o nome "Order Details" torna-se "Order_x0020_Details". Do mesmo modo, os elementos `ColumnID` e `TableID` contidos pelo elemento `ColumnBinding` e os objetos de referência na exibição da fonte de dados também devem codificar nomes durante a serialização para assegurar a correspondência direta dos nomes na exibição da fonte de dados. A instância do Analysis Services descriptocrafará esses nomes, assim como faz o modelo de objeto `DataSet`.  
  
 Um elemento `TableDefinitions` contido por um elemento que usa o tipo de dados `TableBinding` e faz referência a tabelas da exibição da fonte de dados também deve codificar nomes à medida que são serializados em XSD. No entanto, os nomes de tabela nas associações de `Partition` não devem ser codificados porque eles são simplesmente nomes de tabelas que existem no banco de dados e não precisam estar na exibição da fonte de dados. Não codificar os nomes de tabela nas associações de `Partition` também significa o seguinte:  
  
-   Manter a biblioteca de definição de dados (DDL) para partições mais simples.  
  
-   Fornecer mais consistência porque as partições podem ter um nome de tabela ou uma instrução SELECT, que não deve ser codificada.  
  
 Os nomes de tabela e coluna não incluem delimitadores (por exemplo, "[" para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
 Para obter mais informações sobre o `Binding` tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da `Binding` tipo e a hierarquia de herança dos `Binding` tipos, consulte [ &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto AMO é <xref:Microsoft.AnalysisServices.ColumnBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
