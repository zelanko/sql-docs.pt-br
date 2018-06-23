---
title: Manipulando exceções SMO | Microsoft Docs
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
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 329cc87a9a82545708f71202f15de4eb219463e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116563"
---
# <a name="handling-smo-exceptions"></a>Manipulando exceções SMO
  No código gerenciado, as exceções são geradas quando ocorre um erro. Os métodos e propriedades do SMO não informam êxito ou falha no valor de retorno. Em vez disso, as exceções podem ser capturadas e manipuladas por um manipulador de exceções.  
  
 Existem classes diferentes de exceção no SMO. As informações sobre a exceção podem ser obtidas das propriedades de exceção, como a propriedade `Message`, que fornece uma mensagem de texto sobre a exceção.  
  
 As instruções que manipulam exceção são específicas da linguagem de programação. Por exemplo, no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic a instrução é `Catch`.  
  
## <a name="inner-exceptions"></a>Exceções internas  
 As exceções podem ser gerais ou específicas. As exceções gerais contêm um conjunto de exceções específicas. Vários `Catch` instruções podem ser usadas para tratar erros antecipados e deixar os restantes erros falha geral do código de tratamento de exceção. Normalmente, as exceções ocorrem em uma sequência em cascata. Com frequência, a exceção do SMO é causada por uma exceção SQL. A maneira de detectar isso é usar o `InnerException` propriedade sucessivamente para determinar a exceção original que causou a exceção final de nível superior.  
  
> [!NOTE]  
>  O `SQLException` exceção for declarada no **SqlClient** namespace.  
  
 ![Um diagrama que mostra os níveis da qual uma exceção](../../../database-engine/dev-guide/media/exception-flow.gif "um diagrama que mostra os níveis da qual uma exceção")  
  
 O diagrama mostra o fluxo de exceções pelas camadas do aplicativo.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo de programação e a linguagem de programação para criar o aplicativo. Para obter mais informações, consulte [criar um Visual C&#35; projeto SMO no Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md) ou [criar um projeto Visual Basic SMO no Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md).  
  
## <a name="catching-an-exception-in-visual-basic"></a>Capturando uma exceção no Visual Basic  
 Este exemplo de código mostra como usar o `Try…Catch…Finally` [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] instrução para capturar uma exceção de SMO. Todas as exceções do SMO têm o tipo SmoException e estão listadas na referência de SMO. A sequência de exceções internas é exibida para mostrar a raiz do erro. Para obter mais informações, consulte o [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] documentação do .NET.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBExceptions1](SMO How to#SMO_VBExceptions1)]  -->  
  
## <a name="catching-an-exception-in-visual-c"></a>Capturando uma exceção no Visual C#  
 Este exemplo de código mostra como usar a instrução Visual C# `Try…Catch…Finally` para capturar uma exceção do SMO. Todas as exceções do SMO têm o tipo SmoException e estão listadas na referência de SMO. A sequência de exceções internas é exibida para mostrar a raiz do erro. Para obter mais informações, consulte a documentação do Visual C#.  
  
```  
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
  
  