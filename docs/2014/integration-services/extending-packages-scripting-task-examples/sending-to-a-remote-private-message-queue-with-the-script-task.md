---
title: Enviar a uma fila de mensagens particular remota com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a9f9c07d52fe1920c65c1f758a0e86c13037945a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352907"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>Enviando a uma fila de mensagens particular remota com a tarefa Script
  O serviço de enfileiramento de mensagens (também conhecido como MSMQ) facilita a comunicação rápida e confiável de desenvolvedores com programas aplicativos, enviando e recebendo mensagens. Uma fila de mensagens pode estar localizada no computador local ou em um computador remoto, e pode ser pública ou particular. No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o gerenciador de conexões do MSMQ e a tarefa Fila de Mensagens não dão suporte ao envio para uma fila privada em um computador remoto. Porém, a tarefa Script facilita o envio de uma mensagem a uma fila particular remota.  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrição  
 O exemplo a seguir usa um gerenciador de conexões MSMQ existente, junto com objetos e métodos do namespace System.Messaging, para enviar o texto contido em uma variável de pacote a uma fila de mensagens particular remota. A chamada ao método m:Microsoft.SQLServer.DTS.managedconnections.msmqconn.acquireconnection do Gerenciador de conexão do MSMQ retorna um **MessageQueue** do objeto cuja `Send` método realiza isso tarefa.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Crie um gerenciador de conexões do MSMQ com o nome padrão. Defina o caminho de uma fila particular remota válida no seguinte formato:  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  Criar uma [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] variável nomeada **MessageText** do tipo `String` para passar o texto da mensagem para o script. Digite uma mensagem padrão como o valor da variável.  
  
3.  Adicione uma tarefa Script à superfície de design e edite-a. Na guia **Script** do **Editor da Tarefa Script**, adicione a variável `MessageText` à propriedade **ReadOnlyVariables** para disponibilizar a variável dentro do script.  
  
4.  Clique em **Editar Script** para abrir o editor de script VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications).  
  
5.  Adicione uma referência do projeto de script ao namespace `System.Messaging`.  
  
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
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Fila de Mensagens](../control-flow/message-queue-task.md)  
  
  
