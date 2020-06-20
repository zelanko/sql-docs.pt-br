---
title: Trabalhar com variáveis programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9d9ce228394ac5e11e9d526aee98dc1c012ef511
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84924737"
---
# <a name="working-with-variables-programmatically"></a>Trabalhando com variáveis programaticamente
  As variáveis são uma forma de definir valores e controlar processos dinamicamente em pacotes, contêineres, tarefas e manipuladores de eventos. As variáveis também podem ser usadas por restrições de precedência para controlar a direção do fluxo de dados para tarefas diferentes. As variáveis têm uma série de usos:

-   Atualizar propriedades de um pacote em tempo de execução.

-   Popule valores de parâmetro para instruções Transact-SQL em tempo de execução.

-   Controlar o fluxo de um loop Foreach. Para obter mais informações, consulte [Adicionar enumeração a um fluxo de controle](../control-flow/control-flow.md).

-   Controlar uma restrição de precedência por seu uso em uma expressão. Uma restrição de precedência pode incluir variáveis na definição de restrição. Para obter mais informações, consulte [Adicionar expressões a restrições de precedência](../control-flow/precedence-constraints.md).

-   Controlar a repetição condicional de um contêiner de Loop For. Para obter mais informações, consulte [Adicionar iteração a um fluxo de controle](../add-iteration-to-a-control-flow.md).

-   Crie expressões que incluam valores de variáveis.

-   Você pode criar variáveis personalizadas para todos os tipos de contêineres: pacotes, contêineres **Loop Foreach**, contêineres **Loop For**, contêineres de **Sequência**, TaskHosts e manipuladores de eventos. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../use-variables-in-packages.md).

## <a name="scope"></a>Escopo
 Cada contêiner tem sua própria coleção <xref:Microsoft.SqlServer.Dts.Runtime.Variables>. Quando uma nova variável é criada, ela fica dentro do escopo de seu contêiner pai. Como o contêiner de pacote está no topo da hierarquia de contêineres, as variáveis com escopo de pacote funcionam como variáveis globais e ficam visíveis para todos os contêineres de pacote. A coleção de variáveis para o contêiner também pode ser acessada pelos filhos do contêiner através da coleção <xref:Microsoft.SqlServer.Dts.Runtime.Variables>, usando o nome da variável ou o índice da variável na coleção.

 Como a visibilidade de uma variável tem um escopo de cima para baixo, as variáveis declaradas no nível do pacote são visíveis para todos os contêineres do pacote. Portanto, a coleção <xref:Microsoft.SqlServer.Dts.Runtime.Variables> em um contêiner inclui todas as variáveis que pertencem a seu pai além de suas próprias variáveis.

 Por outro lado, as variáveis contidas em uma tarefa têm escopo e visibilidade limitados e são visíveis somente para a tarefa.

 Se um pacote executar outros pacotes, as variáveis definidas no escopo do pacote de chamada estarão disponíveis ao pacote chamado. A única exceção ocorre quando há uma variável do mesmo nome no pacote chamado. Quando essa colisão ocorre, o valor variável no pacote chamado anula o valor do pacote de chamada. As variáveis definidas no escopo do pacote chamado não podem ficar disponíveis para o pacote de chamada de novo.

 O exemplo de código seguinte cria programaticamente uma variável, `myCustomVar`, no escopo do pacote, e itera todas as variáveis visíveis do pacote, imprimindo seu nome, tipo de dados e valor.

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Application app = new Application();
      // Load a sample package that contains a variable that sets the file name.
      Package pkg = app.LoadPackage(
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",
        null);
      Variables pkgVars = pkg.Variables;
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");
      foreach (Variable pkgVar in pkgVars)
      {
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,
          pkgVar.DataType, pkgVar.Value.ToString());
      }
      Console.Read();
    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim app As Application = New Application()
    ' Load a sample package that contains a variable that sets the file name.
    Dim pkg As Package = app.LoadPackage( _
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _
      Nothing)
    Dim pkgVars As Variables = pkg.Variables
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")
    Dim pkgVar As Variable
    For Each pkgVar In pkgVars
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _
        pkgVar.DataType, pkgVar.Value.ToString())
    Next
    Console.Read()

  End Sub

End Module
```

 **Saída de exemplo:**

 `Variable: CancelEvent, Int32, 0`

 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`

 `Variable: CreatorComputerName, String,`

 `Variable: CreatorName, String,`

 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`

 `Variable: FileName, String, Junk`

 `Variable: InteractiveMode, Boolean, False`

 `Variable: LocaleID, Int32, 1033`

 `Variable: MachineName, String, MYCOMPUTERNAME`

 `Variable: myCustomVar, String, 3`

 `Variable: OfflineMode, Boolean, False`

 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`

 `Variable: PackageName, String, DTSPackage1`

 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`

 `Variable: UserName, String, <domain>\<userid>`

 `Variable: VersionBuild, Int32, 198`

 `Variable: VersionComments, String,`

 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`

 `Variable: VersionMajor, Int32, 1`

 `Variable: VersionMinor, Int32, 0`

 Observe que todas as variáveis com escopo no namespace **System** estão disponíveis para o pacote. Para obter mais informações, consulte [Variáveis de sistema](../system-variables.md).

## <a name="namespaces"></a>Namespaces
 O   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) fornece dois namespaces padrão em que as variáveis residem; os namespaces **User** e **System**. Por padrão, qualquer variável personalizada criada pelo desenvolvedor é adicionada ao namespace **User**. As variáveis de sistema residem no namespace **System**. Você pode criar namespaces adicionais, além do namespace **User** para manter variáveis personalizadas e você pode alterar o nome do namespace **User**, mas não pode adicionar ou modificar variáveis no namespace **System** nem atribuir variáveis do sistema a outro namespace.

 As variáveis de sistema que estão disponíveis diferem dependendo do tipo de contêiner. Para uma lista das variáveis de sistema disponíveis para pacotes, contêineres, tarefas e manipuladores de eventos, consulte [System Variables](../system-variables.md).

## <a name="value"></a>Valor
 O valor de uma variável personalizada pode ser literal ou uma expressão:

-   Se você quiser a variável para conter um valor literal, defina o valor de sua propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A>.

-   Se você deseja que a variável contenha uma expressão para que você possa usar os resultados da expressão como seu valor, defina a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> da variável como `true` e forneça uma expressão na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A>. Em tempo de execução, a expressão é avaliada e o resultado da expressão é usado como valor da variável. Por exemplo, se a propriedade da expressão de uma variável for `"100 * 2""100 * 2"`, a variável avaliará a um valor de 200.

 Para uma variável, você não pode definir o valor de seu <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> explicitamente. O valor <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> é inferido do valor inicial atribuído à variável e não pode ser alterado posteriormente. Para obter mais informações sobre tipos de dados de variável, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).

 O exemplo de código a seguir cria uma nova variável, define <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> como `true`, atribui a expressão `"100 * 2"` à propriedade da expressão da variável e produz o valor da variável.

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Package pkg = new Package();
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);
      v100.EvaluateAsExpression = true;
      v100.Expression = "100 * 2";
      Console.WriteLine("Expression for myVar: {0}", 
        v100.Properties["Expression"].GetValue(v100));
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());
      Console.Read();
    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim pkg As Package = New Package
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)
    v100.EvaluateAsExpression = True
    v100.Expression = "100 * 2"
    Console.WriteLine("Expression for myVar: {0}", _
      v100.Properties("Expression").GetValue(v100))
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)
    Console.Read()

  End Sub

End Module
```

 **Saída de exemplo:**

 `Expression for myVar: 100 * 2`

 `Value of myVar: 200`

 A expressão deve ser uma expressão válida que usa a sintaxe da expressão [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Literais são permitidos em expressões variáveis, além dos operadores e funções que a sintaxe da expressão fornece, mas as expressões não podem fazer referência a outras variáveis ou colunas. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md).

## <a name="configuration-files"></a>Arquivos de configuração
 Se um arquivo de configuração incluir uma variável personalizada, a variável poderá ser atualizada em tempo de execução. Isso significa que quando o pacote é executado, o valor da variável originalmente no pacote é substituído por um novo valor do arquivo de configuração. Essa técnica de substituição é útil quando um pacote é implantado em vários servidores que requerem valores de variável diferentes. Por exemplo, uma variável pode especificar o número de vezes que um contêiner **Loop Foreach** repete seu fluxo de trabalho ou então listar os recipientes para os quais um manipulador de eventos envia email quando um erro é gerado ou alterar o número de erros que podem ocorrer antes de o pacote falhar. Essas variáveis são fornecidas dinamicamente em arquivos de configuração para cada ambiente. Portanto, somente as variáveis de leitura/gravação são permitidas em arquivos de configuração. Para obter mais informações, consulte [Criar configurações de pacote](../create-package-configurations.md).

![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

## <a name="see-also"></a>Consulte Também
 [Integration Services &#40;as variáveis do SSIS&#41;](../integration-services-ssis-variables.md) [usam variáveis em pacotes](../use-variables-in-packages.md)


