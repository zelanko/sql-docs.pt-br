---
title: Criar um enumerador Foreach personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom foreach enumerators [Integration Services], creating
ms.assetid: 050e8455-2ed0-4b6d-b3ea-4e80e6c28487
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 78b344d355a048a9933648283af4654f8ff692cf
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427523"
---
# <a name="creating-a-custom-foreach-enumerator"></a>Criando um enumerador Foreach personalizado
  As etapas envolvidas na criação de um enumerador foreach personalizado são semelhantes às etapas da criação de qualquer outro objeto personalizado do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Crie uma classe nova herdada da classe base. Para um enumerador foreach, a classe base é <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>.  
  
-   Aplique o atributo que identifica o tipo de objeto para a classe. Para um enumerador foreach, o atributo é <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
-   Substitua a implementação dos métodos e propriedades da classe base. Para um enumerador foreach, o mais importante é o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
-   Opcionalmente, desenvolva uma interface de usuário personalizada. Para um enumerador foreach, isso requer uma classe que implemente a interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSForEachEnumeratorUI>.  
  
 Um enumerador personalizado é hospedado pelo contêiner <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>. Durante o tempo de execução, o contêiner <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> chama o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> do enumerador personalizado. O enumerador personalizado retorna um objeto que implementa a interface `IEnumerable`, como uma `ArrayList`. O <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> itera em cada elemento da coleção, fornece o valor do elemento atual para o fluxo de controle por meio de uma variável definida pelo usuário e executa o fluxo de controle no contêiner.  
  
## <a name="getting-started-with-a-custom-foreach-enumerator"></a>Guia de Introdução com um enumerador ForEach personalizado  
  
### <a name="creating-projects-and-classes"></a>Criando projetos e classes  
 Como todos os enumeradores foreach derivam da classe base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, o primeiro passo para cria enumerador foreach é criar um projeto de biblioteca de classes na linguagem de programação gerenciada de sua preferência e criar uma classe herdada da classe base. Nessa classe derivada, você substituirá os métodos e propriedades da classe base para implementar sua funcionalidade personalizada.  
  
 Na mesma solução, crie um segundo projeto de biblioteca de classe para a interface de usuário personalizada. Recomenda-se um assembly separado para a interface de usuário para facilitar a implantação pois ela permite que você atualize e reimplante o enumerador foreach ou sua interface de usuário de forma independente.  
  
 Configure ambos os projetos para atribuir os assemblies que serão gerados no momento de compilação usando um arquivo de chave de nome forte.  
  
### <a name="applying-the-dtsforeachenumerator-attribute"></a>Aplicando o atributo DtsForEachEnumerator  
 Aplique o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> à classe que você criou para identificá-lo como um enumerador foreach. Esse atributo fornece informações de tempo de design como o nome e a descrição do enumerador foreach. A `Name` propriedade aparece na lista suspensa de enumeradores disponíveis na guia **coleção** da caixa de diálogo **Editor de loop foreach** .  
  
 Use a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> para vincular o enumerador foreach à sua interface do usuário personalizada. Para obter o token de chave pública exigido para essa propriedade, você pode usar o **sn.exe -t** para exibir o token de chave pública por meio do arquivo de par de chaves (.snk) a ser usado para assinar o assembly da interface do usuário.  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Namespace Microsoft.Samples.SqlServer.Dts  
    <DtsForEachEnumerator(DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")> _   
    Public Class MyEnumerator  
     Inherits ForEachEnumerator  
        'Insert code here.  
    End Class  
End Namespace  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsForEachEnumerator( DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")]  
    public class MyEnumerator : ForEachEnumerator  
    {  
        //Insert code here.  
    }  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-enumerator"></a>Compilando, implantando e depurando um enumerador personalizado  
 As etapas para compilar, implantar e depurar um enumerador foreach personalizado no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] são muito semelhantes às etapas necessárias para outros tipos de objetos personalizados. Para obter mais informações, consulte [Compilar, implantar e depurar objetos personalizados](../building-deploying-and-debugging-custom-objects.md).  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Codificando um enumerador foreach personalizado](coding-a-custom-foreach-enumerator.md)   
 [Desenvolvendo uma interface do usuário para um enumerador ForEach personalizado](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
