---
title: Exemplo da propriedade status (campo) (VB) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ea3ebba271ebdc12802b31cc1f50cdd3befead0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="status-property-example-field-vb"></a>Exemplo da propriedade status (campo) (VB)
O exemplo a seguir abre um documento de uma pasta de leitura/gravação usando o [Internet Publishing Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). O [Status](../../../ado/reference/ado-api/status-property-ado-field.md) propriedade de um [campo](../../../ado/reference/ado-api/field-object.md) objeto do [registro](../../../ado/reference/ado-api/record-object-ado.md) primeiro ser definida como **adFieldPendingInsert**, e ser atualizado para **adFieldOk**.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=http://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 O exemplo a seguir exclui um conhecido **campo** de um **registro** aberto a partir de um documento. O **Status** propriedade ser definida primeiro como **adFieldOK**, em seguida, **adFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 O código a seguir exclui um **campo** de um **registro** aberto em um documento somente leitura. **Status** será definida como **adFieldPendingDelete**. Em [atualização](../../../ado/reference/ado-api/update-method.md), a exclusão falhará e **Status** será **adFieldPendingDelete** mais **adFieldPermissionDenied**. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) limpa o pendente **Status** configuração.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Propriedade Status (campo ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
