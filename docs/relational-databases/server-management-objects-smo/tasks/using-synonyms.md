---
title: Usando sinônimos | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4da1cefbb07186134a1c6f14c335a2aacc507f6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148308"
---
# <a name="using-synonyms"></a>Usando sinônimos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Um sinônimo é um nome alternativo de um objeto com escopo de esquema. No SMO, os sinônimos são representados pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym>. O objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> é um filho do objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. Isso significa que sinônimos só são válidos dentro do escopo do banco de dados no qual eles são definidos. Porém, o sinônimo pode se referir a objetos em outro banco de dados, ou em uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O objeto que recebe um nome alternativo é conhecido como o objeto base. A propriedade do nome do objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> é o nome alternativo fornecido ao objeto base.  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-synonym-in-visual-c"></a>Criando um sinônimo no Visual C#  
 O exemplo de código mostra como criar um sinônimo ou um nome alternativo para um objeto com escopo de esquema. Aplicativos cliente podem usar uma única referência para o objeto base através de um sinônimo, em vez de usar um nome com várias partes para fazer referência ao objeto base.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>Criando um sinônimo no PowerShell  
 O exemplo de código mostra como criar um sinônimo ou um nome alternativo para um objeto com escopo de esquema. Aplicativos cliente podem usar uma única referência para o objeto base através de um sinônimo, em vez de usar um nome com várias partes para fazer referência ao objeto base.  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym `  
-argumentlist $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../../t-sql/statements/create-synonym-transact-sql.md)  
  
  
