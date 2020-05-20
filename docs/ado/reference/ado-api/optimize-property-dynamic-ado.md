---
title: Otimizar propriedade-dinâmica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d27195b00d1e1867f6bf037cd6c20500ec35e84
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762079"
---
# <a name="optimize-property-dynamic-ado"></a>Otimizar a propriedade dinâmica (ADO)
Especifica se um índice deve ser criado em um [campo](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **booliano** que indica se um índice deve ser criado.  
  
## <a name="remarks"></a>Comentários  
 Um índice pode melhorar o desempenho das operações que localizam ou classificam valores em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). O índice é interno ao ADO; Você não pode acessá-lo ou usá-lo explicitamente em seu aplicativo.  
  
 Para criar um índice em um campo, defina a propriedade **Optimize** como **true**. Para excluir o índice, defina essa propriedade como **false**.  
  
 **Optimize** é uma propriedade dinâmica anexada à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto [Field](../../../ado/reference/ado-api/field-object.md) quando a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) é definida como **adUseClient**.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Optimize (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Exemplo da propriedade Optimize (VC + +)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Propriedade de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propriedade Sort](../../../ado/reference/ado-api/sort-property.md)
