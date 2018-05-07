---
title: Criando, alterando e Removendo funções definidas pelo usuário | Microsoft Docs
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
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 70176012dc61676a9c6b2193c8ca9034aa871284
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>Criando, alterando e removendo funções definidas pelo usuário
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto fornece funcionalidade que permite aos usuários gerenciar de forma programática funções definidas pelo usuário em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Funções definidas pelo usuário dão suporte a parâmetros de entrada e saída, e também a referências diretas a colunas de tabela.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requer registro dentro de um banco de dados antes de assemblies podem ser usados dentro de procedimentos armazenados, tipos de dados definidos pelo usuário, gatilhos e funções definidas pelo usuário. O SMO dá suporte a esse recurso com o objeto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly>.  
  
 O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto referencia o assembly .NET com o <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A>, e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A> propriedades.  
  
 Quando o <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto faz referência a um assembly do .NET, você deve registrar o assembly criando um <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> objeto e adicioná-lo para o <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> objeto, que pertence ao <xref:Microsoft.SqlServer.Management.Smo.Database> objeto.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto SMO no Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Criando uma função escalar definida pelo usuário no Visual Basic  
 Este exemplo de código mostra como criar e remover uma função escalar definida pelo usuário que tenha uma entrada <xref:System.DateTime> inteiro e parâmetro de objeto de tipo de retorno no [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. A função definida pelo usuário é criada no [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] banco de dados. O exemplo cria uma função definida pelo usuário, ISOweek, que usa um argumento de data e calcula o número da semana ISO. Para que essa função calcule corretamente, defina a opção DATEFIRST do banco de dados como 1 antes da função ser chamada.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.
Dim udf As UserDefinedFunction
udf = New UserDefinedFunction(db, "IsOWeek")
'Set the TextMode property to false and then set the other properties.
udf.TextMode = False
udf.DataType = DataType.Int
udf.ExecutionContext = ExecutionContext.Caller
udf.FunctionType = UserDefinedFunctionType.Scalar
udf.ImplementationType = ImplementationType.TransactSql
'Add a parameter.
Dim par As UserDefinedFunctionParameter
par = New UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime)
udf.Parameters.Add(par)
'Set the TextBody property to define the user defined function.
udf.TextBody = "BEGIN  DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"
'Create the user defined function on the instance of SQL Server.
udf.Create()
'Remove the user defined function.
udf.Drop()
``` 
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Criando uma função escalar definida pelo usuário no Visual C#  
 Este exemplo de código mostra como criar e remover uma função escalar definida pelo usuário que tenha uma entrada <xref:System.DateTime> inteiro e parâmetro de objeto de tipo de retorno no [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. A função definida pelo usuário é criada no [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] banco de dados. O exemplo cria a função definida pelo usuário. `ISOweek`. Essa função usa um argumento de data e calcula o número da semana ISO. Para que essa função seja calculada corretamente, a opção `DATEFIRST` do banco de dados deve ser definida como `1` antes da função ser chamada.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>Criando uma função escalar definida pelo usuário no PowerShell  
 Este exemplo de código mostra como criar e remover uma função escalar definida pelo usuário que tenha uma entrada <xref:System.DateTime> inteiro e parâmetro de objeto de tipo de retorno no [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. A função definida pelo usuário é criada no [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] banco de dados. O exemplo cria a função definida pelo usuário. `ISOweek`. Essa função usa um argumento de data e calcula o número da semana ISO. Para que essa função seja calculada corretamente, a opção `DATEFIRST` do banco de dados deve ser definida como `1` antes da função ser chamada.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.   
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.   
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int   
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.   
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.   
$udf.Create()  
  
# Remove the user-defined function.   
$udf.Drop()  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
  
  
