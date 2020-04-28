---
title: Erros do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c357384a3de683c05b2922149e2b61630881922
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926207"
---
# <a name="ado-run-time-errors"></a>Erros de tempo de execução do ADO
Os erros do ADO são relatados para seu programa como erros de tempo de execução. Você pode usar o mecanismo de interceptação de erros da sua linguagem de programação para interceptar e tratá-los. Por exemplo, em Visual Basic, use a instrução **On Error** . Em Visual C++, depende do método que você está usando para acessar as bibliotecas do ADO. Com #import, use um bloco **try-catch** . Caso contrário, os programadores do C++ precisam recuperar explicitamente o objeto de erro chamando **GetErrorInfo**. O procedimento a seguir Visual Basic sub demonstra o trapping de um erro ADO:

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 Esse **Form_Load** procedimento de evento cria intencionalmente um erro tentando abrir o mesmo objeto de **conexão** duas vezes. Na segunda vez que o método **Open** é chamado, o manipulador de erro é ativado. Nesse caso, o erro é do tipo **adErrObjectOpen**, portanto, o manipulador de erros exibe a seguinte mensagem antes de continuar a execução do programa:

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 A mensagem de erro inclui cada informação fornecida pelo objeto Visual Basic **Err** , exceto pelo valor **LastDllError** , que não se aplica aqui. O número do erro informa qual erro ocorreu. A descrição é útil em casos em que você não deseja manipular o erro por conta própria. Você pode simplesmente passá-lo ao usuário. Embora você geralmente queira usar mensagens personalizadas para seu aplicativo, não é possível prever todos os erros; a descrição dá algum indício sobre o que deu errado. No código de exemplo, o erro foi relatado pelo objeto de **conexão** . Você verá o tipo ou a ID programática do objeto aqui-não é um nome de variável.

> [!NOTE]
>  O objeto Visual Basic **Err** contém apenas informações sobre o erro mais recente. A coleção de **erros** ADO do objeto de **conexão** contém um objeto de **erro** para cada erro gerado pela operação ADO mais recente. Use a coleção de **erros** em vez do objeto **Err** para lidar com vários erros. Para obter mais informações sobre a coleção de **erros** , consulte [erros do provedor](../../../ado/guide/data/provider-errors.md). No entanto, se não houver um objeto de **conexão** válido, o objeto **Err** será a única fonte para obter informações sobre erros do ADO.

 Que tipos de operações provavelmente causarão erros do ADO? Os erros comuns do ADO podem envolver a abertura de um objeto, como uma **conexão** ou **conjunto de registros**, a tentativa de atualizar dados ou a chamada de um método ou propriedade que não tem suporte no seu provedor.

 OLE DB erros também podem ser passados para seu aplicativo como erros em tempo de execução na coleção de **erros** .

 O tópico a seguir fornece mais informações sobre erros do ADO.

-   [Referência de erros ADO](../../../ado/guide/data/ado-error-reference.md)
