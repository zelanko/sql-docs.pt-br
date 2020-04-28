---
title: Exemplo de propriedades de conexão (VB) | Microsoft Docs
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
- ConnectionString property [ADO], Visual Basic example
- ConnectionTimeout property [ADO], Visual Basic example
- State property [ADO], Visual Basic example
ms.assetid: 4de7336a-b5ea-43f1-b750-5fa302b5b756
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d0cd34b13889ed44e32e29a058ca01d48aea1b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933474"
---
# <a name="connectionstring-connectiontimeout-and-state-properties-example-vb"></a>Exemplo das propriedades ConnectionString, ConnectionTimeout e State (VB)
Este exemplo demonstra diferentes maneiras de usar a propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) para abrir um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) . Ele também usa a propriedade [connectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md) para definir um período de tempo limite de conexão e a propriedade [State](../../../ado/reference/ado-api/state-property-ado.md) para verificar o estado das conexões. A função GetState é necessária para que este procedimento seja executado.  
  
> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.  
  
```  
'BeginConnectionStringVB  
  
    'To integrate this code replace  
    'the database, DSN or Data Source values  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn1 As ADODB.Connection  
    Dim Cnxn2 As ADODB.Connection  
    Dim Cnxn3 As ADODB.Connection  
    Dim Cnxn4 As ADODB.Connection  
  
     ' Open a connection without using a Data Source Name (DSN)  
    Set Cnxn1 = New ADODB.Connection  
    Cnxn1.ConnectionString = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn1.Open  
    MsgBox "Cnxn1 state: " & GetState(Cnxn1.State)  
  
     ' Open a connection using a DSN and ODBC tags  
     ' It is assumed that you have created DSN 'Pubs' with a user name as  
     ' 'MyUserId' and password as 'MyPassword'.  
    Set Cnxn2 = New ADODB.Connection  
    Cnxn2.ConnectionString = "Data Source='Pubs';" & _  
        "User ID='MyUserId';Password='MyPassword';"  
    Cnxn2.ConnectionTimeout = 30  
    Cnxn2.Open  
    MsgBox "Cnxn2 state: " & GetState(Cnxn2.State)  
  
     ' Open a connection using a DSN and OLE DB tags  
     ' It is assumed that you have created DSN 'Pubs1' with windows authentication.  
    Set Cnxn3 = New ADODB.Connection  
    Cnxn3.ConnectionString = "Data Source='Pubs1';"  
    Cnxn3.Open  
    MsgBox "Cnxn2 state: " & GetState(Cnxn3.State)  
  
     ' Open a connection using a DSN and individual  
     ' arguments instead of a connection string  
     ' It is assumed that you have created DSN 'Pubs' with a user name as  
     ' 'MyUserId' and password as 'MyPassword'.  
    Set Cnxn4 = New ADODB.Connection  
    Cnxn4.Open "Pubs", "MyUserId", "MyPassword"  
    MsgBox "Cnxn4 state: " & GetState(Cnxn4.State)  
  
    ' clean up  
    Cnxn1.Close  
    Cnxn2.Close  
    Cnxn3.Close  
    Cnxn4.Close  
    Set Cnxn1 = Nothing  
    Set Cnxn2 = Nothing  
    Set Cnxn3 = Nothing  
    Set Cnxn4 = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not Cnxn1 Is Nothing Then  
        If Cnxn1.State = adStateOpen Then Cnxn1.Close  
    End If  
    Set Cnxn1 = Nothing  
  
    If Not Cnxn2 Is Nothing Then  
        If Cnxn2.State = adStateOpen Then Cnxn2.Close  
    End If  
    Set Cnxn2 = Nothing  
  
    If Not Cnxn3 Is Nothing Then  
        If Cnxn3.State = adStateOpen Then Cnxn3.Close  
    End If  
    Set Cnxn3 = Nothing  
  
    If Not Cnxn4 Is Nothing Then  
        If Cnxn4.State = adStateOpen Then Cnxn4.Close  
    End If  
    Set Cnxn4 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
  
Public Function GetState(intState As Integer) As String  
  
   Select Case intState  
      Case adStateClosed  
         GetState = "adStateClosed"  
      Case adStateOpen  
         GetState = "adStateOpen"  
   End Select  
  
End Function  
'EndConnectionStringVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Propriedade ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)   
 [Propriedade State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)
