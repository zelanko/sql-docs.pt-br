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
manager: craigg
ms.openlocfilehash: 0c12692a6ebd1467148b52f993a77043ff495d43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161779"
---
# <a name="editing-data"></a>Editar dados
Ter explicamos como usar o ADO para conectar a uma fonte de dados, executar um comando, obter os resultados um **conjunto de registros** do objeto e navegar no **conjunto de registros**. Esta seção se concentra na próxima operação ADO fundamental: edição de dados.  
  
 Esta seção continua a usar a amostra **conjunto de registros** introduzido no [examinando dados](../../../ado/guide/data/examining-data.md), com uma alteração importante. O código a seguir é usado para abrir o **Recordset**:  
  
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
  
 A alteração importante no código envolve a configuração de **CursorLocation** propriedade da **Conexão** igual do objeto **adUseClient** no  *GetNewConnection* função (mostrada no exemplo a seguir), que indica o uso de um cursor do cliente. Para obter mais informações sobre as diferenças entre os cursores do lado do cliente e servidor, consulte [Noções básicas sobre cursores e bloqueios](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 O **CursorLocation** da propriedade **adUseClient** configuração move a posição do cursor da fonte de dados (o SQL Server, neste caso) para o local do código do cliente (a área de trabalho da estação de trabalho). Essa configuração força o ADO para invocar o mecanismo de Cursor do cliente para OLE DB no cliente para criar e gerenciar o cursor.  
  
 Você também deve ter notado que o **LockType** parâmetro do **abra** método alterado para **adLockBatchOptimistic**. Isso abre o cursor no modo de lote. (O provedor armazena em cache várias alterações e grava-os à fonte de dados subjacente, somente quando você chama o **UpdateBatch** método.) As alterações que foram feitas para o **conjunto de registros** não será atualizada no banco de dados até que o **UpdateBatch** método é chamado.  
  
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
  
-   [Alternativas: Usando instruções SQL](../../../ado/guide/data/alternatives-using-sql-statements.md)
