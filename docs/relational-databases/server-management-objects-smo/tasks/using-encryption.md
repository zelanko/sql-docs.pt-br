---
title: Usando a criptografia | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad74e5242702ace386fb8c14a034a56886f27191
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="using-encryption"></a>Usando a criptografia
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No SMO, a chave mestra de serviço é representada pelo <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> objeto. Isso é referenciado pelo <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> propriedade o <xref:Microsoft.SqlServer.Management.Smo.Server> objeto. Ele pode ser regenerado usando o <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> método.  
  
 A chave mestra de banco de dados é representada pelo <xref:Microsoft.SqlServer.Management.Smo.MasterKey> objeto. O <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> propriedade indica se a chave mestra de banco de dados é criptografada pela chave mestra de serviço. A cópia criptografada no banco de dados mestre é atualizada automaticamente sempre que a chave mestra do banco de dados é alterada.  
  
 É possível descartar a criptografia de chave de serviço usando o <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> método e criptografar a chave mestra de banco de dados com uma senha. Nessa situação, você precisará abrir a chave mestra do banco de dados explicitamente para poder acessar chaves privadas protegidas.  
  
 Quando um banco de dados está sendo anexado a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve fornecer a senha para a chave mestra de banco de dados ou executar o <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> método para fazer uma cópia não criptografada da chave mestra de banco de dados disponíveis para a criptografia com o serviço chave mestra. Essa etapa é recomendada para evitar a necessidade de abrir a chave mestra do banco de dados explicitamente.  
  
 O <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> método regenera a chave mestra de banco de dados. Quando a chave mestra do banco de dados é regenerada, todas as chaves criptografadas com a chave mestra do banco de dados são descriptografadas e, depois, criptografadas com a nova chave mestra do banco de dados. O <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> método remove a criptografia da chave mestra de banco de dados pela chave mestra de serviço. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> faz com que uma cópia da chave mestra seja criptografada usando a chave mestra de serviço e armazenada no banco de dados atual e no banco de dados mestre.  
  
 No SMO, certificados são representados pelo <xref:Microsoft.SqlServer.Management.Smo.Certificate> objeto. O <xref:Microsoft.SqlServer.Management.Smo.Certificate> objeto tem propriedades que especificam a chave pública, o nome do assunto, o período de validade e informações sobre o emissor. A permissão para acessar o certificado é controlada através dos métodos **Grant**, **Revoke** e **Deny** .  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um Visual C &#35; Projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-a-certificate-in-visual-c"></a>Adicionando um certificado no Visual Basic C#  
 O exemplo de código cria um certificado simples com uma senha de criptografia. Ao contrário de outros objetos, o <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> método tem várias sobrecargas. A sobrecarga usada no exemplo cria um novo certificado com uma senha de criptografia.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>Adicionando um certificado no PowerShell  
 O exemplo de código cria um certificado simples com uma senha de criptografia. Ao contrário de outros objetos, o <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> método tem várias sobrecargas. A sobrecarga usada no exemplo cria um novo certificado com uma senha de criptografia.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate  
  
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -argumentlist $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usando chaves de criptografia](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
