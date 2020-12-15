---
description: Usando a criptografia
title: Usando criptografia | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d5c9818d80ab7ad1eb57e108525ff5a182a01714
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475387"
---
# <a name="using-encryption"></a>Usando a criptografia
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  No SMO, a chave mestra do serviço é representada pelo objeto <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey>. Isso é referenciado pela propriedade <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. Ela pode ser regenerada através do método <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A>.  
  
 A chave mestra do banco de dados é representada pelo objeto <xref:Microsoft.SqlServer.Management.Smo.MasterKey>. A propriedade <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> indica se a chave mestra do banco de dados é criptografada ou não pela chave mestra do serviço. A cópia criptografada no banco de dados mestre é atualizada automaticamente sempre que a chave mestra do banco de dados é alterada.  
  
 É possível descartar a criptografia chave do serviço através do método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> e criptografar a chave mestra do banco de dados com uma senha. Nessa situação, você precisará abrir a chave mestra do banco de dados explicitamente para poder acessar chaves privadas protegidas.  
  
 Quando um banco de dados estiver sendo anexado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], forneça a senha para a chave mestra do banco de dados ou execute o método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> para fazer uma cópia não criptografada da chave mestra do banco de dados disponível para criptografia com a chave mestra do serviço. Essa etapa é recomendada para evitar a necessidade de abrir a chave mestra do banco de dados explicitamente.  
  
 O método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> regenera a chave mestra do banco de dados. Quando a chave mestra do banco de dados é regenerada, todas as chaves criptografadas com a chave mestra do banco de dados são descriptografadas e, depois, criptografadas com a nova chave mestra do banco de dados. O método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> remove a criptografia da chave mestra de banco de dados através da chave mestra de serviço. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> faz com que uma cópia da chave mestra seja criptografada usando a chave mestra de serviço e armazenada no banco de dados atual e no banco de dados mestre.  
  
 No SMO, certificados são representados pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Certificate>. O objeto <xref:Microsoft.SqlServer.Management.Smo.Certificate> tem propriedades que especificam a chave pública, o nome do assunto, o período de validade e informações sobre o emissor. A permissão para acessar o certificado é controlada através dos métodos **Grant**, **Revoke** e **Deny** .  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-a-certificate-in-visual-c"></a>Adicionando um certificado no Visual Basic C#  
 O exemplo de código cria um certificado simples com uma senha de criptografia. Diferente de outros objetos, o método <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> possui várias sobrecargas. A sobrecarga usada no exemplo cria um novo certificado com uma senha de criptografia.  
  
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
 O exemplo de código cria um certificado simples com uma senha de criptografia. Diferente de outros objetos, o método <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> possui várias sobrecargas. A sobrecarga usada no exemplo cria um novo certificado com uma senha de criptografia.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Usando chaves de criptografia](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
