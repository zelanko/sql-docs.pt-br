---
title: "Otimizar a propriedade dinâmica (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4aeae41d865e585c4c8b93c86bd6f8e9753eaea1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="optimize-property-dynamic-ado"></a>Otimizar a propriedade dinâmica (ADO)
Especifica se um índice deve ser criado em uma [campo](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **booliano** valor que indica se um índice deve ser criado.  
  
## <a name="remarks"></a>Comentários  
 Um índice pode melhorar o desempenho de operações que encontrar ou classificar valores em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md). O índice é interno ao ADO; não é possível acessar ou usá-lo em seu aplicativo explicitamente.  
  
 Para criar um índice em um campo, defina o **otimizar** propriedade **True**. Para excluir o índice, defina essa propriedade como **False**.  
  
 **Otimizar** é uma propriedade dinâmica anexada para o [campo](../../../ado/reference/ado-api/field-object.md) objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient**.  
  
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
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Otimizar o exemplo da propriedade (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Otimizar o exemplo da propriedade (VC + +)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Propriedade de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Localizar o método (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propriedade Sort](../../../ado/reference/ado-api/sort-property.md)

