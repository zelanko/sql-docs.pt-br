---
title: Usando a criptografia | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 9045033e7158bcd2ab47f4e924a4485128f451a3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555916"
---
# <a name="using-encryption"></a>Usando a criptografia
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No SMO, a chave mestra de serviço é representada pelo <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> objeto. Isso é referenciado pela <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Server> objeto. Ele pode ser regenerado usando o <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> método.  
  
 A chave mestra de banco de dados é representada pelo <xref:Microsoft.SqlServer.Management.Smo.MasterKey> objeto. O <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> propriedade indica se a chave mestra de banco de dados é criptografada pela chave mestra de serviço. A cópia criptografada no banco de dados mestre é atualizada automaticamente sempre que a chave mestra do banco de dados é alterada.  
  
 É possível descartar a chave de criptografia de serviço usando o <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> método e criptografar a chave mestra de banco de dados com uma senha. Nessa situação, você precisará abrir a chave mestra do banco de dados explicitamente para poder acessar chaves privadas protegidas.  
  
 Quando um banco de dados estiver sendo anexado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve fornecer a senha para a chave mestra de banco de dados ou executar o <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> método para fazer uma cópia não criptografada da chave mestra do banco de dados disponível para criptografia com o serviço chave mestra. Essa etapa é recomendada para evitar a necessidade de abrir a chave mestra do banco de dados explicitamente.  
  
 O <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> método regenera a chave mestra de banco de dados. Quando a chave mestra do banco de dados é regenerada, todas as chaves criptografadas com a chave mestra do banco de dados são descriptografadas e, depois, criptografadas com a nova chave mestra do banco de dados. O <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> método remove a criptografia da chave mestra de banco de dados pela chave mestra de serviço. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> faz com que uma cópia da chave mestra seja criptografada usando a chave mestra de serviço e armazenada no banco de dados atual e no banco de dados mestre.  
  
 No SMO, certificados são representados pelo <xref:Microsoft.SqlServer.Management.Smo.Certificate> objeto. O <xref:Microsoft.SqlServer.Management.Smo.Certificate> objeto tem propriedades que especificam a chave pública, o nome do assunto, o período de validade e informações sobre o emissor. A permissão para acessar o certificado é controlada através dos métodos **Grant**, **Revoke** e **Deny** .  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto do SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
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
  
  
