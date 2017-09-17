---
title: "Salve e abra o exemplo de métodos (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad4d79342ae4903e3469f3685210e882d64d318f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="save-and-open-methods-example-vb"></a>Salve e abra o exemplo de métodos (VB)
Esses três exemplos demonstram como o [salvar](../../../ado/reference/ado-api/save-method.md) e [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos podem ser usados juntos.  
  
 Suponha que você vai uma viagem de negócios e é executada ao longo de uma tabela de banco de dados. Antes de entrar, você acessa os dados como um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) e salvá-lo em um formulário transportável. Quando você chega ao seu destino, você acessa o **registros** como um local, desconectado **registros**. Fazer alterações para o **registros**e, em seguida, salve-o novamente. Finalmente, quando você voltar ao início, você se conectar novamente ao banco de dados e atualizá-lo com as alterações feitas em trânsito.  
  
 Primeiro, acessar e salvar o ***autores*** tabela.  
  
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
  
 Neste ponto, você chegou ao seu destino. Você vai acessar o ***autores*** tabela como um local, desconectado **registros**. Você deve ter o **MSPersist** provedor no computador que você está usando para acessar o arquivo salvo, a:\Pubs.xml.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Finalmente, retornar ao local original. Agora, atualize o banco de dados com suas alterações.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Mais informações sobre a persistência de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
