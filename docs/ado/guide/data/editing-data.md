---
title: Editando dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e8fd90849b8e046a7f4fe5d158d4594e612c91f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925499"
---
# <a name="editing-data"></a>Editar dados
Explicamos como usar o ADO para se conectar a uma fonte de dados, executar um comando, obter os resultados em um objeto **Recordset** e navegar no **conjunto de registros**. Esta seção se concentra na próxima operação de ADO fundamental: editando dados.  
  
 Esta seção continua a usar o **conjunto de registros** de exemplo introduzidos no [exame de dados](../../../ado/guide/data/examining-data.md), com uma alteração importante. O código a seguir é usado para abrir o **conjunto de registros**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 A alteração importante no código envolve a definição da propriedade **CursorLocation** do objeto de **conexão** igual a **adUseClient** na função *GetNewConnection* (mostrada no próximo exemplo), que indica o uso de um cursor do cliente. Para obter mais informações sobre as diferenças entre cursores do lado do cliente e do servidor, consulte [noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 A configuração **adUseClient** da propriedade **CursorLocation** move o local do cursor da fonte de dados (o SQL Server, nesse caso) para o local do código do cliente (a estação de trabalho desktop). Essa configuração força o ADO a invocar o mecanismo de cursor do cliente para OLE DB no cliente a fim de criar e gerenciar o cursor.  
  
 Você também pode ter notado que o parâmetro **LockType** do método **Open** foi alterado para **adLockBatchOptimistic**. Isso abre o cursor no modo de lote. (O provedor armazena em cache várias alterações e as grava na fonte de dados subjacente somente quando você chama o método **UpdateBatch** .) As alterações feitas no conjunto de **registros** não serão atualizadas no banco de dados até que o método **UpdateBatch** seja chamado.  
  
 Por fim, o código nesta seção usa uma versão modificada da função GetNewConnection. Esta versão da função agora retorna um cursor do lado do cliente. A função é parecida com esta:  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Editar registros existentes](../../../ado/guide/data/editing-existing-records.md)  
  
-   [Adicionando registros](../../../ado/guide/data/adding-records.md)  
  
-   [Determinar o que é compatível](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Excluir registros usando o método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [Alternativas: usar instruções SQL](../../../ado/guide/data/alternatives-using-sql-statements.md)
