---
title: Erros de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a36f5b96ac0c04b6315ba5a135bbab0dbe75df2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ado-run-time-errors"></a>Erros de tempo de execução de ADO
São relatados erros de ADO para o seu programa como erros de tempo de execução. Você pode usar o mecanismo de interceptação de erro da linguagem de programação para interceptar e tratá-los. Por exemplo, no Visual Basic, utilize o **On Error** instrução. No Visual C++, ele depende do método que você está usando para acessar as bibliotecas do ADO. Com #import, use um **de try-catch** bloco. Caso contrário, os programadores do C++ precisará recuperar explicitamente o objeto de erro chamando **GetErrorInfo**. O seguinte procedimento sub Visual Basic demonstra a interceptação de erro de ADO:

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

 Isso **Form_Load** procedimento de evento intencionalmente gera um erro ao tentar abrir o mesmo **Conexão** objeto duas vezes. Na segunda vez que o **abrir** método é chamado, o manipulador de erros é ativado. Nesse caso, o erro é do tipo **adErrObjectOpen**, portanto, o manipulador de erros exibe a mensagem a seguir antes de continuar a execução do programa:

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 A mensagem de erro inclui cada parte das informações fornecidas pelo Visual Basic **Err** objeto exceto para o **LastDLLError** valor, que não se aplicam aqui. O número do erro informa o erro ocorrido. A descrição é útil em casos em que você não deseja tratar o erro por conta própria. Você pode simplesmente passá-lo ao longo para o usuário. Embora geralmente você desejará usar mensagens personalizadas para seu aplicativo, você não pode prever cada erro. a descrição fornece alguma indicação sobre o que deu errado. No código de exemplo, o erro foi relatado pelo **Conexão** objeto. Você verá o tipo do objeto ou o ID programática aqui, não um nome de variável.

> [!NOTE]
>  O Visual Basic **Err** objeto contém apenas informações sobre o erro mais recente. O ADO **erros** coleção do **Conexão** objeto contém um **erro** objeto para cada erro gerado pela operação mais recente do ADO. Use o **erros** coleção em vez de **Err** objeto para manipular vários erros. Para obter mais informações sobre o **erros** coleta, consulte [erros do provedor](../../../ado/guide/data/provider-errors.md). No entanto, se não houver não válido **Conexão** objeto, o **Err** objeto é a única fonte para obter informações sobre erros de ADO.

 Que tipos de operações são prováveis que causam erros de ADO? Erros comuns de ADO podem envolver a abertura de um objeto, como um **Conexão** ou **registros**, a tentativa de atualizar dados ou chamar um método ou propriedade que não é suportada pelo provedor.

 Erros de OLE DB também podem ser passados para o seu aplicativo como erros de tempo de execução no **erros** coleção.

 O tópico a seguir fornece mais informações sobre erros de ADO.

-   [Referência de erros ADO](../../../ado/guide/data/ado-error-reference.md)
