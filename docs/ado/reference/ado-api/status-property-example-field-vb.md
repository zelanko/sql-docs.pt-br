---
title: Exemplo da propriedade status (campo) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caf016190e585aa64ee24f81fdcc0c18a4dab93f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027588"
---
# <a name="status-property-example-field-vb"></a>Exemplo da propriedade Status (Campo) (VB)
O exemplo a seguir abre um documento de uma pasta de leitura/gravação usando o [Internet Publishing Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). O [Status](../../../ado/reference/ado-api/status-property-ado-field.md) propriedade de uma [campo](../../../ado/reference/ado-api/field-object.md) objeto do [registro](../../../ado/reference/ado-api/record-object-ado.md) primeiro será definido como **adFieldPendingInsert**, e em seguida, ser atualizado para **adFieldOk**.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
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
  
 O exemplo a seguir exclui um conhecido **campo** de uma **registro** aberto a partir de um documento. O **Status** propriedade ser definida primeiro como **adFieldOK**, em seguida, **adFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 O código a seguir exclui um **campo** de uma **registro** aberto em um documento somente leitura. **Status** será definido como **adFieldPendingDelete**. No [atualização](../../../ado/reference/ado-api/update-method.md), a exclusão falhará e **Status** estará **adFieldPendingDelete** plus **adFieldPermissionDenied**. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) limpa o pendente **Status** configuração.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Propriedade Status (campo ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
