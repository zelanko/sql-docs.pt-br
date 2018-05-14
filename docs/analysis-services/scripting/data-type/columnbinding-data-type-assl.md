---
title: Tipo de dados ColumnBinding (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55c16d18e7ffbe9a53ec80af12f4c111788dc6f4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="columnbinding-data-type-assl"></a>Tipo de dados ColumnBinding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define um tipo de dados derivado que representa a associação de uma coluna em uma exibição da fonte de dados para um [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Associação](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md), [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|Elementos derivados|Consulte [Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Para criar nomes de elemento XML válidos, [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] **DataSet** objetos codificam nomes de tabela à medida que são serializados para definição de esquema XML (XSD); por exemplo, o nome "Order Details" se torna "Order_x0020_Details". Da mesma forma, o **ColumnID** e **TableID** elementos contidos pelo **ColumnBinding** elemento e também devem codificar os objetos de referência na exibição da fonte de dados (DSV) nomes durante a serialização, para garantir que os nomes correspondem diretamente o texto no DSV. A instância do Analysis Services descriptocrafará esses nomes, assim como o **conjunto de dados** modelo de objeto.  
  
 Um **TableDefinitions** elemento contido por um elemento usando o **TableBinding** que se refere a tabelas na DSV e tipo de dados devem também codificar nomes à medida que são serializados em XSD. No entanto, os nomes de tabelas no **partição** associações não devem ser codificadas porque essas são simplesmente nomes de tabelas que existem no banco de dados e não precisam estar no DSV. Nomes de codificação não a tabela no **partição** associações também usa as seguintes:  
  
-   Manter a biblioteca de definição de dados (DDL) para partições mais simples.  
  
-   Fornecer mais consistência porque as partições podem ter um nome de tabela ou uma instrução SELECT, que não deve ser codificada.  
  
 Os nomes de tabela e coluna não incluem delimitadores (por exemplo, "[" para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
 Para obter informações adicionais sobre o **associação** tipo, incluindo tabelas de objetos do Analysis Services Scripting Language (ASSL) da **associação** tipo e a hierarquia de herança de  **Associação** tipos, consulte [tipo de dados de associação &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obter uma visão geral de associações de dados em ASSL, consulte [fontes de dados e associações & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 O elemento correspondente no modelo de objeto AMO é <xref:Microsoft.AnalysisServices.ColumnBinding>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
