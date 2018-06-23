---
title: Aprimorando uma saída de erro com o componente Script | Microsoft Docs
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
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: db92a9dddb75f8dd7b6856124a8a1abd450f7323
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121511"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Aprimorando uma saída de erro com o componente Script
  Por padrão, as duas colunas extras em uma saída de erro do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ErrorCode e ErrorColumn, contêm apenas códigos numéricos que representam um número de erro e a ID da coluna na qual o erro ocorreu. Esses valores numéricos podem ter uso limitado sem a descrição de erro correspondente.  
  
 Este tópico descreve como acrescentar uma coluna de descrição de erro a dados de saída de erro existentes no fluxo de dados usando o componente Script. O exemplo adiciona a descrição de erro que corresponde a um código de erro específico e predefinido do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> da interface do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, disponível através da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> do componente Script.  
  
> [!NOTE]  
>  Se desejar criar um componente que possa ser reutilizado mais facilmente em várias tarefas de fluxo de dados e em vários pacotes, procure utilizar o código deste exemplo de componente Script como o ponto inicial de um componente de fluxo de dados personalizado. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo demonstrado aqui usa um componente Script configurado como uma transformação para acrescentar uma coluna de descrição de erro a dados de saída de erro existentes no fluxo de dados.  
  
 Para obter mais informações sobre como configurar o componente de Script para usar como uma transformação no fluxo de dados, consulte [criando uma transformação síncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)e [criando uma assíncrona Transformação com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Antes de criar o novo componente Script, configure um componente upstream no fluxo de dados para redirecionar linhas para sua saída de erro quando um erro ou truncamento ocorrer. Por motivo de teste, você pode configurar um componente de forma a assegurar que os erros ocorram – por exemplo, configurando uma transformação Pesquisa entre duas tabelas onde a pesquisa vai falhar.  
  
2.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
3.  Conecte a saída de erro do componente upstream ao novo componente Script.  
  
4.  Abra o **Editor de Transformação Scripts** e, na página **Script**, para a propriedade **ScriptLanguage**, selecione a linguagem de script.  
  
5.  Clique em **Editar Script** para abrir o IDE do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) e adicionar o código de exemplo mostrado abaixo.  
  
6.  Feche o VSTA.  
  
7.  No Editor de transformação de Script, sobre o **colunas de entrada** página, selecione a coluna ErrorCode.  
  
8.  Sobre o **entradas e saídas** página, adicione uma nova coluna de saída do tipo `String` chamado **ErrorDescription**. Aumente o comprimento padrão da coluna nova para 255 para suportar mensagens longas.  
  
9. Feche o **Editor de Transformação Scripts**.  
  
10. Anexe a saída do componente Script a um destino satisfatório. Um destino de arquivo simples é o mais fácil de configurar para testar ad hoc.  
  
11. Execute o pacote.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  Row.ErrorDescription = _  
    Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
  Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
    }  
}  
  
```  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**permanecer acima para data com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Tratamento de erro em dados](../data-flow/error-handling-in-data.md)   
 [Usando saídas de erro em um componente de fluxo de dados](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Criar uma transformação síncrona com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  