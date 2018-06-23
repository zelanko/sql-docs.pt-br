---
title: Introdução à integração CLR | Microsoft Docs
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
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration]
- namespaces [CLR integration]
- database objects [CLR integration], about CLR integration
- stored procedures [CLR integration]
- common language runtime [SQL Server], about CLR integration
- building database objects [CLR integration], about CLR integration
- common language runtime [SQL Server], stored procedures
- common language runtime [SQL Server], namespaces
- Hello World example [CLR integration]
- library [CLR integration]
ms.assetid: c73e628a-f54a-411a-bfe3-6dae519316cc
caps.latest.revision: 60
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7616d610cbdd581325325f9ad00a57b417ef2987
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010266"
---
# <a name="getting-started-with-clr-integration"></a>Introdução à integração CLR
  Este tópico fornece uma visão geral dos namespaces e bibliotecas necessários para compilar objetos de banco de dados usando o [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] integração com o .NET Framework common language runtime (CLR). O tópico também mostra como escrever, compilar e executar um procedimento armazenado CLR simples escrito no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#.  
  
## <a name="required-namespaces"></a>Namespaces obrigatórios  
 Começando com [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)]. A funcionalidade de integração CLR é exposta em um assembly chamado system.data.dll, que faz parte do .NET Framework. Esse assembly pode ser localizado no GAC (cache de assembly global), bem como no diretório do .NET Framework. Normalmente uma referência a esse assembly é adicionada automaticamente por ferramentas de linha de comando e pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio, por isso não é necessário adicioná-lo manualmente.  
  
 O assembly system.data.dll contém os namespaces a seguir, que são necessários para compilar objetos de banco de dados de CLR:  
  
 `System.Data`  
  
 `System.Data.Sql`  
  
 `Microsoft.SqlServer.Server`  
  
 `System.Data.SqlTypes`  
  
## <a name="writing-a-simple-hello-world-stored-procedure"></a>Escrevendo um simples procedimento armazenado "Hello World"  
 Copie e cole o seguinte código em Visual C# ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic em um editor de texto e salve-o em um arquivo chamado "helloworld.cs" ou "helloworld.vb".  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
  
public class HelloWorldProc  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld(out string text)  
    {  
        SqlContext.Pipe.Send("Hello world!" + Environment.NewLine);  
        text = "Hello world!";  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.Runtime.InteropServices  
  
Public Class HelloWorldProc  
    <Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
 Esse programa simples contém um único método estático em uma classe pública. Esse método usa duas classes novas, `SqlContext` e `SqlPipe`, para criar objetos de banco de dados gerenciados para produzir uma mensagem de texto simples. O método também atribui a cadeia de caracteres "Hello world!" como o valor de um parâmetro de saída. Esse método pode ser declarado como um procedimento armazenado no [!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)] procedimento armazenado.  
  
 Agora vamos compilar esse programa como uma biblioteca, carregá-lo no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e executá-lo como um procedimento armazenado.  
  
## <a name="compiling-the-hello-world-stored-procedure"></a>Compilando o procedimento armazenado "Hello World"  
 [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)] Arquivos de redistribuição do .NET framework por padrão. Esses arquivos incluem csc.exe e vbc.exe, os compiladores de linha de comando para os programas Visual C# e Visual Basic. Para compilar nosso exemplo, você precisa modificar sua variável de caminho para que aponte para o diretório que contém csc.exe ou vbc.exe. A seguir está o caminho de instalação padrão do .NET Framework.  
  
```  
C:\Windows\Microsoft.NET\Framework\(version)  
```  
  
 Version é o número de versão do redistribuível do .NET Framework instalado. Por exemplo:  
  
```  
C:\Windows\Microsoft.NET\Framework\v2.0.31113  
```  
  
 Depois de adicionar o diretório do .NET Framework ao caminho, você pode compilar o exemplo de procedimento armazenado em um assembly com o comando a seguir. A opção `/target` permite compilá-lo em um assembly.  
  
 Para arquivos de origem do Visual C#:  
  
```  
csc /target:library helloworld.cs   
```  
  
 Para arquivos de origem do Visual Basic:  
  
```  
vbc /target:library helloworld.vb  
```  
  
 Esses comandos iniciam o compilador do Visual C# ou do Visual Basic que usa a opção /target para especificar a compilação de uma DLL da biblioteca.  
  
## <a name="loading-and-running-the-hello-world-stored-procedure-in-sql-server"></a>Carregando e executando o procedimento armazenado "Hello World" no SQL Server  
 Depois que o procedimento de exemplo foi compilada com êxito, você pode testá-lo no [!INCLUDE[ssNoVersion](../../../includes/ssmanstudiofull-md.md)] e crie uma nova consulta, conectando-se a um banco de dados de teste correspondente (por exemplo, dados de exemplo AdventureWorks).  
  
 A capacidade de executar código CLR (Common Language Runtime) é definida, por padrão, como OFF no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código CLR pode ser habilitado usando o **sp_configure** procedimento armazenado do sistema. Para obter mais informações, consulte [Enabling CLR Integration](../clr-integration-enabling.md).  
  
 Precisaremos criar o assembly para podermos acessar o procedimento armazenado. Nesse exemplo, vamos pressupor que você criou o assembly helloworld.dll no diretório C:\. Adicione a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] à sua consulta.  
  
```  
CREATE ASSEMBLY helloworld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE  
```  
  
 Após a criação do assembly, poderemos acessar nosso método HelloWorld usando a instrução create procedure. Chamaremos nosso procedimento armazenado de "hello":  
  
```  
  
CREATE PROCEDURE hello  
@i nchar(25) OUTPUT  
AS  
EXTERNAL NAME helloworld.HelloWorldProc.HelloWorld  
-- if the HelloWorldProc class is inside a namespace (called MyNS),  
-- the last line in the create procedure statement would be  
-- EXTERNAL NAME helloworld.[MyNS.HelloWorldProc].HelloWorld  
```  
  
 Após a criação do procedimento, ele poderá ser executado como um procedimento armazenado normal escrito em [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Execute o comando a seguir:  
  
```  
DECLARE @J nchar(25)  
EXEC hello @J out  
PRINT @J  
```  
  
 Isso deve resultar na seguinte saída na janela de mensagens do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
```  
Hello world!  
Hello world!  
```  
  
## <a name="removing-the-hello-world-stored-procedure-sample"></a>Removendo o exemplo de procedimento armazenado "Hello World"  
 Quando você concluir a execução do exemplo de procedimento armazenado, poderá remover o procedimento e o assembly de seu banco de dados de teste.  
  
 Primeiro, remova o procedimento usando o comando drop procedure.  
  
```  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'hello')  
   drop procedure hello  
```  
  
 Após o descarte do procedimento, você poderá remover o assembly que contém seu código de exemplo.  
  
```  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'helloworld')  
   drop assembly helloworld  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [Extensões específicas do SQL Server no processo para o ADO.NET](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)   
 [Depuração de objetos de banco de dados CLR](../debugging-clr-database-objects.md)   
 [Segurança da integração CLR](../security/clr-integration-security.md)  
  
  