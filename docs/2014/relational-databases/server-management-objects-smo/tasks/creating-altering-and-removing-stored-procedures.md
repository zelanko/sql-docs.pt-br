---
title: Criando, alterando e removendo procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [SMO]
ms.assetid: 2a072f9c-8f11-4364-ab71-3990735a8d66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc38e4f11b32c368626b0f84a352d3f9c00fa0f7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805408"
---
# <a name="creating-altering-and-removing-stored-procedures"></a>Criando, alterando e removendo procedimentos armazenados
  No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), procedimentos armazenados são representados pelo objeto <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>.  
  
 A criação de um objeto <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> no SMO exige a definição da propriedade <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.TextBody%2A> como o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] que define o procedimento armazenado. Parâmetros exigem o \@ de prefixo e devem ser criados individualmente usando <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> objetos e adicionando ao <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> coleção do <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> objeto.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) ou [criar um Visual C&#35; projeto de SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-basic"></a>Criando, alterando e removendo um procedimento armazenado no Visual Basic  
 Este exemplo de código mostra como criar um procedimento armazenado para o banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O exemplo retorna o sobrenome de um funcionário quando é fornecido o número de identificação do funcionário. O procedimento armazenado exige um parâmetro de entrada para especificar o número de identificação do funcionário e um parâmetro de saída para retornar o sobrenome do funcionário.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStoredProcs1](SMO How to#SMO_VBStoredProcs1)]  -->  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-c"></a>Criando, alterando e removendo um procedimento armazenado no Visual C#  
 Este exemplo de código mostra como criar um procedimento armazenado para o banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O exemplo retorna o sobrenome de um funcionário quando é fornecido o número de identificação do funcionário (`BusinessEntityID`). O procedimento armazenado exige um parâmetro de entrada para especificar o número de identificação do funcionário e um parâmetro de saída para retornar o sobrenome do funcionário.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
            StoredProcedure sp;  
            sp = new StoredProcedure(db, "GetLastNameByBusinessEntityID");  
            //Set the TextMode property to false and then set the other object properties.   
            sp.TextMode = false;  
            sp.AnsiNullsStatus = false;  
            sp.QuotedIdentifierStatus = false;  
            //Add two parameters.   
            StoredProcedureParameter param;  
            param = new StoredProcedureParameter(sp, "@empval", DataType.Int);  
            sp.Parameters.Add(param);  
            StoredProcedureParameter param2;  
            param2 = new StoredProcedureParameter(sp, "@retval", DataType.NVarChar(50));  
            param2.IsOutputParameter = true;  
            sp.Parameters.Add(param2);  
            //Set the TextBody property to define the stored procedure.   
            string stmt;  
            stmt = " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )";  
            sp.TextBody = stmt;  
            //Create the stored procedure on the instance of SQL Server.   
            sp.Create();  
            //Modify a property and run the Alter method to make the change on the instance of SQL Server.   
            sp.QuotedIdentifierStatus = true;  
            sp.Alter();  
            //Remove the stored procedure.   
            sp.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-powershell"></a>Criando, alterando e removendo um procedimento armazenado no PowerShell  
 Este exemplo de código mostra como criar um procedimento armazenado para o banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . O exemplo retorna o sobrenome de um funcionário quando é fornecido o número de identificação do funcionário (`BusinessEntityID`). O procedimento armazenado exige um parâmetro de entrada para especificar o número de identificação do funcionário e um parâmetro de saída para retornar o sobrenome do funcionário.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
$sp  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedure `  
-argumentlist $db, "GetLastNameByBusinessEntityID"  
  
#Set the TextMode property to false and then set the other object properties.   
$sp.TextMode = $false  
$sp.AnsiNullsStatus = $false  
$sp.QuotedIdentifierStatus = $false  
  
# Add two parameters  
$type = [Microsoft.SqlServer.Management.SMO.Datatype]::Int  
$param  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@empval",$type  
$sp.Parameters.Add($param)  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::NVarChar(50)  
$param2  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@retval",$type  
$param2.IsOutputParameter = $true  
$sp.Parameters.Add($param2)  
  
#Set the TextBody property to define the stored procedure.   
$sp.TextBody =  " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )"  
  
# Create the stored procedure on the instance of SQL Server.   
$sp.Create()  
  
# Modify a property and run the Alter method to make the change on the instance of SQL Server.   
$sp.QuotedIdentifierStatus = $true  
$sp.Alter()  
  
#Remove the stored procedure.   
$sp.Drop()  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>  
  
  
