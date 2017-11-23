---
title: "Gerenciando usuários, funções e logons | Microsoft Docs"
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
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eeda3dc5a30031545b7a6e500c378d6d4c190a6c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="managing-users-roles-and-logins"></a>Gerenciando usuários, funções e logons
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]No SMO, os logons são representados pelo <xref:Microsoft.SqlServer.Management.Smo.Login> objeto. Quando o logon existir no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ele poderá ser adicionado a uma função de servidor. A função de servidor é representada pelo <xref:Microsoft.SqlServer.Management.Smo.ServerRole> objeto. A função de banco de dados é representada pelo objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> e a função de aplicativo é representada pelo objeto <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole>.  
  
 Privilégios associados ao nível de servidor são listados como propriedades do <xref:Microsoft.SqlServer.Management.Smo.ServerPermission> objeto. Os privilégios em nível de servidor podem ser concedidos a, negados a ou revogados de contas de logon individuais.  
  
 Cada <xref:Microsoft.SqlServer.Management.Smo.Database> objeto tem um <xref:Microsoft.SqlServer.Management.Smo.UserCollection> objeto que especifica todos os usuários no banco de dados. Cada usuário é associado a um logon. Um logon pode ser associado a usuários em mais de um banco de dados. O <xref:Microsoft.SqlServer.Management.Smo.Login> do objeto <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> método pode ser usado para listar todos os usuários em cada banco de dados que está associado ao logon. Alternativamente, a propriedade <xref:Microsoft.SqlServer.Management.Smo.User> do objeto <xref:Microsoft.SqlServer.Management.Smo.Login> especifica o logon que é associado ao usuário.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]bancos de dados também têm funções que especificam um conjunto de privilégios em nível de banco de dados que permitem que um usuário executar tarefas específicas. Diferente das funções de servidor, as funções de banco de dados não são fixas. Elas podem ser criadas, modificadas e removidas. Privilégios e usuários podem ser designados a uma função de banco de dados para administração em massa.  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um Visual C &#35; Projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>Enumerando logons e usuários associados no Visual C#  
 Cada usuário em um banco de dados é associado a um logon. O logon pode ser associado a usuários em mais de um banco de dados. O exemplo de código mostra como chamar o método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para listar todos os usuários de banco de dados associados ao logon. O exemplo cria um logon e usuário no [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] banco de dados para verificar se há informações de mapeamento para enumerar.  
  
```csharp  
{   
Server srv = new Server();   
//Iterate through each database and display.   
  
foreach ( Database db in srv.Databases) {   
   Console.WriteLine("========");   
   Console.WriteLine("Login Mappings for the database: " + db.Name);   
   Console.WriteLine(" ");   
   //Run the EnumLoginMappings method and return details of database user-login mappings to a DataTable object variable.   
   DataTable d;  
   d = db.EnumLoginMappings();   
   //Display the mapping information.   
   foreach (DataRow r in d.Rows) {   
      foreach (DataColumn c in r.Table.Columns) {   
         Console.WriteLine(c.ColumnName + " = " + r[c]);   
      }   
      Console.WriteLine(" ");   
   }   
}   
}  
```  
  
## <a name="enumerating-logins-and-associated-users-in-powershell"></a>Enumerando logons e usuários associados no PowerShell  
 Cada usuário em um banco de dados é associado a um logon. O logon pode ser associado a usuários em mais de um banco de dados. O exemplo de código mostra como chamar o método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para listar todos os usuários de banco de dados associados ao logon. O exemplo cria um logon e usuário no [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] banco de dados para verificar se há informações de mapeamento para enumerar.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\Default\Databases  
  
#Iterate through all databases  
 foreach ($db in Get-ChildItem)  
 {  
 "====="  
 "Login Mappings for the database: "+ $db.Name  
  
 #get the datatable containing the mapping from the smo database oject  
 $dt = $db.EnumLoginMappings()  
  
 #display the results  
 foreach($row in $dt.Rows)  
     {  
        foreach($col in $row.Table.Columns)  
      {  
        $col.ColumnName + "=" + $row[$col]  
       }  
  
     }  
 }  
```  
  
## <a name="managing-roles-and-users"></a>Gerenciando funções e usuários  
 Este exemplo demonstra como gerenciar funções e usuários. Para executar este exemplo, você precisará referenciar os seguintes assemblies:  
  
-   Microsoft.SqlServer.Smo.dll  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
-   Microsoft.SqlServer.ConnectionInfo.dll  
  
-   Microsoft.SqlServer.SqlEnum.dll  
  
```csharp  
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // Creating Logins  
      Login login = new Login(svr, "Login1");  
      login.LoginType = LoginType.SqlLogin;  
      login.Create("password@1");  
  
      Login login2 = new Login(svr, "Login2");  
      login2.LoginType = LoginType.SqlLogin;  
      login2.Create("password@1");  
  
      // Creating Users in the database for the logins created  
      User user1 = new User(db, "User1");  
      user1.Login = "Login1";  
      user1.Create();  
  
      User user2 = new User(db, "User2");  
      user2.Login = "Login2";  
      user2.Create();  
  
      // Creating database permission Sets  
      DatabasePermissionSet dbPermSet = new DatabasePermissionSet(DatabasePermission.AlterAnySchema);  
      dbPermSet.Add(DatabasePermission.AlterAnyUser);  
  
      DatabasePermissionSet dbPermSet2 = new DatabasePermissionSet(DatabasePermission.CreateType);  
      dbPermSet2.Add(DatabasePermission.CreateSchema);  
      dbPermSet2.Add(DatabasePermission.CreateTable);  
  
      // Creating Database roles  
      DatabaseRole role1 = new DatabaseRole(db, "Role1");  
      role1.Create();  
  
      DatabaseRole role2 = new DatabaseRole(db, "Role2");  
      role2.Create();  
  
      // Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name);  
      db.Grant(dbPermSet2, role2.Name);  
  
      // Adding members (Users / Roles) to Role  
      role1.AddMember("User1");  
  
      role2.AddMember("User2");  
  
      // Role1 becomes a member of Role2  
      role2.AddMember("Role1");  
  
      // Enumerating through explicit permissions granted to Role1  
      // enumerates all database permissions for the Grantee  
      DatabasePermissionInfo[] dbPermsRole1 = db.EnumDatabasePermissions("Role1");     
      foreach (DatabasePermissionInfo dbp in dbPermsRole1) {  
         Console.WriteLine(dbp.Grantee + " has " + dbp.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
   }  
}  
```
  
  
