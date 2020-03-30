---
title: Enviar uma mensagem de email HTML com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eb1de7efdc8592551343a9424e4ab3b1dd1f69f9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71286743"
---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>Enviando uma mensagem de email HTML com a tarefa Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa SendMail do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oferece suporte apenas a mensagens de email em formato de texto sem formatação. Porém, você pode enviar mensagens de email HTML facilmente usando a tarefa Script e as capacidades de email do .NET Framework.  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>DESCRIÇÃO  
 O exemplo a seguir usa o namespace **System.Net.Mail** para configurar e enviar uma mensagem de email HTML. O script obtém o Para, o De, o Assunto e o corpo do email das variáveis do pacote, usa-os para criar uma nova **MailMessage** e define sua propriedade **IsBodyHtml** para **True**. Em seguida, ele obtém o nome do servidor SMTP de uma outra variável do pacote, inicializa uma instância do **System.Net.Mail.SmtpClient** e chama seu método **Send** para enviar a mensagem HTML. O exemplo encapsula a funcionalidade de envio da mensagem em uma sub-rotina que pode ser reutilizada em outros scripts.  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>Para configurar este exemplo de tarefa Script sem um gerenciador de conexões SMTP  
  
1.  Crie variáveis de cadeia de caracteres denominadas `HtmlEmailTo`, `HtmlEmailFrom` e `HtmlEmailSubject` e atribua a elas valores apropriados para uma mensagem de teste válida.  
  
2.  Crie uma variável String denominada `HtmlEmailBody` e atribua a ela uma cadeia de caracteres de marcação HTML. Por exemplo:  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  Crie uma variável de cadeia de caracteres denominada `HtmlEmailServer` e atribua o nome de um servidor SMTP disponível que aceite mensagens de saída anônimas.  
  
4.  Atribua todas as cinco variáveis à propriedade **ReadOnlyVariables** de uma nova tarefa Script.  
  
5.  Importe os namespaces **System.Net** e **System.Net.Mail** em seu código.  
  
 O código de exemplo neste tópico obtém o nome do servidor SMTP de uma variável do pacote. Contudo, você também pode tirar proveito de um gerenciador de conexões SMTP para encapsular as informações da conexão e extrair o nome do servidor do gerenciador de conexões em seu código. O método <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> do gerenciador de conexões SMTP retorna uma cadeia de caracteres no formato seguinte:  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 Você pode usar o método **String.Split** para separar essa lista de argumentos em uma matriz de cadeias de caracteres individuais a cada ponto-e-vírgula (;) ou sinal de igual (=) e, em seguida, extrair o segundo argumento (subscript 1) da matriz como o nome do servidor.  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>Para configurar este exemplo de tarefa Script com um gerenciador de conexões SMTP  
  
1.  Modifique a tarefa Script configurada anteriormente removendo a variável `HtmlEmailServer` da lista de **ReadOnlyVariables**.  
  
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
  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageFrom, htmlMessageTo, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal From As String, ByVal SendTo As String,  _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    From, SendTo, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageFrom, htmlMessageTo, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string From, string SendTo, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(From, SendTo, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa Enviar Email](../../integration-services/control-flow/send-mail-task.md)  
  
  
