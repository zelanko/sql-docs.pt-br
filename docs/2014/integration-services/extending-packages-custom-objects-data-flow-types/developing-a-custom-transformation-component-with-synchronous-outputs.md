---
title: Desenvolver um componente de transformação personalizado com saídas síncronas | Microsoft Docs
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
- ProcessInput method
- buffer allocations [Integration Services]
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- data flow components [Integration Services], transformation components
ms.assetid: b694d21f-9919-402d-9192-666c6449b0b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 785ca6c05bc221e1449607b9dc3deaa93aa667bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896578"
---
# <a name="developing-a-custom-transformation-component-with-synchronous-outputs"></a>Desenvolvendo um componente de transformação personalizado com saídas síncronas
  Os componentes de transformação com saídas síncronas recebem linhas de componentes upstream e leem ou modificam os valores das colunas dessas linhas à medida que passam as linhas para os componentes downstream. Eles também podem definir colunas de saída adicionais derivadas das colunas fornecidas pelos componentes upstream, mas não acrescentam linhas ao fluxo de dados. Para obter mais informações sobre a diferença entre componentes síncronos e assíncronos, consulte [Compreender as transformações síncronas e assíncronas](../understanding-synchronous-and-asynchronous-transformations.md).  
  
 Esse tipo de componente é adequado para tarefas em que os dados são modificados em linha, à medida que são fornecidos ao componente, e o componente não tem que ver todas as linhas antes de processá-las. É o componente mais fácil a desenvolver por que as transformações com saídas síncronas em geral não se conectam a fontes de dados externas, gerenciam colunas de metadados externas ou adicionam linhas a buffers de saída.  
  
 Criar um componente de transformação com saídas síncronas envolve adicionar um <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> contendo as colunas upstream selecionadas para o componente, e um objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> que podem conter colunas derivadas criadas pelo componente. Também inclui a implementação de métodos de tempo de design e o fornecimento de um código que leia ou modifique as colunas nas linhas do buffer de entrada durante a execução.  
  
 Esta seção fornece as informações necessárias para implementar um componente de transformação personalizado e fornece exemplos de códigos para ajudar você a entender melhor os conceitos.  
  
## <a name="design-time"></a>Tempo de design  
 O código do tempo de design desse componente envolve a criação de entradas e saídas, a adição de qualquer coluna de saída adicional que o componente gere e a validação da configuração do componente.  
  
### <a name="creating-the-component"></a>Criando o componente  
 As entradas, saídas e propriedades personalizadas do componente normalmente são criadas durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>. Há dois modos de adicionar a entrada e a saída de um componente de transformação com saídas síncronas. Você pode usar a implementação da classe base do método e modificar a entrada e a saída padrão que ele cria, ou adicionar explicitamente a entrada e a saída.  
  
 O exemplo de código a seguir mostra uma implementação de <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> que explicitamente adiciona os objetos de entrada e saída. A chamada para a classe base que realizaria a mesma função é incluída em um comentário.  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SynchronousComponent", ComponentType = ComponentType.Transform)]  
    public class SyncComponent : PipelineComponent  
    {  
  
        public override void ProvideComponentProperties()  
        {  
            // Add the input.  
            IDTSInput100 input = ComponentMetaData.InputCollection.New();  
            input.Name = "Input";  
  
            // Add the output.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
            output.Name = "Output";  
            output.SynchronousInputID = input.ID;  
  
            // Alternatively, you can let the base class add the input and output  
            // and set the SynchronousInputID of the output to the ID of the input.  
            // base.ProvideComponentProperties();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="SynchronousComponent", ComponentType:=ComponentType.Transform)> _  
Public Class SyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Add the input.  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New()  
        input.Name = "Input"  
  
        ' Add the output.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()  
        output.Name = "Output"  
        output.SynchronousInputID = Input.ID  
  
        ' Alternatively, you can let the base class add the input and output  
        ' and set the SynchronousInputID of the output to the ID of the input.  
        ' base.ProvideComponentProperties();  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>Criando e configurando colunas de saída  
 Embora componentes de transformação com saídas síncronas não acrescentem linhas a buffers, eles podem acrescentar colunas de saída extras à sua saída. Normalmente, quando um componente adiciona uma coluna de saída, os valores dessa nova coluna são derivados em tempo de execução dos dados contidos em uma ou mais das colunas fornecidas ao componente por um componente upstream.  
  
 Depois que uma coluna de saída foi criada, suas propriedades de tipo de dados devem ser definidas. Definir as propriedades de tipo de dados de uma coluna de saída requer manipulação especial e é executado chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A>. Esse método é necessário por que as propriedades <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> são individualmente somente leitura, porque cada uma delas depende das configurações da outra. Esse método garante que os valores das propriedades sejam definidos de forma consistente, e a tarefa de fluxo de dados valida se eles foram definidos corretamente.  
  
 O <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> da coluna determina os valores que são definidos para as outras propriedades. A tabela a seguir mostra os requisitos nas propriedades dependentes para cada <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>. Os tipos de dados não listados têm as propriedades dependentes definidas como zero.  
  
|DataType|Comprimento|Escala|Precisão|CodePage|  
|--------------|------------|-----------|---------------|--------------|  
|DT_DECIMAL|0|Maior que 0 e menor ou igual a 28.|0|0|  
|DT_CY|0|0|0|0|  
|DT_NUMERIC|0|Maior que 0 e menor ou igual a 28, e menor que a Precisão.|Maior ou igual a 1 e menor ou igual a 38.|0|  
|DT_BYTES|Maior que 0.|0|0|0|  
|DT_STR|Maior que 0 e menor que 8000.|0|0|Não 0 e uma página de código válida.|  
|DT_WSTR|Maior que 0 e menor que 4.000.|0|0|0|  
  
 Como as restrições nas propriedades de tipo de dados são baseadas no tipo de dados da coluna de saída, você deve escolher o tipo de dados correto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando trabalha com tipos gerenciados. A classe base fornece três métodos auxiliares, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>, que auxiliam desenvolvedores de componente gerenciados a selecionar um tipo de dados do [!INCLUDE[ssIS](../../includes/ssis-md.md)] que recebeu um tipo gerenciado. Esses métodos convertem tipos de dados gerenciados em tipos de dados do [!INCLUDE[ssIS](../../includes/ssis-md.md)] e vice-versa.  
  
## <a name="run-time"></a>Tempo de execução  
 Geralmente, a implementação da parte de tempo de execução do componente é categorizada em duas tarefas – localizar as colunas de entrada e saída do componente no buffer e ler ou escrever os valores dessas colunas nas linhas de entrada do buffer.  
  
### <a name="locating-columns-in-the-buffer"></a>Localizando colunas no buffer  
 O número de colunas nos buffers fornecido a um componente durante a execução provavelmente excederá o número de colunas nas coleções de entrada ou saída do componente. Isso se dá por que cada buffer contém todas as colunas de saída definidas nos componentes em um fluxo de dados. Para que as colunas do buffer sejam corretamente associadas às colunas da entrada ou da saída, os desenvolvedores de componentes devem usar o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A>. Esse método localiza uma coluna no buffer especificado por sua ID de linhagem. Normalmente, são localizadas colunas durante <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> por que este é o primeiro método de tempo de execução em que a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> fica disponível.  
  
 O exemplo de código seguinte mostra um componente que localiza índices das colunas em sua coleção de colunas de entrada e saída durante <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>. Os índices da coluna são armazenados em uma matriz de inteiro e podem ser acessados pelo componente durante <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>.  
  
```csharp  
int []inputColumns;  
int []outputColumns;  
  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    inputColumns = new int[input.InputColumnCollection.Count];  
    outputColumns = new int[output.OutputColumnCollection.Count];  
  
    for(int col=0; col < input.InputColumnCollection.Count; col++)  
    {  
        IDTSInputColumn100 inputColumn = input.InputColumnCollection[col];  
        inputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID);  
    }  
  
    for(int col=0; col < output.OutputColumnCollection.Count; col++)  
    {  
        IDTSOutputColumn100 outputColumn = output.OutputColumnCollection[col];  
        outputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID);  
    }  
  
}  
```  
  
```vb  
Public Overrides Sub PreExecute()  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    ReDim inputColumns(input.InputColumnCollection.Count)  
    ReDim outputColumns(output.OutputColumnCollection.Count)  
  
    For col As Integer = 0 To input.InputColumnCollection.Count  
  
        Dim inputColumn As IDTSInputColumn100 = input.InputColumnCollection(col)  
        inputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID)  
    Next  
  
    For col As Integer = 0 To output.OutputColumnCollection.Count  
  
        Dim outputColumn As IDTSOutputColumn100 = output.OutputColumnCollection(col)  
        outputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID)  
    Next  
  
End Sub  
```  
  
### <a name="processing-rows"></a>Processando linhas  
 Componentes recebem objetos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> que contêm linhas e colunas no método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>. Durante esse método são iteradas as linhas do buffer e as colunas identificadas durante <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> são lidas e modificadas. O método é chamado repetidamente pela tarefa de fluxo de dados até que nenhuma linha seja mais fornecida a partir do componente upstream.  
  
 Uma coluna individual no buffer é lida ou gravada através do método de acesso do indexador matriz ou um dos métodos `Get` ou `Set`. Os métodos `Get` e `Set` são mais eficientes e devem ser usados quando o tipo de dados da coluna no buffer for conhecido.  
  
 O exemplo de código seguinte mostra uma implementação do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> que processa linhas de entrada.  
  
```csharp  
public override void ProcessInput( int InputID, PipelineBuffer buffer)  
{  
       while( buffer.NextRow())  
       {  
            for(int x=0; x < inputColumns.Length;x++)  
            {  
                if(!buffer.IsNull(inputColumns[x]))  
                {  
                    object columnData = buffer[inputColumns[x]];  
                    // TODO: Modify the column data.  
                    buffer[inputColumns[x]] = columnData;  
                }  
            }  
  
      }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal InputID As Integer, ByVal buffer As PipelineBuffer)  
  
        While (buffer.NextRow())  
  
            For x As Integer = 0 To inputColumns.Length  
  
                if buffer.IsNull(inputColumns(x)) = false then  
  
                    Dim columnData As Object = buffer(inputColumns(x))  
                    ' TODO: Modify the column data.  
                    buffer(inputColumns(x)) = columnData  
  
                End If  
            Next  
  
        End While  
End Sub  
```  
  
## <a name="sample"></a>Amostra  
 O exemplo seguinte mostra um componente de transformação simples com saídas síncronas que converte os valores de todas as colunas de cadeia de caracteres para escrever em letra maiúscula. Esse exemplo não demonstra todos os métodos e todas as funcionalidades discutidas nesse tópico. Ele demonstra os métodos importantes que todo componente de transformação personalizado com saídas síncronas deve substituir, mas não contém código para a validação em tempo de design.  
  
```csharp  
using System;  
using System.Collections;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Uppercase  
{  
  [DtsPipelineComponent(DisplayName = "Uppercase")]  
  public class Uppercase : PipelineComponent  
  {  
    ArrayList m_ColumnIndexList = new ArrayList();  
  
    public override void ProvideComponentProperties()  
    {  
      base.ProvideComponentProperties();  
      ComponentMetaData.InputCollection[0].Name = "Uppercase Input";  
      ComponentMetaData.OutputCollection[0].Name = "Uppercase Output";  
    }  
  
    public override void PreExecute()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection[0];  
      IDTSInputColumnCollection100 inputColumns = input.InputColumnCollection;  
  
      foreach (IDTSInputColumn100 column in inputColumns)  
      {  
        if (column.DataType == DataType.DT_STR || column.DataType == DataType.DT_WSTR)  
        {  
          m_ColumnIndexList.Add((int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID));  
        }  
      }  
    }  
  
    public override void ProcessInput(int inputID, PipelineBuffer buffer)  
    {  
      while (buffer.NextRow())  
      {  
        foreach (int columnIndex in m_ColumnIndexList)  
        {  
          string str = buffer.GetString(columnIndex);  
          buffer.SetString(columnIndex, str.ToUpper());  
        }  
      }  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.Collections   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper   
Namespace Uppercase   
  
 <DtsPipelineComponent(DisplayName="Uppercase")> _   
 Public Class Uppercase   
 Inherits PipelineComponent   
   Private m_ColumnIndexList As ArrayList = New ArrayList   
  
   Public  Overrides Sub ProvideComponentProperties()   
     MyBase.ProvideComponentProperties   
     ComponentMetaData.InputCollection(0).Name = "Uppercase Input"   
     ComponentMetaData.OutputCollection(0).Name = "Uppercase Output"   
   End Sub   
  
   Public  Overrides Sub PreExecute()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
     Dim inputColumns As IDTSInputColumnCollection100 = input.InputColumnCollection   
     For Each column As IDTSInputColumn100 In inputColumns   
       If column.DataType = DataType.DT_STR OrElse column.DataType = DataType.DT_WSTR Then   
         m_ColumnIndexList.Add(CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer))   
       End If   
     Next   
   End Sub   
  
   Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
     While buffer.NextRow   
       For Each columnIndex As Integer In m_ColumnIndexList   
         Dim str As String = buffer.GetString(columnIndex)   
         buffer.SetString(columnIndex, str.ToUpper)   
       Next   
     End While   
   End Sub   
 End Class   
End Namespace  
```  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)   
 [Compreender as transformações síncronas e assíncronas](../understanding-synchronous-and-asynchronous-transformations.md)   
 [Criar uma transformação síncrona com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
