---
title: Definindo propriedades | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SMO [SQL Server], properties
- SQL Server Management Objects, properties
- properties [SMO]
ms.assetid: 342569ba-d2f7-44d2-8f3f-ae9c701c7f0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ceffa7d590ad7861b07700ac13ab795a309bff39
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080986"
---
# <a name="setting-properties"></a>Definindo propriedades
  Propriedades são valores que armazenam informações descritivas sobre o objeto. Por exemplo, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] opções de configuração são representadas pelo <xref:Microsoft.SqlServer.Management.Smo.Server.Configuration%2A> propriedades do objeto. As propriedades podem ser acessadas direta ou indiretamente por meio da coleção de propriedades. O acesso direto às propriedades usa a seguinte sintaxe:  
  
 `objInstance.PropertyName`  
  
 Um valor de propriedade pode ser modificado ou recuperado dependendo do tipo de acesso que tem a propriedade, ou seja, acesso de leitura/gravação ou acesso somente leitura. Também é necessário definir certas propriedades antes que um objeto possa ser criado. Para obter mais informações, consulte a referência SMO para o objeto em particular.  
  
> [!NOTE]  
>  Coleções de objetos filho aparecem como a propriedade de um objeto. Por exemplo, o `Tables` coleção é uma propriedade de um `Server` objeto. Para obter mais informações, consulte [usando coleções](using-collections.md).  
  
 As propriedades de um objeto são membros da coleção Properties. A coleção Properties pode ser usada para iterar por cada propriedade de um objeto.  
  
 Às vezes, uma propriedade não está disponível pelas seguintes razões:  
  
-   A versão do servidor não suporta a propriedade, como se você tentasse acessar uma propriedade que representasse um novo recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma versão mais antiga do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   O servidor não fornece dados para a propriedade, por exemplo, se você tentar acessar uma propriedade que representa um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] componente que não está instalado.  
  
 Você pode lidar com essas situações capturando as exceções do SMO <xref:Microsoft.SqlServer.Management.Smo.UnknownPropertyException> e <xref:Microsoft.SqlServer.Management.Smo.PropertyCannotBeRetrievedException>.  
  
## <a name="setting-default-initialization-fields"></a>Definindo campos de inicialização padrão  
 O SMO executa uma otimização ao recuperar objetos. A otimização minimiza o número de propriedades carregado, dimensionando automaticamente entre os seguintes estados:  
  
1.  Parcialmente carregado. Quando um objeto é referenciado pela primeira vez, ele tem um mínimo de propriedades disponíveis (como Nome e Esquema).  
  
2.  Completamente carregado. Quando qualquer propriedade é referenciada, as propriedades restantes de carregamento rápido são inicializadas e disponibilizadas.  
  
3.  Propriedades que consomem muita memória. As propriedades indisponíveis restantes consomem muita memória e têm uma <xref:Microsoft.SqlServer.Management.Smo.Property.Expensive%2A> valor da propriedade de true (como <xref:Microsoft.SqlServer.Management.Smo.Database.DataSpaceUsage%2A>). Essas propriedades só são carregadas quando especificamente referenciadas.  
  
 Se seu aplicativo busca outras propriedades, além daquelas fornecidas no estado parcialmente carregado, ele envia uma consulta para recuperar essas propriedades extras e sobe para o estado totalmente carregado. Isso pode gerar um tráfego desnecessário entre o cliente e o servidor. Mais otimização pode ser obtida chamando o <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> método. O método <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> permite a especificação das propriedades que são carregadas quando o objeto é inicializado.  
  
 O método <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> define o comportamento de carregamento da propriedade para o restante do aplicativo ou até que ele seja reiniciado. Você pode salvar o comportamento original usando o <xref:Microsoft.SqlServer.Management.Smo.Server.GetDefaultInitFields%2A> método e restaurá-lo conforme necessário.  
  
## <a name="examples"></a>Exemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="getting-and-setting-a-property-in-visual-basic"></a>Obtendo e configurando uma propriedade no Visual Basic  
 Este exemplo de código mostra como obter o <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Information> objeto e como definir a <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade para o `ExecuteSql` membro do <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> tipo enumerado.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties1](SMO How to#SMO_VBProperties1)]  -->  
  
## <a name="getting-and-setting-a-property-in-visual-c"></a>Obtendo e configurando uma propriedade no Visual C#  
 Este exemplo de código mostra como obter o <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Information> objeto e como definir a <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propriedade para o `ExecuteSql` membro do <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> tipo enumerado.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Get a property.   
Console.WriteLine(srv.Information.Version);   
//Set a property.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-basic"></a>Definindo várias propriedades antes de um objeto ser criado no Visual Basic  
 Este exemplo de código mostra como definir diretamente a <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Table> objeto e como criar e adicionar colunas antes de criar o <xref:Microsoft.SqlServer.Management.Smo.Table> objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties2](SMO How to#SMO_VBProperties2)]  -->  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-c"></a>Definindo várias propriedades antes de um objeto ser criado no Visual C#  
 Este exemplo de código mostra como definir diretamente a <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Table> objeto e como criar e adicionar colunas antes de criar o <xref:Microsoft.SqlServer.Management.Smo.Table> objeto.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Create a new table in the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
Table tb;   
//Specify the parent database, table schema, and the table name in the constructor.   
tb = new Table(db, "Test_Table", "HumanResources");   
//Add columns because the table requires columns before it can be created.   
Column c1;   
//Specify the parent table, the column name, and data type in the constructor.   
c1 = new Column(tb, "ID", DataType.Int);   
tb.Columns.Add(c1);   
c1.Nullable = false;   
c1.Identity = true;   
c1.IdentityIncrement = 1;   
c1.IdentitySeed = 0;   
Column c2;   
c2 = new Column(tb, "Name", DataType.NVarChar(100));   
c2.Nullable = false;   
tb.Columns.Add(c2);   
tb.AnsiNullsStatus = true;   
//Create the table on the instance of SQL Server.   
tb.Create();   
}  
```  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-basic"></a>Iterando por todas as propriedades de um objeto no Visual Basic  
 Este exemplo de código itera por meio de `Properties` coleção do <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> do objeto e as exibe no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] tela de saída.  
  
 No exemplo, o <xref:Microsoft.SqlServer.Management.Smo.Property> objeto foi colocado entre colchetes porque também é um [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] palavra-chave.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties3](SMO How to#SMO_VBProperties3)]  -->  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-c"></a>Iterando por todas as propriedades de um objeto no Visual C#  
 Este exemplo de código itera por meio de `Properties` coleção do <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> do objeto e as exibe no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] tela de saída.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Set properties on the uspGetEmployeedManagers stored procedure on the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
StoredProcedure sp;   
sp = db.StoredProcedures("uspGetEmployeeManagers");   
sp.AnsiNullsStatus = false;   
sp.QuotedIdentifierStatus = false;   
//Iterate through the properties of the stored procedure and display.   
  Property p;   
  foreach ( p in sp.Properties) {   
    Console.WriteLine(p.Name + p.Value);   
  }   
}  
```  
  
## <a name="setting-default-initialization-fields-in-visual-basic"></a>Definindo campos de inicialização padrão no Visual Basic  
 Este exemplo de código mostra como minimizar o número de propriedades de objeto inicializadas em um programa de SMO. Você tem que incluir o `using System.Collections.Specialized`; instrução para usar o <xref:System.Collections.Specialized.StringCollection> objeto.  
  
 O [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] pode ser usado para comparar as instruções de número enviadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com esta otimização.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaultInitFields1](SMO How to#SMO_VBDefaultInitFields1)]  -->  
  
## <a name="setting-default-initialization-fields-in-visual-c"></a>Definindo campos de inicialização padrão no Visual C#  
 Este exemplo de código mostra como minimizar o número de propriedades de objeto inicializadas em um programa de SMO. Você tem que incluir o `using System.Collections.Specialized`; instrução para usar o <xref:System.Collections.Specialized.StringCollection> objeto.  
  
 O [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] pode ser usado para comparar as instruções de número enviadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com esta otimização.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Assign the Table object type to a System.Type object variable.   
Table tb;   
Type typ;   
tb = new Table();   
typ = tb.GetType;   
//Assign the current default initialization fields for the Table object type to a   
//StringCollection object variable.   
StringCollection sc;   
sc = srv.GetDefaultInitFields(typ);   
//Set the default initialization fields for the Table object type to the CreateDate property.   
srv.SetDefaultInitFields(typ, "CreateDate");   
//Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.   
   //Note that the improvement in performance can be viewed in SQL Server Profiler.   
foreach ( tb in db.Tables) {   
   Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate);   
}   
//Set the default initialization fields for the Table object type back to the original settings.   
srv.SetDefaultInitFields(typ, sc);   
}  
```  
  
  
