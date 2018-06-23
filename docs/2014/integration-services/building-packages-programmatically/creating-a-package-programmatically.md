---
title: Criar um pacote programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c5955cc67583b5560e3998898822c7905d2d8e41
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009799"
---
# <a name="creating-a-package-programmatically"></a>Criando um pacote programaticamente
  O objeto <xref:Microsoft.SqlServer.Dts.Runtime.Package> é o contêiner de alto nível para todos os outros objetos em uma solução de projeto do [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Como contêiner de alto nível, o pacote é o primeiro objeto criado, e os objetos subsequentes são adicionados a ele e executados dentro do contexto do pacote. O próprio pacote não move nem transforma dados. O pacote confia nas tarefas que contém para executar o trabalho. As tarefas executam a maioria do trabalho executado por um pacote e definem a funcionalidade de um pacote. Um pacote é criado e executado com apenas três linhas de código, mas várias tarefas e objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> são adicionados para acrescentar funcionalidades ao seu pacote. Esta seção discute como criar um pacote programaticamente. Ela não fornece informações sobre como criar as tarefas ou o <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>. Essas informações são discutidas em seções posteriores.  
  
## <a name="example"></a>Exemplo  
 Para gravar um código usando o ambiente de desenvolvimento integrado (IDE) do Visual Studio, uma referência ao Microsoft.SqlServer.ManagedDTS.DLL é necessária para criar uma instrução `using` (`Imports` no Visual Basic .NET) para o Microsoft.SqlServer.Dts.Runtime. O exemplo de código seguinte demonstra como criar um pacote vazio.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package;  
      package = new Package();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package  
    package = New Package  
  
  End Sub  
  
End Module  
```  
  
 Para compilar e executar o exemplo, pressione F5 no Visual Studio. Para compilar o código usando o compilador C#, **csc.exe**, no prompt de comando para compilar, use o comando e as referências de arquivo a seguir, substituindo o *\<nomedoarquivo>* pelo nome do arquivo .cs ou .vb e dando a ele um *\<nomedoarquivodesaída>* de sua escolha.  
  
 **csc /target:library /out: \<nomedoarquivodesaída>.dll \<nomedoarquivo>.cs /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 Para compilar o código usando o compilador do Visual Basic .NET, **vbc.exe**, no prompt de comando para compilar, use o comando e as referências de arquivo a seguir.  
  
 **vbc /target:library /out: \<nomedoarquivodesaída>.dll \<nomedoarquivo>.vb /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 Você também pode criar um pacote carregando um pacote existente que foi salvo em disco, no sistema de arquivos, ou no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A diferença é que o objeto <xref:Microsoft.SqlServer.Dts.Runtime.Application> é criado primeiro e depois o objeto do pacote é preenchido por um dos métodos sobrecarregados do aplicativo: `LoadPackage` para arquivos simples, `LoadFromSQLServer` para pacotes salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> para pacotes salvos no sistema de arquivos. O exemplo seguinte carrega um pacote existente do disco e exibe várias propriedades no pacote.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class ApplicationTests  
  {  
    static void Main(string[] args)  
    {  
      // The variable pkg points to the location of the  
      // ExecuteProcess package sample that was installed with  
      // the SSIS samples.  
      string pkg = @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx";  
  
      Application app = new Application();  
      Package p = app.LoadPackage(pkg, null);  
  
      // Now that the package is loaded, we can query on  
      // its properties.  
      int n = p.Configurations.Count;  
      DtsProperty p2 = p.Properties["VersionGUID"];  
      DTSProtectionLevel pl = p.ProtectionLevel;  
  
      Console.WriteLine("Number of configurations = " + n.ToString());  
      Console.WriteLine("VersionGUID = " + (string)p2.GetValue(p));  
      Console.WriteLine("ProtectionLevel = " + pl.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module ApplicationTests  
  
  Sub Main()  
  
    ' The variable pkg points to the location of the  
    ' ExecuteProcess package sample that was installed with  
    ' the SSIS samples.  
    Dim pkg As String = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx"  
  
    Dim app As Application = New Application()  
    Dim p As Package = app.LoadPackage(pkg, Nothing)  
  
    ' Now that the package is loaded, we can query on  
    ' its properties.  
    Dim n As Integer = p.Configurations.Count  
    Dim p2 As DtsProperty = p.Properties("VersionGUID")  
    Dim pl As DTSProtectionLevel = p.ProtectionLevel  
  
    Console.WriteLine("Number of configurations = " & n.ToString())  
    Console.WriteLine("VersionGUID = " & CType(p2.GetValue(p), String))  
    Console.WriteLine("ProtectionLevel = " & pl.ToString())  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Saída de exemplo:**  
  
 `Number of configurations = 2`  
  
 `VersionGUID = {09016682-89B8-4406-AAC9-AF1E527FF50F}`  
  
 `ProtectionLevel = DontSaveSensitive`  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [API Sample – OleDB source and OleDB destination](http://go.microsoft.com/fwlink/?LinkId=220824), (Amostra de API – origem e destino de OleDB) em blogs.msdn.com.  
  
-   Entrada de blog, [EzAPI – Atualizado para SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223) em blogs.msdn.com.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**permanecer acima para data com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar tarefas programaticamente](../building-packages-programmatically/adding-tasks-programmatically.md)  
  
  