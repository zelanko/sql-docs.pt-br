---
title: Tipo de dados TableBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 475044a0bcad3c90ffaffa71eeeb6735a37f96c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220246"
---
# <a name="tablebinding-data-type-assl"></a>Tipo de dados TableBinding (ASSL)
  Define um tipo de dados derivado que representa uma associação a uma tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<TableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceID>...</DataSourceID>  
   <DbTableName>...</DbTableName>  
   <DbSchemaName>...</DbSchemaName>  
</TableBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|[TabularBinding](binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[DataSourceID](../properties/id-element-assl.md), [DbSchemaName](../properties/name-element-assl.md), [DbTableName](../properties/dbtablename-element-assl.md)|  
|Elementos derivados|Consulte [de associação](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Observe que fazer referência a outras tabelas na expressão do filtro pelo uso de uma subseleção pode causar implicações de desempenho em algumas fontes de dados. No entanto, o designer pode controlar totalmente a expressão SQL, definindo uma consulta nomeada na exibição da fonte de dados e, em seguida, fazendo referência a ela.  
  
 O método de definição das associações de uma partição independem do uso de tabelas particionadas na exibição da fonte de dados.  
  
 Como exemplo, considere um grupo de medidas cuja tabela padrão seja "Vendas", como as colunas Data, ID do produto, Qtd., Preço e Total (calculado na exibição da fonte de dados). Então a partição "Sales97" poderia usar o tabela "Sales97" com o filtro "Year (Sales.Date) = 97."  
  
 A consulta efetiva é:  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 A expressão calculada ainda se aplica, até mesmo se a expressão tenha utilizado nomes de tabelas qualificados (por exemplo, Sales.Qty). O mesmo se aplica se, em vez disso, as tabelas fossem substituídas pela mesma consulta "SELECT…" A cláusula FROM acima iria se tornar "FROM SELECT ... As Sales."  
  
 Para obter mais informações sobre o `Binding` tipo, incluindo as tabelas de objetos do Analysis Services Scripting Language (ASSL) do tipo `Binding` e a hierarquia de herança dos `Binding` tipos, consulte [tipo de associação de dados &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.TableBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados de associação &#40;ASSL&#41;](binding-data-type-assl.md)   
 [Fontes de dados e associações &#40;Multidimensional do SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
