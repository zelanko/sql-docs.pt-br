---
description: Exemplo dos métodos Save e Open (VB)
title: Exemplo dos métodos Save e Open (VB) | Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: rothja
ms.author: jroth
ms.openlocfilehash: 048fbb83c8a6b9de150642f6094a1f07e0c1e11e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442218"
---
# <a name="save-and-open-methods-example-vb"></a>Exemplo dos métodos Save e Open (VB)
Esses três exemplos demonstram como os métodos [Save](../../../ado/reference/ado-api/save-method.md) e [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) podem ser usados juntos.  
  
 Suponha que você esteja passando por uma viagem de negócios e queira levar uma tabela de um banco de dados. Antes de começar, você acessa os dados como um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) e salva-os em um formulário transportável. Ao chegar ao seu destino, você acessa o **conjunto** de registros como um conjunto de **registros**local e desconectado. Faça alterações no conjunto de **registros**e salve-o novamente. Por fim, ao retornar Home, você se conecta ao banco de dados novamente e o atualiza com as alterações feitas em trânsito.  
  
 Primeiro, acesse e salve a tabela ***autores*** .  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 Neste ponto, você chegou ao seu destino. Você acessará a tabela ***autores*** como um conjunto de **registros**local e desconectado. Você deve ter o provedor **MSPersist** no computador que está usando para acessar o arquivo salvo, a:\Pubs.xml.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Por fim, você retorna a página inicial. Agora, atualize o banco de dados com suas alterações.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Mais sobre persistência de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
