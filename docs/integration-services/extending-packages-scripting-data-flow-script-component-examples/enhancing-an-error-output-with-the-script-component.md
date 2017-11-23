---
title: "Aprimorando uma saída de erro com o componente Script | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 3881b57f4089dbb075d019f9bd1a88a96a307b72
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Aprimorando uma saída de erro com o componente Script
  Por padrão, as duas colunas extras em uma [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] saída de erro, ErrorCode e ErrorColumn, só contêm códigos numéricos que representam um número de erro e a ID da coluna na qual ocorreu o erro. Esses valores numéricos podem ter uso limitado sem a descrição de erro correspondente e o nome da coluna.  
  
 Este tópico descreve como adicionar a descrição do erro e o nome da coluna de dados de saída de erro existentes no fluxo de dados usando o componente de Script. O exemplo adiciona a descrição de erro que corresponde a um código de erro específico e predefinido do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> da interface do <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, disponível através da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> do componente Script. Em seguida, o exemplo adiciona o nome da coluna que corresponde à ID de linhagem capturadas usando o <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> método da interface do mesmo.  
  
> [!NOTE]  
>  Se desejar criar um componente que possa ser reutilizado mais facilmente em várias tarefas de fluxo de dados e em vários pacotes, procure utilizar o código deste exemplo de componente Script como o ponto inicial de um componente de fluxo de dados personalizado. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo mostrado aqui usa um componente Script configurado como uma transformação para adicionar a descrição do erro e o nome da coluna de dados de saída de erro existentes no fluxo de dados.  
  
 Para obter mais informações sobre como configurar o componente de Script para usar como uma transformação no fluxo de dados, consulte [criando uma transformação síncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) e [criando uma transformação assíncrona com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Antes de criar o novo componente Script, configure um componente upstream no fluxo de dados para redirecionar linhas para sua saída de erro quando um erro ou truncamento ocorrer. Por motivo de teste, você pode configurar um componente de forma a assegurar que os erros ocorram – por exemplo, configurando uma transformação Pesquisa entre duas tabelas onde a pesquisa vai falhar.  
  
2.  Adicione um novo componente Script à superfície de designer Fluxo de Dados e configure-o como uma transformação.  
  
3.  Conecte a saída de erro do componente upstream ao novo componente Script.  
  
4.  Abra o **Editor de transformação scripts**e na **Script** página, para o **ScriptLanguage** propriedade, selecione a linguagem de script.  
  
5.  Clique em **Editar Script** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE e adicione o código de exemplo mostrado abaixo.  
  
6.  Feche o VSTA.  
  
7.  No Editor de transformação de Script, sobre o **colunas de entrada** página, selecione as colunas ErrorCode e ErrorColumn.  
  
8.  Sobre o **entradas e saídas** página, adicione duas novas colunas.  
  
    -   Adicionar uma nova coluna de saída do tipo **cadeia de caracteres** chamado **ErrorDescription**. Aumente o comprimento padrão da coluna nova para 255 para suportar mensagens longas.  
  
    -   Adicione outra nova coluna de saída do tipo **cadeia de caracteres** chamado **ColumnName**. Aumente o tamanho padrão da coluna nova para 255 para suportar valores longos.  
  
9. Fechar o **Editor de transformação scripts.**  
  
10. Anexe a saída do componente Script a um destino satisfatório. Um destino de arquivo simples é o mais fácil de configurar para testar ad hoc.  
  
11. Execute o pacote.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription = _  
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
      Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)  
      If componentMetaData130 IsNot Nothing Then  
        Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)  
         End If  
  
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
  
      var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;  
      if (componentMetaData130 != null)  
        {  
            Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);  
        }  
  
    }  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)   
 [Usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Criando uma transformação síncrona com o componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  

