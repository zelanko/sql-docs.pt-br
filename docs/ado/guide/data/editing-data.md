---
title: Editando dados | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a5921185f6643f328559e3bc73dfac46bfee0c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="editing-data"></a>Editando dados
Ter explicamos como usar o ADO para se conectar a uma fonte de dados, executar um comando, obter os resultados em um **Recordset** objeto e, em seguida, navegar dentro a **Recordset**. Esta seção aborda a próxima operação ADO fundamental: edição de dados.  
  
 Esta seção continua a usar o exemplo **registros** introduzido no [examinando dados](../../../ado/guide/data/examining-data.md), com uma alteração importante. O código a seguir é usado para abrir o **registros**:  
  
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
  
 A alteração importante para o código envolve a configuração de **CursorLocation** propriedade do **Conexão** objeto igual a **adUseClient** no  *GetNewConnection* função (mostrada no exemplo a seguir), que indica o uso de um cursor do cliente. Para obter mais informações sobre as diferenças entre os cursores do lado do cliente e do servidor, consulte [Noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 O **CursorLocation** da propriedade **adUseClient** configuração move o local do cursor da fonte de dados (o SQL Server, neste caso) para o local do código de cliente (a estação de trabalho da área de trabalho). Essa configuração força o ADO para invocar o mecanismo de Cursor do cliente para OLE DB no cliente para criar e gerenciar o cursor.  
  
 Você também deve ter notado que o **LockType** parâmetro o **abrir** método alterado para **adLockBatchOptimistic**. Isso abre o cursor no modo de lote. (O provedor armazena em cache várias alterações e grava a fonte de dados somente quando você chamar o **UpdateBatch** método.) As alterações feitas a **Recordset** não serão atualizadas no banco de dados até que o **UpdateBatch** método é chamado.  
  
 Por fim, o código nesta seção usa uma versão modificada da função GetNewConnection. Esta versão da função agora retorna um cursor do lado do cliente. A função tem esta aparência:  
  
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
  
 Esta seção contém os tópicos a seguir.  
  
-   [Editando registros existentes](../../../ado/guide/data/editing-existing-records.md)  
  
-   [Adicionando registros](../../../ado/guide/data/adding-records.md)  
  
-   [Determinando o que tem suporte](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Excluindo registros usando o método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [Alternativas: usando instruções SQL](../../../ado/guide/data/alternatives-using-sql-statements.md)

