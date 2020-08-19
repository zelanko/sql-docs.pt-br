---
description: Manipulando exceções SMO
title: Manipulando exceções SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 92167925e38e2029ac94d83b7ca4c9566e41527f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448054"
---
# <a name="handling-smo-exceptions"></a>Manipulando exceções SMO
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  No código gerenciado, as exceções são geradas quando ocorre um erro. Os métodos e propriedades do SMO não informam êxito ou falha no valor de retorno. Em vez disso, as exceções podem ser capturadas e manipuladas por um manipulador de exceções.  
  
 Existem classes diferentes de exceção no SMO. As informações sobre a exceção podem ser obtidas das propriedades de exceção, como a propriedade **Message** , que fornece uma mensagem de texto sobre a exceção.  
  
 As instruções que manipulam exceção são específicas da linguagem de programação. Por exemplo, no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic a instrução é **Catch** .  
  
## <a name="inner-exceptions"></a>Exceções internas  
 As exceções podem ser gerais ou específicas. As exceções gerais contêm um conjunto de exceções específicas. Várias instruções **Catch** podem ser usadas para tratar erros antecipados e deixar os erros restantes sem solução no código geral de manipulação de exceção. Normalmente, as exceções ocorrem em uma sequência em cascata. Com frequência, a exceção do SMO é causada por uma exceção SQL. Para detectar isso, use a propriedade **InnerException** sucessivamente para determinar a exceção original que causou a exceção final de nível superior.  
  
> [!NOTE]  
>  A exceção **SqlException** é declarada no namespace **System. Data. SqlClient** .  
  
 ![Um diagrama que mostra os níveis a partir dos quais uma exceção](../../../relational-databases/server-management-objects-smo/create-program/media/exception-flow.gif "Um diagrama que mostra os níveis a partir dos quais uma exceção")  
  
 O diagrama mostra o fluxo de exceções pelas camadas do aplicativo.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).
  
## <a name="catching-an-exception-in-visual-basic"></a>Capturando uma exceção no Visual Basic  
 Este exemplo de código mostra como usar o **bloco try... Capturar... Instrução Finally** [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] para capturar uma exceção de Smo. Todas as exceções do SMO têm o tipo SmoException e estão listadas na referência de SMO. A sequência de exceções internas é exibida para mostrar a raiz do erro. Para obter mais informações, consulte a documentação do [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
```VBNET
'This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace is included.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.
'Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.
Dim op As [Operator]
op = New [Operator](srv.JobServer, "Test_Operator")
op.Create()
'Start exception handling.
Try
    'Create the operator again to cause an SMO exception.
    Dim opx As OperatorCategory
    opx = New OperatorCategory(srv.JobServer, "Test_Operator")
    opx.Create()
    'Catch the SMO exception
Catch smoex As SmoException
    Console.WriteLine("This is an SMO Exception")
    'Display the SMO exception message.
    Console.WriteLine(smoex.Message)
    'Display the sequence of non-SMO exceptions that caused the SMO exception.
    Dim ex As Exception
    ex = smoex.InnerException
    Do While ex.InnerException IsNot (Nothing)
        Console.WriteLine(ex.InnerException.Message)
        ex = ex.InnerException
    Loop
    'Catch other non-SMO exceptions.
Catch ex As Exception
    Console.WriteLine("This is not an SMO exception.")
End Try
``` 
  
## <a name="catching-an-exception-in-visual-c"></a>Capturando uma exceção no Visual C#  
 Este exemplo de código mostra como usar o **bloco try... Capturar... Finalmente,** a instrução Visual C# para capturar uma exceção de Smo. Todas as exceções do SMO têm o tipo SmoException e estão listadas na referência de SMO. A sequência de exceções internas é exibida para mostrar a raiz do erro. Para obter mais informações, consulte a documentação do Visual C#.  
  
```csharp  
{   
//This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace to be included.   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.   
//Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.   
op = new Operator(srv.JobServer, "Test_Operator");   
op.Create();   
//Start exception handling.   
try {   
    //Create the operator again to cause an SMO exception.   
    OperatorCategory opx;   
    opx = new OperatorCategory(srv.JobServer, "Test_Operator");   
    opx.Create();   
}   
//Catch the SMO exception   
catch (SmoException smoex) {   
    Console.WriteLine("This is an SMO Exception");   
   //Display the SMO exception message.   
   Console.WriteLine(smoex.Message);   
   //Display the sequence of non-SMO exceptions that caused the SMO exception.   
   Exception ex;   
   ex = smoex.InnerException;   
   while (!object.ReferenceEquals(ex.InnerException, (null))) {   
      Console.WriteLine(ex.InnerException.Message);   
      ex = ex.InnerException;   
    }   
    }   
   //Catch other non-SMO exceptions.   
   catch (Exception ex) {   
      Console.WriteLine("This is not an SMO exception.");   
}   
}  
```  
  
  
