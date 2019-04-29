---
title: Desenvolver um componente de transformação personalizado com saídas assíncronas | Microsoft Docs
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
- custom data flow components [Integration Services], transformation components
- asynchronous outputs [Integration Services]
- ProcessInput method
- cache [Integration Services]
- buffer allocations [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], transformation components
ms.assetid: 1c3e92c7-a4fa-4fdd-b9ca-ac3069536274
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5bb52fc5c8a3789cc945a2ea850d0849335917e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896627"
---
# <a name="developing-a-custom-transformation-component-with-asynchronous-outputs"></a>Desenvolvendo um componente de transformação personalizado com saídas assíncronas
  Você usa um componente com saídas assíncronas quando uma transformação só consegue liberar linhas depois de o componente receber todas as suas linhas de saída, ou quando a transformação não gera exatamente uma linha de saída para cada linha recebida como entrada. Por exemplo, a transformação Agregação só consegue calcular uma soma em linhas depois de ler todas as linhas. Em contraste, você pode usar um componente com saídas síncronas a qualquer momento quando modifica cada linha de dados percorrida por ele. Você pode modificar os dados de cada linha estabelecida, ou criar uma ou mais colunas novas, cada qual com um valor para cada linha de entrada. Para obter mais informações sobre a diferença entre componentes síncronos e assíncronos, consulte [Compreender as transformações síncronas e assíncronas](../understanding-synchronous-and-asynchronous-transformations.md).  
  
 Componentes de transformação com saídas assíncronas são exclusivos pois agem como componentes de destino e de origem. Esse tipo de componente recebe linhas de componentes upstream e adiciona linhas que são consumidas por componentes downstream. Nenhum outro componente de fluxo de dados executa essas duas operações.  
  
 As colunas de componentes upstream que estão disponíveis para um componente com saídas síncronas estão automaticamente disponíveis para componentes downstream. Portanto, um componente com saídas síncronas não precisa definir colunas de saída para fornecer colunas e linhas ao próximo componente. Por outro lado, componentes com saídas assíncronas precisam definir colunas de saída e fornecer linhas a componentes downstream. Portanto, um componente com saídas assíncronas precisa executar mais tarefas durante o tempo de design e execução, e o desenvolvedor de componentes precisa implementar mais códigos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contém várias transformações com saídas assíncronas. Por exemplo, a transformação Classificação precisa de todas as linhas para poder classificá-las, e consegue isso através de saídas assíncronas. Depois de receber todas as linhas, ela as classifica e as adiciona à sua saída.  
  
 Essa seção explica detalhadamente como desenvolver transformações com saídas assíncronas. Para obter mais informações sobre o desenvolvimento de componentes de origem, consulte [Desenvolver um componente de origem personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md).  
  
## <a name="design-time"></a>Tempo de design  
  
### <a name="creating-the-component"></a>Criando o componente  
 A propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> do objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> identifica se uma saída é síncrona ou assíncrona. Para criar uma saída assíncrona, adicione a saída ao componente e defina o <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> como zero. A definição dessa propriedade também determina se a tarefa de fluxo de dados aloca objetos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> parar a entrada e a saída do componente, ou se um único buffer é alocado e compartilhado entre os dois objetos.  
  
 O código de exemplo a seguir mostra um componente que cria uma saída assíncrona em sua implementação <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>.  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "AsyncComponent",ComponentType = ComponentType.Transform)]  
    public class AsyncComponent : PipelineComponent  
    {  
        public override void ProvideComponentProperties()  
        {  
            // Call the base class, which adds a synchronous input  
            // and output.  
            base.ProvideComponentProperties();  
  
            // Make the output asynchronous.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
            output.SynchronousInputID = 0;  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="AsyncComponent", ComponentType:=ComponentType.Transform)> _  
Public Class AsyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Call the base class, which adds a synchronous input  
        ' and output.  
        Me.ProvideComponentProperties()  
  
        ' Make the output asynchronous.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
        output.SynchronousInputID = 0  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>Criando e configurando colunas de saída  
 Conforme mencionado antes, um componente assíncrono adiciona colunas à sua coleção de colunas de saída para fornecer colunas a componentes downstream. Você pode escolher entre vários métodos de tempo de design, de acordo com as necessidades do componente. Por exemplo, para passar todas as colunas dos componentes upstream para os componentes downstream, substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.OnInputPathAttached%2A> para adicionar as colunas, pois esse é o primeiro método em que as colunas de entrada estão disponíveis para o componente.  
  
 Se o componente criar colunas de saída com base nas colunas selecionadas para sua entrada, substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetUsageType%2A> para selecionar as colunas de saída e indicar como elas serão utilizadas.  
  
 Se um componente com saídas assíncronas criar colunas de saída com base nas colunas de componentes upstream e houver alterações nas colunas upstream disponíveis, o componente deverá atualizar sua coleção de colunas de saída. Essas alterações devem ser detectadas pelo componente durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> e corrigidas durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>.  
  
> [!NOTE]  
>  Quando uma coluna de saída é removida da coleção de colunas de saída, os componentes downstream do fluxo de dados que referenciam a coluna são afetados negativamente. A coluna de saída deve ser reparada sem remover e recriar a coluna para impedir a quebra de componentes downstream. Por exemplo, se o tipo de dados da coluna for alterado, atualize-o.  
  
 O exemplo de código a seguir mostra um componente que adiciona uma coluna de saída à sua coleção de colunas de saída; esse procedimento ocorre em cada coluna disponível do componente upstream.  
  
```csharp  
public override void OnInputPathAttached(int inputID)  
{  
   IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
   IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
   IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
   foreach (IDTSVirtualInputColumn100 vCol in vInput.VirtualInputColumnCollection)  
   {  
      IDTSOutputColumn100 outCol = output.OutputColumnCollection.New();  
      outCol.Name = vCol.Name;  
      outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage);  
   }  
}  
```  
  
```vb  
Public Overrides Sub OnInputPathAttached(ByVal inputID As Integer)  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
    Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput()  
  
    For Each vCol As IDTSVirtualInputColumn100 In vInput.VirtualInputColumnCollection  
  
        Dim outCol As IDTSOutputColumn100 = output.OutputColumnCollection.New()  
        outCol.Name = vCol.Name  
        outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage)  
  
    Next  
End Sub  
```  
  
## <a name="run-time"></a>Tempo de execução  
 Componentes com saídas assíncronas também executam, em tempo de execução, uma sequência diferente de métodos que outros tipos de componentes. Primeiro, eles são os únicos componentes que recebem uma chamada para os métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>. Componentes com saídas assíncronas também precisam de acesso a todas as linhas recebidas para poder começar o processamento; portanto, eles precisam armazenar as linhas de entrada em cache internamente até a conclusão da leitura de todas as linhas. Finalmente, diferente de outros componentes, os componentes com saídas assíncronas recebem um buffer de entrada e um buffer de saída.  
  
### <a name="understanding-the-buffers"></a>Compreendendo os buffers  
 O componente recebe o buffer de entrada durante <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>. Esse buffer contém as linhas adicionadas ao buffer por componentes upstream. O buffer também contém as colunas de entrada do componente, além das colunas fornecidas na saída de um componente upstream, mas não adicionadas à coleção de entradas do componente assíncrono.  
  
 O buffer de saída, que é fornecido ao componente em <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, não contém linhas inicialmente. O componente adiciona linhas a esse buffer e fornece o buffer a componentes downstream quando está cheio. O buffer de saída contém as colunas definidas na coleção de colunas de saída do componente, além de quaisquer colunas adicionadas por outros componentes downstream às suas saídas.  
  
 Os componentes com saídas síncronas se comportam de maneira diferente, pois recebem um único buffer compartilhado. O buffer compartilhado de um componente com saídas síncronas contém as colunas de entrada e saída do componente, além das colunas adicionadas às saídas dos componentes upstream e downstream.  
  
### <a name="processing-rows"></a>Processando linhas  
  
#### <a name="caching-input-rows"></a>Armazenando linhas de entrada em cache  
 Ao escrever um componente com saídas assíncronas, você tem três opções para adicionar linhas ao buffer de saída. Você pode adicioná-las à medida que recebe linhas de entrada, armazená-las em cache até o componente receber todas as linhas do componente upstream ou adicioná-las quando for apropriado fazer isso para o componente. O método escolhido depende dos requisitos do componente. Por exemplo, o componente Classificação exige que todas as linhas upstream sejam recebidas antes de sua classificação. Portanto, ele aguarda a leitura de todas as linhas para poder adicioná-las ao buffer de saída.  
  
 O componente deve armazenar em cache, internamente, as linhas recebidas no buffer de entrada, como preparação para processá-las. As linhas de buffer de entrada podem ser armazenadas em cache em uma tabela de dados, em uma matriz multidimensional ou em qualquer outra estrutura interna.  
  
#### <a name="adding-output-rows"></a>Adicionando linhas de saída  
 Independentemente de adicionar linhas ao buffer de saída durante ou depois do recebimento de todas as linhas, você faz isso através do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> no buffer de saída. Depois de adicionar a linha, defina os valores de cada coluna na linha nova.  
  
 Como às vezes há mais colunas no buffer de saída do que na coleção de colunas de saída do componente, localize o índice da coluna apropriada no buffer antes de definir seu valor. O método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> retorna o índice da coluna na linha do buffer com o ID de linhagem especificado, que é utilizado para atribuir o valor à coluna do buffer.  
  
 O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>, que é chamado antes do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> ou do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>, é o primeiro método em que a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> está disponível, e a primeira oportunidade de localizar os índices das colunas nos buffers de entrada e saída.  
  
## <a name="sample"></a>Amostra  
 O exemplo a seguir mostra um componente de transformação simples com saídas assíncronas que adiciona linhas ao buffer de saída à medida que as recebe. Esse exemplo não demonstra todos os métodos e todas as funcionalidades discutidas nesse tópico. Ele demonstra os métodos importantes que todo componente de transformação personalizado com saídas assíncronas deve substituir, mas não contém código para a validação em tempo de design. Além disso, o código em <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> pressupõe que a coleção de colunas de saída contém uma coluna relativa a cada coluna da coleção de colunas de entrada.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
   [DtsPipelineComponent(DisplayName = "AsynchronousOutput")]  
   public class AsynchronousOutput : PipelineComponent  
   {  
      PipelineBuffer outputBuffer;  
      int[] inputColumnBufferIndexes;  
      int[] outputColumnBufferIndexes;  
  
      public override void ProvideComponentProperties()  
      {  
         // Let the base class add the input and output objects.  
         base.ProvideComponentProperties();  
  
         // Name the input and output, and make the  
         // output asynchronous.  
         ComponentMetaData.InputCollection[0].Name = "Input";  
         ComponentMetaData.OutputCollection[0].Name = "AsyncOutput";  
         ComponentMetaData.OutputCollection[0].SynchronousInputID = 0;  
      }  
      public override void PreExecute()  
      {  
         IDTSInput100 input = ComponentMetaData.InputCollection[0];  
         IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
         inputColumnBufferIndexes = new int[input.InputColumnCollection.Count];  
         outputColumnBufferIndexes = new int[output.OutputColumnCollection.Count];  
  
         for (int col = 0; col < input.InputColumnCollection.Count; col++)  
            inputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection[col].LineageID);  
  
         for (int col = 0; col < output.OutputColumnCollection.Count; col++)  
            outputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[col].LineageID);  
  
      }  
  
      public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
      {  
         if (buffers.Length != 0)  
            outputBuffer = buffers[0];  
      }  
      public override void ProcessInput(int inputID, PipelineBuffer buffer)  
      {  
            // Advance the buffer to the next row.  
            while (buffer.NextRow())  
            {  
               // Add a row to the output buffer.  
               outputBuffer.AddRow();  
               for (int x = 0; x < inputColumnBufferIndexes.Length; x++)  
               {  
                  // Copy the data from the input buffer column to the output buffer column.  
                  outputBuffer[outputColumnBufferIndexes[x]] = buffer[inputColumnBufferIndexes[x]];  
               }  
            }  
         if (buffer.EndOfRowset)  
         {  
            // EndOfRowset on the input buffer is true.  
            // Set EndOfRowset on the output buffer.  
            outputBuffer.SetEndOfRowset();  
         }  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
Namespace Microsoft.Samples.SqlServer.Dts  
  
    <DtsPipelineComponent(DisplayName:="AsynchronousOutput")> _  
    Public Class AsynchronousOutput  
  
        Inherits PipelineComponent  
  
        Private outputBuffer As PipelineBuffer  
        Private inputColumnBufferIndexes As Integer()  
        Private outputColumnBufferIndexes As Integer()  
  
        Public Overrides Sub ProvideComponentProperties()  
  
            ' Let the base class add the input and output objects.  
            Me.ProvideComponentProperties()  
  
            ' Name the input and output, and make the  
            ' output asynchronous.  
            ComponentMetaData.InputCollection(0).Name = "Input"  
            ComponentMetaData.OutputCollection(0).Name = "AsyncOutput"  
            ComponentMetaData.OutputCollection(0).SynchronousInputID = 0  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
            Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
            ReDim inputColumnBufferIndexes(input.InputColumnCollection.Count)  
            ReDim outputColumnBufferIndexes(output.OutputColumnCollection.Count)  
  
            For col As Integer = 0 To input.InputColumnCollection.Count  
                inputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection(col).LineageID)  
            Next  
  
            For col As Integer = 0 To output.OutputColumnCollection.Count  
                outputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(col).LineageID)  
            Next  
  
        End Sub  
        Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())  
  
            If buffers.Length <> 0 Then  
                outputBuffer = buffers(0)  
            End If  
  
        End Sub  
  
        Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
                ' Advance the buffer to the next row.  
                While (buffer.NextRow())  
  
                    ' Add a row to the output buffer.  
                    outputBuffer.AddRow()  
                    For x As Integer = 0 To inputColumnBufferIndexes.Length  
  
                        ' Copy the data from the input buffer column to the output buffer column.  
                        outputBuffer(outputColumnBufferIndexes(x)) = buffer(inputColumnBufferIndexes(x))  
  
                    Next  
                End While  
  
            If buffer.EndOfRowset = True Then  
                ' EndOfRowset on the input buffer is true.  
                ' Set the end of row set on the output buffer.  
                outputBuffer.SetEndOfRowset()  
            End If  
        End Sub  
    End Class  
End Namespace  
```  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver um componente de transformação personalizado com saídas síncronas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [Compreender as transformações síncronas e assíncronas](../understanding-synchronous-and-asynchronous-transformations.md)   
 [Criar uma transformação assíncrona com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
