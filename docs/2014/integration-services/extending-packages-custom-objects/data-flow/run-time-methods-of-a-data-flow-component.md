---
title: Métodos de tempo de execução de um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- run-time [Integration Services]
- data flow components [Integration Services], run-time methods
ms.assetid: fd9e4317-18dd-43af-bbdc-79db32183ac4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b7c5e6a413a2bcf647752d2a1ad4c4f77ac3560b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436943"
---
# <a name="run-time-methods-of-a-data-flow-component"></a>Métodos de tempo de execução de um componente de fluxo de dados
  No tempo de execução, a tarefa de fluxo de dados examina a sequência de componentes, prepara um plano de execução e gerencia um pool de threads de trabalho que executa o plano de trabalho. A tarefa carrega linhas de dados de origens, processa essas linhas através de transformações e as salva em destinos.  
  
## <a name="sequence-of-method-execution"></a>Sequência de execução do método  
 Durante a execução de um componente de fluxo de dados, um subconjunto dos métodos na classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> é chamado. Os métodos e a sequência na qual eles são chamados são sempre os mesmos, com exceção dos métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>. Esses dois métodos são chamados com base na existência e na configuração dos objetos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> de um componente.  
  
 A lista seguinte mostra os métodos na ordem em que são chamados durante a execução do componente. Observe que <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, quando chamado, é sempre chamado antes do <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrepareForExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PostExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Cleanup%2A>  
  
### <a name="primeoutput-method"></a>Método PrimeOutput  
 O método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> é chamado quando um componente tem pelo menos uma saída anexada a um componente downstream por meio de um objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>, e a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> da saída é zero. O método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> é chamado para componentes de origem e para transformações com saídas assíncronas. Ao contrário do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> descrito abaixo, o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> só é chamado uma vez para cada componente que o requer.  
  
### <a name="processinput-method"></a>Método ProcessInput  
 O método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> é chamado para componentes que têm pelo menos uma entrada anexada a um componente upstream por um objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>. O método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> é chamado para componentes de destino e para transformações com saídas síncronas. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> é chamado repetidamente até que não haja mais nenhuma linha para processamento de componentes upstream.  
  
## <a name="working-with-inputs-and-outputs"></a>Funcionando com entradas e saídas  
 Em tempo de execução, componentes de fluxo de dados executam as tarefas seguintes:  
  
-   Componentes de origem adicionam linhas.  
  
-   Componentes de transformação com saídas síncronas recebem linhas fornecidas por componentes de origem.  
  
-   Componentes de transformação com saídas assíncronas recebem linhas e adicionam linhas.  
  
-   Componentes de destino recebem linhas e as carregam em um destino.  
  
 Durante a execução, a tarefa de fluxo de dados aloca objetos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> que contêm todas as colunas definidas nas coleções de colunas de saída de uma sequência de componentes. Por exemplo, se cada um dos quatro componentes em uma sequência de fluxo de dados adicionar uma coluna de saída à sua coleção de colunas de saída, o buffer fornecido a cada componente conterá quatro colunas, uma para cada coluna de saída por componente. Por causa desse comportamento, às vezes um componente recebe buffers que contêm colunas que ele não usa.  
  
 Como os buffers recebidos pelo seu componente podem conter colunas que o componente não vai usar, você deve localizar as colunas que quer usar nas coleções de colunas de entrada e saída do seu componente no buffer fornecido ao componente pela tarefa de fluxo de dados. Para isso, use o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A>. Por razões de desempenho, essa tarefa é executada ordinariamente durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>, em lugar de em <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> ou <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> é chamado antes dos métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>, e é a primeira oportunidade para um componente realizar esse trabalho depois que <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> fica disponível para o componente. Durante esse método, o componente deve localizar suas colunas nos buffers e armazenar essas informações internamente, de forma que as colunas possam ser usadas nos métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> ou <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>.  
  
 O exemplo de código seguinte demonstra como um componente de transformação com uma saída síncrona localiza suas colunas de entrada no buffer durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>.  
  
```csharp  
private int []bufferColumnIndex;  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    bufferColumnIndex = new int[input.InputColumnCollection.Count];  
  
    for( int x=0; x < input.InputColumnCollection.Count; x++)  
    {  
        IDTSInputColumn100 column = input.InputColumnCollection[x];  
        bufferColumnIndex[x] = BufferManager.FindColumnByLineageID( input.Buffer, column.LineageID);  
    }  
}  
```  
  
```vb  
Dim bufferColumnIndex As Integer()  
  
    Public Overrides Sub PreExecute()  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
  
        ReDim bufferColumnIndex(input.InputColumnCollection.Count)  
  
        For x As Integer = 0 To input.InputColumnCollection.Count  
  
            Dim column As IDTSInputColumn100 = input.InputColumnCollection(x)  
            bufferColumnIndex(x) = BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID)  
  
        Next  
  
    End Sub  
```  
  
### <a name="adding-rows"></a>Adicionando linhas  
 Os componentes fornecem linhas a componentes downstream acrescentando linhas aos objetos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer>. A tarefa de fluxo de dados fornece uma matriz de buffers de saída – uma para cada objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> que é conectado a um componente downstream – como um parâmetro para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>. Os componentes de origem e os componentes de transformação com saídas assíncronas acrescentam linhas aos buffers e chamam o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> quando terminam de adicionar linhas. A tarefa de fluxo de dados gerencia os buffers de saída que fornece aos componentes e, quando um buffer fica cheio, automaticamente move as linhas do buffer para o próximo componente. O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> é chamado uma vez por componente, ao contrário do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>, que é chamado repetidamente.  
  
 O exemplo de código seguinte demonstra como um componente acrescenta linhas aos seus buffers de saída durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, em seguida chama o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A>.  
  
```csharp  
public override void PrimeOutput( int outputs, int []outputIDs,PipelineBuffer []buffers)  
{  
    for( int x=0; x < outputs; x++ )  
    {  
        IDTSOutput100 output = ComponentMetaData.OutputCollection.GetObjectByID( outputIDs[x]);  
        PipelineBuffer buffer = buffers[x];  
  
        // TODO: Add rows to the output buffer.  
    }  
    foreach( PipelineBuffer buffer in buffers )  
    {  
        /// Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset();  
    }  
}  
```  
  
```vb  
public overrides sub PrimeOutput( outputs as Integer , outputIDs() as Integer ,buffers() as PipelineBuffer buffers)  
  
    For x As Integer = 0 To outputs.MaxValue  
  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.GetObjectByID(outputIDs(x))  
        Dim buffer As PipelineBuffer = buffers(x)  
  
        ' TODO: Add rows to the output buffer.  
  
    Next  
  
    For Each buffer As PipelineBuffer In buffers  
  
        ' Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset()  
  
    Next  
  
End Sub  
```  
  
 Para obter mais informações sobre o desenvolvimento de componentes que adicionam linhas a buffers de saída, consulte [Desenvolver um componente de origem personalizado](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md) e [Desenvolver um componente de transformação personalizado com saídas assíncronas](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
### <a name="receiving-rows"></a>Recebendo linhas  
 Os componentes recebem linhas de componentes upstream em objetos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer>. A tarefa de fluxo de dados fornece um objeto <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> que contém as linhas adicionadas ao fluxo de dados pelos componentes upstream como um parâmetro para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>. Esse buffer de entrada pode ser usado para examinar e modificar as linhas e colunas no buffer, mas não pode ser usado para adicionar ou remover linhas. O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> é chamado repetidamente até que não haja mais nenhum buffer disponível. Na última vez que é chamado, a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> é `true`. Você pode repetir a coleção de linhas no buffer usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A>, que avança o buffer à próxima linha. Esse método retorna `false` quando o buffer está na última linha da coleção. Não é necessário verificar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A>, a menos que você tenha de executar uma ação adicional depois que as últimas linhas de dados forem processadas.  
  
 O texto abaixo mostra o padrão correto para usar o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> e a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A>:  
  
 `while (buffer.NextRow())`  
  
 `{`  
  
 `// Do something with each row.`  
  
 `}`  
  
 `if (buffer.EndOfRowset)`  
  
 `{`  
  
 `// Optionally, do something after all rows have been processed.`  
  
 `}`  
  
 O exemplo de código a seguir demonstra como um componente processa as linhas em buffers de entrada durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>.  
  
```csharp  
public override void ProcessInput( int inputID, PipelineBuffer buffer )  
{  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
        while( buffer.NextRow())  
        {  
            // TODO: Examine the columns in the current row.  
        }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
        While buffer.NextRow() = True  
  
            ' TODO: Examine the columns in the current row.  
        End While  
  
End Sub  
```  
  
 Para obter mais informações sobre o desenvolvimento de componentes que recebem linhas em buffers de entrada, consulte [Desenvolver um componente de destino personalizado](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md) e [Desenvolver um componente de transformação personalizado com saídas síncronas](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos de tempo de design de um componente de fluxo de dados](design-time-methods-of-a-data-flow-component.md)  
  
  
