---
title: Usando o Database Mail | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7ddfd4155b0dfe0a5b624935c79098fb82ed0ea
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="using-database-mail"></a>Usando o Database Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]No SMO, o subsistema Database Mail é representado pelo <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> que é referenciado pelo objeto de <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> propriedade. Através do objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> do SMO, você pode configurar o subsistema Database Mail e gerenciar perfis e contas de email. O SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> objeto pertence a **Server** objeto, o que significa que o escopo das contas de email está no nível do servidor.  
  
## <a name="examples"></a>Exemplos  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C &#35; Projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Para programas que usam [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Database Mail, você deve incluir o **Imports** instrução para qualificar o namespace do Mail. Insira a instrução após outras instruções **Imports** , antes de qualquer declaração no aplicativo, como:  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Criando uma conta de email de banco de dados usando o Visual Basic  
 Este exemplo de código mostra como criar uma conta de email no SMO. O Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O SMO pode ser usado para configurar programaticamente o Database Mail, mas não pode ser usado para enviar ou tratar emails recebidos.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Define the Database Mail service with a SqlMail object variable and reference it using the Server Mail property.
Dim sm As SqlMail
sm = srv.Mail
'Define and create a mail account by supplying the Database Mail service, name, description, display name, and email address arguments in the constructor.
Dim a As MailAccount
a = New MailAccount(sm, "AdventureWorks Administrator", "AdventureWorks Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com")
a.Create()
```
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Criando uma conta de email de banco de dados usando o Visual C#  
 Este exemplo de código mostra como criar uma conta de email no SMO. O Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O SMO pode ser usado para configurar programaticamente o Database Mail, mas não pode ser usado para enviar ou tratar emails recebidos.  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>Criando uma conta de email de banco de dados usando o PowerShell  
 Este exemplo de código mostra como criar uma conta de email no SMO. O Database Mail é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> e referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. O SMO pode ser usado para configurar programaticamente o Database Mail, mas não pode ser usado para enviar ou tratar emails recebidos.  
  
  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
