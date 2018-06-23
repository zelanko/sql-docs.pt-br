---
title: Usando coleções | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e0743b27b996266e546bc04787cda009af5ec005
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120538"
---
# <a name="using-collections"></a>Usando coleções
  Uma coleção é uma lista de objetos que foram construídos na mesma classe de objeto e que compartilham o mesmo objeto pai. O objeto de coleção sempre contém o nome do tipo de objeto com o sufixo Collection. Por exemplo, para acessar as colunas em uma tabela especificada, use o tipo de objeto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Ele contém todos os objetos <xref:Microsoft.SqlServer.Management.Smo.Column> que pertencem ao mesmo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each` instrução ou o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach` instrução pode ser usada para iterar por meio de cada membro da coleção.  
  
## <a name="examples"></a>Exemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Referenciando um objeto usando uma coleção no Visual Basic  
 Este exemplo de código mostra como definir uma propriedade de coluna usando o <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>, e <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> propriedades. Essas propriedades representam coleções, que podem ser usadas para identificar um determinado objeto quando usadas com um parâmetro que especifica o nome do objeto. O nome e o esquema são necessários para o <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> propriedade do objeto de coleção.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Referenciando um objeto usando uma coleção no Visual C#  
 Este exemplo de código mostra como definir uma propriedade de coluna usando o <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>, e <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> propriedades. Essas propriedades representam coleções, que podem ser usadas para identificar um determinado objeto quando usadas com um parâmetro que especifica o nome do objeto. O nome e o esquema são necessários para o <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> propriedade do objeto de coleção.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>Iterando através dos membros de uma coleção no Visual Basic  
 Este exemplo de código itera por meio de <xref:Microsoft.AnalysisServices.Server.Databases%2A> exibe todas as conexões com a instância do banco de dados e propriedade da coleção [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Iterando através dos membros de uma coleção no Visual C#  
 Este exemplo de código itera por meio de <xref:Microsoft.AnalysisServices.Server.Databases%2A> exibe todas as conexões com a instância do banco de dados e propriedade da coleção [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  