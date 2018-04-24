---
title: Exemplo da propriedade Version (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Version property [ADO], Visual Basic example
ms.assetid: 708efd50-2905-4168-b7e4-91b2e9b23539
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5fddbf0c3ad6370bf6d15801a5cb21f2655700e0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="version-property-example-vb"></a>Exemplo da propriedade Version (VB)
Este exemplo usa o [versão](../../../ado/reference/ado-api/version-property-ado.md) propriedade de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto para exibir a versão atual do ADO. Ele também usa várias propriedades dinâmicas para mostrar:  
  
-   o nome do DBMS atual e a versão.  
  
-   Versão do OLE DB.  
  
-   Nome do provedor e a versão.  
  
-   Versão do ODBC.  
  
-   Nome do driver ODBC e versão.  
  
```  
'BeginVersionVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strVersionInfo As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    strVersionInfo = "ADO Version: " & Cnxn.Version & vbCr  
    strVersionInfo = strVersionInfo & "DBMS Name: " & Cnxn.Properties("DBMS Name") & vbCr  
    strVersionInfo = strVersionInfo & "DBMS Version: " & Cnxn.Properties("DBMS Version") & vbCr  
    strVersionInfo = strVersionInfo & "OLE DB Version: " & Cnxn.Properties("OLE DB Version") & vbCr  
    strVersionInfo = strVersionInfo & "Provider Name: " & Cnxn.Properties("Provider Name") & vbCr  
    strVersionInfo = strVersionInfo & "Provider Version: " & Cnxn.Properties("Provider Version") & vbCr  
  
    MsgBox strVersionInfo  
  
    ' clean up  
    Cnxn.Close  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndVersionVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade Version (ADO)](../../../ado/reference/ado-api/version-property-ado.md)
