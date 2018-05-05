---
title: Exemplo de propriedade CacheSize (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- CacheSize property [ADO], Visual Basic example
ms.assetid: a237ffdb-6e5b-47c6-9901-d5cdbe8625f3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41a30b36b35fbaa2c14ee2f5139b32260cf88153
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cachesize-property-example-vb"></a>Exemplo de propriedade CacheSize (VB)
Este exemplo usa o [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) para mostrar a diferença no desempenho de uma operação realizada com e sem um cache de registro de 30.  
  
```  
'BeginCacheSizeVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstRoySched As ADODB.Recordset  
    Dim strSQLSched As String  
    Dim strCnxn As String  
     'record variables  
    Dim sngStart As Single  
    Dim sngEnd As Single  
    Dim sngNoCache As Single  
    Dim sngCache As Single  
    Dim intLoop As Integer  
    Dim strTemp As String  
  
    ' Open the connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    ' Open the RoySched Table  
    Set rstRoySched = New ADODB.Recordset  
    strSQLSched = "roysched"  
    rstRoySched.Open strSQLSched, strCnxn, , , adCmdTable  
  
    ' Enumerate the Recordset object twice and  
    ' record the elapsed time  
    sngStart = Timer  
  
    For intLoop = 1 To 2  
        rstRoySched.MoveFirst  
  
        If Not rstRoySched.EOF Then  
            ' Execute a simple operation for the  
            ' performance test  
            Do  
                strTemp = rstRoySched!title_id  
                rstRoySched.MoveNext  
            Loop Until rstRoySched.EOF  
        End If  
    Next intLoop  
  
    sngEnd = Timer  
    sngNoCache = sngEnd - sngStart  
  
    ' Cache records in groups of 30 records.  
    rstRoySched.MoveFirst  
    rstRoySched.CacheSize = 30  
    sngStart = Timer  
  
    ' Enumerate the Recordset object twice and record  
    ' the elapsed time  
    For intLoop = 1 To 2  
        rstRoySched.MoveFirst  
        Do While Not rstRoySched.EOF  
            ' Execute a simple operation for the  
            ' performance test  
            strTemp = rstRoySched!title_id  
            rstRoySched.MoveNext  
        Loop  
    Next intLoop  
  
    sngEnd = Timer  
    sngCache = sngEnd - sngStart  
  
    ' Display performance results.  
    MsgBox "Caching Performance Results:" & vbCr & _  
        "   No cache: " & Format(sngNoCache, "##0.000") & " seconds" & vbCr & _  
        "   30-record cache: " & Format(sngCache, "##0.000") & " seconds"  
  
    ' clean up  
    rstRoySched.Close  
    Set rstRoySched = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstRoySched Is Nothing Then  
        If rstRoySched.State = adStateOpen Then rstRoySched.Close  
    End If  
    Set rstRoySched = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCacheSizeVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade CacheSize (ADO)](../../../ado/reference/ado-api/cachesize-property-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
