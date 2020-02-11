---
title: Usando mensagens | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ff94bf10dee2bda0a61b573b87621fa5d3256b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72781796"
---
# <a name="using-messages"></a>Usando mensagens
  No SMO, mensagens do sistema são representadas pelo objeto <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> que pertence ao objeto `Server`. Como as mensagens do sistema não podem ser modificadas, as propriedades do objeto `SystemMessage` são somente leitura.  
  
 Mensagens definidas pelo usuário são representadas programaticamente no SMO pelo objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection>. Mensagens existentes, definidas pelo usuário, podem ser descobertas através da iteração pela coleção. Para gerar novas mensagens definidas pelo usuário, você pode criar uma instância de um novo objeto `UserDefinedMessage` e definir as propriedades adequadas.  
  
## <a name="examples"></a>Exemplos  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>Localizando uma mensagem de sistema específica no Visual Basic .NET  
 O exemplo de código mostra como identificar uma mensagem de sistema através do número de identificação e como exibir a mensagem.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMessages1](SMO How to#SMO_VBMessages1)]  -->  
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>Localizando uma mensagem do sistema específica no Visual Basic C#  
 O exemplo de código mostra como identificar uma mensagem de sistema através do número de identificação e como exibir a mensagem.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference an existing system message using the   
            //ItemByIdAndLanguage method.   
            SystemMessage msg = default(SystemMessage);  
            msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
        }  
```  
  
## <a name="finding-a-particular-system-message-in-powershell"></a>Localizando uma mensagem do sistema específica no PowerShell  
 O exemplo de código mostra como identificar uma mensagem de sistema através do número de identificação e como exibir a mensagem.  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>Adicionando uma nova mensagem definida pelo usuário no Visual Basic  
 O exemplo de código demonstra como criar uma mensagem definida pelo usuário com uma identificação maior que 50000.  
  
```vb
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>Adicionando uma nova mensagem definida pelo usuário no Visual Basic C#  
 O exemplo de código demonstra como criar uma mensagem definida pelo usuário com uma identificação maior que 50000.  
  
```csharp
{
            Server mysrv = new Server();  
  
            UserDefinedMessage udm = new UserDefinedMessage(mysrv, 50030, "us_english",16, "Test message");  
            udm.Create();  
             UserDefinedMessage  msg = mysrv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
  
        }  
```  
  
## <a name="adding-a-new-user-defined-message-in-powershell"></a>Adicionando uma nova mensagem definida pelo usuário no PowerShell
 O exemplo de código demonstra como criar uma mensagem definida pelo usuário com uma identificação maior que 50000.  
  
```powershell
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -ArgumentList `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
