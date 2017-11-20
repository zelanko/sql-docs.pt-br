---
title: Enviando uma mensagem de email HTML com a tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b5f50a79ca83243ea130c77a0d95ab402ba2d31a
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>Enviando uma mensagem de email HTML com a tarefa Script
  A tarefa SendMail do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oferece suporte apenas a mensagens de email em formato de texto sem formatação. Porém, você pode enviar mensagens de email HTML facilmente usando a tarefa Script e as capacidades de email do .NET Framework.  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 O exemplo a seguir usa o **mail** namespace para configurar e enviar uma mensagem de email HTML. O script obtém o para, de, assunto e corpo do email de variáveis de pacote, usa-os para criar um novo **MailMessag**e define seu **IsBodyHtml** propriedade **True**. Em seguida, ele obtém o nome do servidor SMTP de outra variável de pacote, inicializa uma instância de **SmtpClient**e chama seu **enviar** método para enviar a mensagem HTML. O exemplo encapsula a funcionalidade de envio da mensagem em uma sub-rotina que pode ser reutilizada em outros scripts.  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>Para configurar este exemplo de tarefa Script sem um gerenciador de conexões SMTP  
  
1.  Crie variáveis de cadeia de caracteres denominadas `HtmlEmailTo`, `HtmlEmailFrom` e `HtmlEmailSubject` e atribua a elas valores apropriados para uma mensagem de teste válida.  
  
2.  Crie uma variável String denominada `HtmlEmailBody` e atribua a ela uma cadeia de caracteres de marcação HTML. Por exemplo:  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  Crie uma variável de cadeia de caracteres denominada `HtmlEmailServer` e atribua o nome de um servidor SMTP disponível que aceite mensagens de saída anônimas.  
  
4.  Atribua todas as cinco dessas variáveis para o **ReadOnlyVariables** propriedade de uma nova tarefa de Script.  
  
5.  Importar o **System.Net** e **mail** namespaces em seu código.  
  
 O código de exemplo neste tópico obtém o nome do servidor SMTP de uma variável do pacote. Contudo, você também pode tirar proveito de um gerenciador de conexões SMTP para encapsular as informações da conexão e extrair o nome do servidor do gerenciador de conexões em seu código. O método <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> do gerenciador de conexões SMTP retorna uma cadeia de caracteres no formato seguinte:  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 Você pode usar o **Split** método para separar essa lista de argumentos em uma matriz de cadeias de caracteres individuais em cada ponto e vírgula (;) ou igual a entre (=) e, em seguida, extrair o segundo argumento (subscript 1) da matriz como o nome do servidor.  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>Para configurar este exemplo de tarefa Script com um gerenciador de conexões SMTP  
  
1.  Modificar a tarefa Script configurada anteriormente removendo a `HtmlEmailServer` variável na lista de **ReadOnlyVariables**.  
  
2.  Substitua a linha do código que obtém o nome do servidor:  
  
    ```  
    Dim smtpServer As String = _  
      Dts.Variables("HtmlEmailServer").Value.ToString  
    ```  
  
     pelas seguintes linhas:  
  
    ```  
    Dim smtpConnectionString As String = _  
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)  
    Dim smtpServer As String = _  
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)  
    ```  
  
## <a name="code"></a>Código  
  
```vb  
Public Sub Main()  
  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageTo, htmlMessageFrom, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal SendTo As String, ByVal From As String, _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    SendTo, From, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(SendTo, From, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa enviar email](../../integration-services/control-flow/send-mail-task.md)  
  
  

