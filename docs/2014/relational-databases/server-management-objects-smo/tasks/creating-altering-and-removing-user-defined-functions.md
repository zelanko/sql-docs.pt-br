---
title: Criando, alterando e Removendo funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4f5c1cdb80e7965fbc8e9038307f93df6dcec489
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63226255"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>Criando, alterando e removendo funções definidas pelo usuário
  O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto fornece a funcionalidade que permite aos usuários gerenciar de forma programática funções definidas pelo usuário no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Funções definidas pelo usuário dão suporte a parâmetros de entrada e saída, e também a referências diretas a colunas de tabela.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige o registro de assemblies dentro de um banco de dados antes de sua utilização dentro de procedimentos armazenados, funções definidas pelo usuário, gatilhos e tipos de dados definidos pelo usuário. O SMO dá suporte a esse recurso com o objeto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly>.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> referencia o assembly .NET com as propriedades <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A>.  
  
 Quando o objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> referenciar um assembly .NET, registre o assembly criando um objeto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> e adicionando-o ao objeto <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection>, que pertence ao objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto de SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Criando uma função escalar definida pelo usuário no Visual Basic  
 Este exemplo de código mostra como criar e remover uma função escalar definida pelo usuário que possui um parâmetro do objeto <xref:System.DateTime> de entrada e um tipo de retorno inteiro no [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. A função definida pelo usuário é criada no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O exemplo cria uma função definida pelo usuário, ISOweek, que usa um argumento de data e calcula o número da semana ISO. Para que essa função calcule corretamente, defina a opção DATEFIRST do banco de dados como 1 antes da função ser chamada.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Criando uma função escalar definida pelo usuário no Visual C#  
 Este exemplo de código mostra como criar e remover uma função escalar definida pelo usuário que possui um parâmetro do objeto <xref:System.DateTime> de entrada e um tipo de retorno inteiro no [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. A função definida pelo usuário é criada no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O exemplo cria a função definida pelo usuário. `ISOweek`. Essa função usa um argumento de data e calcula o número da semana ISO. Para que essa função seja calculada corretamente, a opção `DATEFIRST` do banco de dados deve ser definida como `1` antes da função ser chamada.  
  
```  
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
 Este exemplo de código mostra como criar e remover uma função escalar definida pelo usuário que possui um parâmetro do objeto <xref:System.DateTime> de entrada e um tipo de retorno inteiro no [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. A função definida pelo usuário é criada no banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O exemplo cria a função definida pelo usuário. `ISOweek`. Essa função usa um argumento de data e calcula o número da semana ISO. Para que essa função seja calculada corretamente, a opção `DATEFIRST` do banco de dados deve ser definida como `1` antes da função ser chamada.  
  
```  
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
  
  
