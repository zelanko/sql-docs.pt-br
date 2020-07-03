---
title: Introdução com integração CLR | Microsoft Docs
description: Este artigo descreve os namespaces e as bibliotecas necessárias para compilar objetos de banco de dados usando a integração de Microsoft SQL Server com o .NET Framework CLR.
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: quickstart
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cc5169c81b53f45ca036b064b47d370f21ec2e32
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885919"
---
# <a name="getting-started-with-clr-integration"></a>Introdução à integração CLR

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Este tópico fornece uma visão geral dos namespaces e das bibliotecas necessárias para compilar objetos de banco de dados usando a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integração com o .NET Framework Common Language Runtime (CLR). O tópico também mostra como escrever, compilar e executar um procedimento armazenado CLR simples escrito no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#.  
  
## <a name="required-namespaces"></a>Namespaces obrigatórios  

Os componentes necessários para desenvolver objetos básicos de banco de dados CLR são instalados com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A funcionalidade de integração CLR é exposta em um assembly chamado system.data.dll, que faz parte do .NET Framework. Esse assembly pode ser localizado no GAC (cache de assembly global), bem como no diretório do .NET Framework. Normalmente uma referência a esse assembly é adicionada automaticamente por ferramentas de linha de comando e pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio, por isso não é necessário adicioná-lo manualmente.  
  
O assembly system.data.dll contém os namespaces a seguir, que são necessários para compilar objetos de banco de dados de CLR:  
  
- `System.Data`  
- `System.Data.Sql`  
- `Microsoft.SqlServer.Server`  
- `System.Data.SqlTypes`  

> [!TIP]
> Há suporte para o carregamento de objetos de banco de dados CLR no Linux, mas eles devem ser criados com o .NET Framework (a integração do SQL Server CLR não dá suporte ao .NET Core). Além disso, os assemblies CLR com o EXTERNAL_ACCESS ou o conjunto de permissões não seguro não têm suporte no Linux.

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
    \<Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(\<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
Esse programa simples contém um único método estático em uma classe pública. Esse método usa duas novas classes, **[SqlContext](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.aspx)** e **[SqlPipe](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)**, para criar objetos de banco de dados gerenciado para gerar uma mensagem de texto simples. O método também atribui a cadeia de caracteres "Olá, mundo!" como o valor de um parâmetro out. Esse método pode ser declarado como procedimento armazenado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e executado de maneira igual a um procedimento armazenado [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
Compile este programa como uma biblioteca, carregue-o em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e execute-o como um procedimento armazenado.  
  
## <a name="compile-the-hello-world-stored-procedure"></a>Compilar o procedimento armazenado "Olá, Mundo"  

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala os arquivos de redistribuição do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework por padrão. Esses arquivos incluem csc.exe e vbc.exe, os compiladores de linha de comando para os programas Visual C# e Visual Basic. Para compilar nosso exemplo, você precisa modificar sua variável de caminho para que aponte para o diretório que contém csc.exe ou vbc.exe. A seguir está o caminho de instalação padrão do .NET Framework.  
  
`C:\Windows\Microsoft.NET\Framework\(version)`  
  
Version é o número de versão do redistribuível do .NET Framework instalado. Por exemplo:  
  
`C:\Windows\Microsoft.NET\Framework\v4.6.1`

Depois de adicionar o diretório do .NET Framework ao caminho, você pode compilar o exemplo de procedimento armazenado em um assembly com o comando a seguir. A opção **/target** permite compilá-lo em um assembly.  
  
Para arquivos de origem do Visual C#:  
  
`csc /target:library helloworld.cs`  
  
 Para arquivos de origem do Visual Basic:  
  
`vbc /target:library helloworld.vb`  
  
Esses comandos iniciam o compilador do Visual C# ou do Visual Basic que usa a opção /target para especificar a compilação de uma DLL da biblioteca.  
  
## <a name="loading-and-running-the-hello-world-stored-procedure-in-sql-server"></a>Carregando e executando o procedimento armazenado "Hello World" no SQL Server  

Após o término da compilação do exemplo de procedimento, você pode testá-lo no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para fazer isso, abra o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e crie uma consulta nova, conectando-se a um banco de dados de teste satisfatório (por exemplo, o banco de dados de amostra do AdventureWorks).  
  
A capacidade de executar código CLR (Common Language Runtime) é definida, por padrão, como OFF no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código CLR pode ser habilitado usando o procedimento armazenado do sistema **sp_configure** . Para obter mais informações, consulte [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
  
Precisaremos criar o assembly para podermos acessar o procedimento armazenado. Nesse exemplo, vamos pressupor que você criou o assembly helloworld.dll no diretório C:\. Adicione a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] à sua consulta.  
  
`CREATE ASSEMBLY helloworld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE`  
  
Após a criação do assembly, poderemos acessar nosso método HelloWorld usando a instrução create procedure. Chamaremos nosso procedimento armazenado de "hello":  
  
```sql
CREATE PROCEDURE hello  
@i nchar(25) OUTPUT  
AS  
EXTERNAL NAME helloworld.HelloWorldProc.HelloWorld  
-- if the HelloWorldProc class is inside a namespace (called MyNS),  
-- the last line in the create procedure statement would be  
-- EXTERNAL NAME helloworld.[MyNS.HelloWorldProc].HelloWorld  
```  
  
Após a criação do procedimento, ele poderá ser executado como um procedimento armazenado normal escrito em [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Execute o comando a seguir:  
  
```sql
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
  
```sql
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'hello')  
   drop procedure hello  
```  
  
Após o descarte do procedimento, você poderá remover o assembly que contém seu código de exemplo.  
  
```sql
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'helloworld')  
   drop assembly helloworld  
```  
  
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre a integração CLR no SQL Server, consulte os seguintes artigos:

- [Procedimentos armazenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)
- [Extensões específicas em processo do SQL Server para o ADO.NET](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)
- [Depurando objetos de banco de dados CLR](../../../relational-databases/clr-integration/debugging-clr-database-objects.md)
- [Segurança da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)
