---
title: Salvar e abrir um exemplo dos métodos (VB) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 32ed7e6240f5f9622bfcb80e2f05a633fcaf2fdc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711639"
---
# <a name="save-and-open-methods-example-vb"></a>Exemplo dos métodos Save e Open (VB)
Esses três exemplos demonstram como o [salve](../../../ado/reference/ado-api/save-method.md) e [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos podem ser usados juntos.  
  
 Suponha que você está saindo de uma viagem de negócios e deseja levar ao longo de uma tabela de banco de dados. Antes de entrar, você acessa os dados como uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) e salve-o em um formulário transportável. Quando você chega ao seu destino, você acessa o **conjunto de registros** como um local, desconectado **conjunto de registros**. Fazer alterações para o **Recordset**e, em seguida, salve-o novamente. Finalmente, quando você voltar ao início, conecte-se novamente ao banco de dados e atualizá-lo com as alterações feitas em trânsito.  
  
 Primeiro, acessar e salvar a ***autores*** tabela.  
  
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
  
 Neste ponto, você chegou ao seu destino. Você acessará o ***autores*** tabela como um local, desconectado **conjunto de registros**. Você deve ter o **MSPersist** provedor no computador que você está usando para acessar o arquivo salvo, a:\Pubs.xml.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Finalmente, retornar para casa. Agora, atualize o banco de dados com suas alterações.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Mais sobre a persistência do conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
