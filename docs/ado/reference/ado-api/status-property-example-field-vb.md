---
description: Exemplo da propriedade Status (Campo) (VB)
title: Exemplo da propriedade Status (campo) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 23a6ebaa724e06ce4a8283b95e3d7a982c8deef1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988687"
---
# <a name="status-property-example-field-vb"></a>Exemplo da propriedade Status (Campo) (VB)
O exemplo a seguir abre um documento de uma pasta de leitura/gravação usando o [provedor de publicação da Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). A propriedade [status](./status-property-ado-field.md) de um [objeto Field](./field-object.md) do [registro](./record-object-ado.md) será definida primeiro como **adFieldPendingInsert**e, em seguida, será atualizada para **adFieldOk**.  
  
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
  
 O exemplo a seguir exclui um **campo** conhecido de um **registro** aberto de um documento. A propriedade **status** será definida primeiro como **AdFieldOK**, então **adFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 O código a seguir exclui um **campo** de um **registro** aberto em um documento somente leitura. O **status** será definido como **adFieldPendingDelete**. Na [atualização](./update-method.md), a exclusão falhará e o **status** será **adFieldPendingDelete** mais **adFieldPermissionDenied**. [CancelUpdate](./cancelupdate-method-ado.md) limpa a configuração de **status** pendente.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Field](./field-object.md)   
 [Objeto Record (ADO)](./record-object-ado.md)   
 [Propriedade Status (campo ADO)](./status-property-ado-field.md)