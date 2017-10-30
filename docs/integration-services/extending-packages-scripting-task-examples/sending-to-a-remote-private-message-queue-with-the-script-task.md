---
title: Enviando a uma fila de mensagens particular remota com a tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5ab9314ef0825486914d1801bfa2b9613883b43e
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>Enviando a uma fila de mensagens particular remota com a tarefa Script
  O serviço de enfileiramento de mensagens (também conhecido como MSMQ) facilita a comunicação rápida e confiável de desenvolvedores com programas aplicativos, enviando e recebendo mensagens. Uma fila de mensagens pode estar localizada no computador local ou em um computador remoto, e pode ser pública ou particular. No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o gerenciador de conexões do MSMQ e a tarefa Fila de Mensagens não dão suporte ao envio para uma fila privada em um computador remoto. Porém, a tarefa Script facilita o envio de uma mensagem a uma fila particular remota.  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 O exemplo a seguir usa um Gerenciador de conexão de MSMQ existente, junto com objetos e métodos do namespace System. Messaging, para enviar o texto contido em uma variável de pacote a uma fila de mensagens particular remota. A chamada para o método M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) do Gerenciador de conexão do MSMQ retorna um **MessageQueue** do objeto cuja **enviar** método realiza essa tarefa.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Crie um gerenciador de conexões do MSMQ com o nome padrão. Defina o caminho de uma fila particular remota válida no seguinte formato:  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  Criar um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] variável chamada **MessageText** do tipo **cadeia de caracteres** para passar o texto da mensagem para o script. Digite uma mensagem padrão como o valor da variável.  
  
3.  Adicione uma tarefa Script à superfície de design e edite-a. No **Script** guia do **Editor da tarefa Script**, adicione o `MessageText` variável para o **ReadOnlyVariables** propriedade para disponibilizar a variável dentro do script .  
  
4.  Clique em **Editar Script** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ferramentas para o editor de script Applications (VSTA).  
  
5.  Adicione uma referência no projeto de script para o **Messaging** namespace.  
  
6.  Substitua o conteúdo da janela de script pelo código da seção a seguir.  
  
## <a name="code"></a>Código  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Fila de Mensagens](../../integration-services/control-flow/message-queue-task.md)  
  
  

