---
title: Desenvolvendo um componente de destino personalizado | Microsoft Docs
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
- validation [Integration Services], components
- destinations [Integration Services], components
- ProcessInput method
- external data sources [Integration Services]
- custom data flow components [Integration Services], destination components
- data flow components [Integration Services], destination components
ms.assetid: 24619363-9535-4c0e-8b62-1d22c6630e40
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f090cd6dbfaa0194bc02af581fc4765fca9eac0b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382334"
---
# <a name="developing-a-custom-destination-component"></a>Desenvolvendo um componente de destino personalizado
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite que os desenvolvedores escrevam componentes de destino personalizados que podem conectar e armazenar dados em qualquer fonte de dados personalizada. Os componentes de destino personalizados são úteis quando você precisa se conectar a fontes de dados que não podem ser acessadas através de um dos componentes de origem existentes incluídos no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Os componentes de destino têm uma ou mais entradas e zero saídas. Em tempo de design, eles criam e configuram conexões e metadados de coluna de leitura a partir da fonte de dados externa. Durante a execução, eles se conectam à fonte de dados externa e adicionam linhas que são recebidas dos componentes upstream do fluxo de dados para a fonte de dados externa. Se a fonte de dados externa existir antes da execução do componente, o componente de destino também deverá verificar se os tipos de dados das colunas recebidas pelo componente coincidem com os tipos de dados das colunas da fonte de dados externa.  
  
 Essa seção discute os detalhes de como desenvolver componentes de destino e fornece exemplos de código para esclarecer conceitos importantes. Para obter uma visão geral do desenvolvimento de componentes de fluxo de dados, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="design-time"></a>Tempo de design  
 A implementação da funcionalidade em tempo de design de um componente de destino envolve a especificação de uma conexão a uma fonte de dados externa e a confirmação de que o componente foi configurado corretamente. Por definição, um componente de destino tem uma entrada e possivelmente uma saída de erro.  
  
### <a name="creating-the-component"></a>Criando o componente  
 Os componentes de destino se conectam a fontes de dados externas através de objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> definidos em um pacote. O componente de destino indica seu requisito de um gerenciador de conexões para o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] e para usuários do componente, adicionando um elemento à coleção <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>. Essa coleção tem duas finalidades: primeiro, ela transmite a necessidade de um gerenciador de conexões para o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]; segundo, depois de o usuário selecionar ou criar um gerenciador de conexões, ele mantém uma referência a esse gerenciador no pacote em uso pelo componente. Quando um <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> é adicionado à coleção, o **Editor Avançado** exibe a guia **Propriedades da Conexão** para solicitar que o usuário selecione ou crie uma conexão no pacote a ser usado pelo componente.  
  
 O exemplo de código a seguir mostra uma implementação do <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> que adiciona uma entrada e, depois, um objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> ao <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "Destination Component",ComponentType =ComponentType.DestinationAdapter)]  
    public class DestinationComponent : PipelineComponent   
    {  
        public override void ProvideComponentProperties()  
        {  
            // Reset the component.  
            base.RemoveAllInputsOutputsAndCustomProperties();  
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll();  
  
            IDTSInput100 input = ComponentMetaData.InputCollection.New();  
            input.Name = "Input";  
  
            IDTSRuntimeConnection100 connection = ComponentMetaData.RuntimeConnectionCollection.New();  
            connection.Name = "ADO.net";  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Namespace Microsoft.Samples.SqlServer.Dts  
  
    <DtsPipelineComponent(DisplayName:="Destination Component", ComponentType:=ComponentType.DestinationAdapter)> _  
    Public Class DestinationComponent  
        Inherits PipelineComponent  
  
        Public Overrides Sub ProvideComponentProperties()  
  
            ' Reset the component.  
            Me.RemoveAllInputsOutputsAndCustomProperties()  
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll()  
  
            Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New()  
            input.Name = "Input"  
  
            Dim connection As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New()  
            connection.Name = "ADO.net"  
  
        End Sub  
    End Class  
End Namespace  
```  
  
### <a name="connecting-to-an-external-data-source"></a>Conectando-se a uma fonte de dados externa  
 Depois da adição de uma conexão ao <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>, substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> para estabelecer uma conexão à fonte de dados externa. Esse método é chamado em tempo de design e em tempo de execução. O componente deve estabelecer uma conexão com o gerenciador de conexões especificado pela conexão em tempo de execução e, depois, com a fonte de dados externa. Depois de concluir essas conexões, o componente deverá armazenar a conexão em cache internamente e liberá-la quando o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> for chamado. Os desenvolvedores substituem esse método e liberam a conexão estabelecida pelo componente durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>. Esses dois métodos, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>, são chamados em tempo de design e em tempo de execução.  
  
 O exemplo de código a seguir mostra um componente que se conecta a uma conexão ADO.NET no método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> e, depois, fecha a conexão no <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>.  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
private SqlConnection sqlConnection;  
  
public override void AcquireConnections(object transaction)  
{  
    if (ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager != null)  
    {  
        ConnectionManager cm = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager);  
        ConnectionManagerAdoNet cmado = cm.InnerObject as ConnectionManagerAdoNet;  
  
        if (cmado == null)  
            throw new Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.");  
  
        sqlConnection = cmado.AcquireConnection(transaction) as SqlConnection;  
        sqlConnection.Open();  
    }  
}  
  
public override void ReleaseConnections()  
{  
    if (sqlConnection != null && sqlConnection.State != ConnectionState.Closed)  
        sqlConnection.Close();  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
Private sqlConnection As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal transaction As Object)  
  
    If IsNothing(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager) = False Then  
  
        Dim cm As ConnectionManager = DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager)  
        Dim cmado As ConnectionManagerAdoNet = CType(cm.InnerObject,ConnectionManagerAdoNet)  
  
        If IsNothing(cmado) Then  
            Throw New Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.")  
        End If  
  
        sqlConnection = CType(cmado.AcquireConnection(transaction), SqlConnection)  
        sqlConnection.Open()  
  
    End If  
End Sub  
  
Public Overrides Sub ReleaseConnections()  
  
    If IsNothing(sqlConnection) = False And sqlConnection.State <> ConnectionState.Closed Then  
        sqlConnection.Close()  
    End If  
  
End Sub  
```  
  
### <a name="validating-the-component"></a>Validando o componente  
 Os desenvolvedores de componentes de destino devem executar a validação conforme descrito em [Validação de Componente](../extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md). Além disso, eles devem verificar se as propriedades do tipo de dados das colunas definidas na coleção de colunas de entrada do componente coincidem com as das colunas da fonte de dados externa. Às vezes, a verificação de colunas de entrada em relação à fonte de dados externa pode ser impossível ou indesejável. Isso ocorre, por exemplo, quando o componente ou o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] se encontra desconectado ou quando viagens de ida e volta ao servidor são inaceitáveis. Nessas situações, as colunas da coleção de colunas de entrada podem ser validadas através do objeto de entrada <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.ExternalMetadataColumnCollection%2A>.  
  
 Essa coleção existe nos objetos de entrada e saída e precisa ser preenchida pelo desenvolvedor de componentes a partir das colunas da fonte de dados externa. Essa coleção pode ser usada para validar as colunas de entrada quando o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] está offline, quando o componente está desconectado ou quando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> é `false`.  
  
 O código de exemplo a seguir adiciona uma coluna de metadados externa com base em uma coluna de entrada existente.  
  
```csharp  
private void AddExternalMetaDataColumn(IDTSInput100 input,IDTSInputColumn100 inputColumn)  
{  
    // Set the properties of the external metadata column.  
    IDTSExternalMetadataColumn100 externalColumn = input.ExternalMetadataColumnCollection.New();  
    externalColumn.Name = inputColumn.Name;  
    externalColumn.Precision = inputColumn.Precision;  
    externalColumn.Length = inputColumn.Length;  
    externalColumn.DataType = inputColumn.DataType;  
    externalColumn.Scale = inputColumn.Scale;  
  
    // Map the external column to the input column.  
    inputColumn.ExternalMetadataColumnID = externalColumn.ID;  
}  
```  
  
```vb  
Private Sub AddExternalMetaDataColumn(ByVal input As IDTSInput100, ByVal inputColumn As IDTSInputColumn100)  
  
    ' Set the properties of the external metadata column.  
    Dim externalColumn As IDTSExternalMetadataColumn100 = input.ExternalMetadataColumnCollection.New()  
    externalColumn.Name = inputColumn.Name  
    externalColumn.Precision = inputColumn.Precision  
    externalColumn.Length = inputColumn.Length  
    externalColumn.DataType = inputColumn.DataType  
    externalColumn.Scale = inputColumn.Scale  
  
    ' Map the external column to the input column.  
    inputColumn.ExternalMetadataColumnID = externalColumn.ID  
  
End Sub  
```  
  
## <a name="run-time"></a>Tempo de execução  
 Durante a execução, o componente de destino recebe uma chamada para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> toda vez que um <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> completo é disponibilizado do componente upstream. Esse método será chamado repetidamente até não haver mais buffers disponíveis e a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> ser `true`. Durante esse método, os componentes de destino fazem a leitura de colunas e linhas no buffer e as adicionam à fonte de dados externa.  
  
### <a name="locating-columns-in-the-buffer"></a>Localizando colunas no buffer  
 O buffer de entrada de um componente contém todas as colunas definidas nas coleções de colunas de saída dos componentes upstream a partir do componente no fluxo de dados. Por exemplo, se um componente de origem fornecer três colunas na saída e o próximo componente adicionar mais uma coluna de saída, o buffer fornecido ao componente de destino conterá quatro colunas, mesmo que o componente de destino só grave duas colunas.  
  
 A ordem das colunas no buffer de entrada não é definida pelo índice da coluna na coleção de colunas de entrada do componente de destino. É possível localizar de forma confiável colunas em uma linha de buffer através do método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> do <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A>. Esse método localiza a coluna que tem a ID de linhagem especificada no buffer especificado e retorna sua localização na linha. Os índices das colunas de entrada costumam ser localizados durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> e são armazenados em cache pelo desenvolvedor para uso posterior durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>.  
  
 O exemplo de código a seguir indica a localização das colunas de entrada no buffer durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> e armazena-as em uma matriz. A matriz é usada subsequentemente durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> para ler os valores das colunas no buffer.  
  
```csharp  
int[] cols;  
  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
  
    cols = new int[input.InputColumnCollection.Count];  
  
    for (int x = 0; x < input.InputColumnCollection.Count; x++)  
    {  
        cols[x] = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection[x].LineageID);  
    }  
}  
```  
  
```vb  
Private cols As Integer()  
  
Public Overrides Sub PreExecute()  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
  
    ReDim cols(input.InputColumnCollection.Count)  
  
    For x As Integer = 0 To input.InputColumnCollection.Count  
  
        cols(x) = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection(x).LineageID)  
    Next x  
  
End Sub  
```  
  
### <a name="processing-rows"></a>Processando linhas  
 Depois de serem localizadas, as colunas de entrada no buffer podem ser lidas e escritas na fonte de dados externa.  
  
 Apesar de o componente de destino escrever linhas na fonte de dados externa, talvez você queira atualizar o contador de desempenho "Linhas lidas" ou "Bytes de BLOB lidos", chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.IncrementPipelinePerfCounter%2A>. Para obter mais informações, consulte [Performance Counters](../performance/performance-counters.md).  
  
 O exemplo a seguir mostra um componente que lê linhas do buffer fornecido em <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>. Os índices das colunas no buffer foram localizados durante o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> no exemplo de código anterior.  
  
```csharp  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
        while (buffer.NextRow())  
        {  
            foreach (int col in cols)  
            {  
                if (!buffer.IsNull(col))  
                {  
                    //  TODO: Read the column data.  
                }  
            }  
        }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
        While (buffer.NextRow())  
  
            For Each col As Integer In cols  
  
                If buffer.IsNull(col) = False Then  
  
                    '  TODO: Read the column data.  
                End If  
  
            Next col  
        End While  
End Sub  
```  
  
## <a name="sample"></a>Amostra  
 O exemplo a seguir mostra um componente de destino simples que usa um gerenciador de conexões do Arquivo para salvar dados binários do fluxo de dados em arquivos. Esse exemplo não demonstra todos os métodos e todas as funcionalidades discutidas nesse tópico. Ele demonstra os métodos importantes que todo componente de destino personalizado deve substituir, mas não contém código para a validação em tempo de design.  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace BlobDst  
{  
  [DtsPipelineComponent(DisplayName = "BLOB Extractor Destination", Description = "Writes values of BLOB columns to files")]  
  public class BlobDst : PipelineComponent  
  {  
    string m_DestDir;  
    int m_FileNameColumnIndex = -1;  
    int m_BlobColumnIndex = -1;  
  
    public override void ProvideComponentProperties()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection.New();  
      input.Name = "BLOB Extractor Destination Input";  
      input.HasSideEffects = true;  
  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection.New();  
      conn.Name = "FileConnection";  
    }  
  
    public override void AcquireConnections(object transaction)  
    {  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection[0];  
      m_DestDir = (string)conn.ConnectionManager.AcquireConnection(null);  
  
      if (m_DestDir.Length > 0 && m_DestDir[m_DestDir.Length - 1] != '\\')  
        m_DestDir += "\\";  
    }  
  
    public override IDTSInputColumn100 SetUsageType(int inputID, IDTSVirtualInput100 virtualInput, int lineageID, DTSUsageType usageType)  
    {  
      IDTSInputColumn100 inputColumn = base.SetUsageType(inputID, virtualInput, lineageID, usageType);  
      IDTSCustomProperty100 custProp;  
  
      custProp = inputColumn.CustomPropertyCollection.New();  
      custProp.Name = "IsFileName";  
      custProp.Value = (object)false;  
  
      custProp = inputColumn.CustomPropertyCollection.New();  
      custProp.Name = "IsBLOB";  
      custProp.Value = (object)false;  
  
      return inputColumn;  
    }  
  
    public override void PreExecute()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection[0];  
      IDTSInputColumnCollection100 inputColumns = input.InputColumnCollection;  
      IDTSCustomProperty100 custProp;  
  
      foreach (IDTSInputColumn100 column in inputColumns)  
      {  
        custProp = column.CustomPropertyCollection["IsFileName"];  
        if ((bool)custProp.Value == true)  
        {  
          m_FileNameColumnIndex = (int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID);  
        }  
  
        custProp = column.CustomPropertyCollection["IsBLOB"];  
        if ((bool)custProp.Value == true)  
        {  
          m_BlobColumnIndex = (int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID);  
        }  
      }  
    }  
  
    public override void ProcessInput(int inputID, PipelineBuffer buffer)  
    {  
      while (buffer.NextRow())  
      {  
        string strFileName = buffer.GetString(m_FileNameColumnIndex);  
        int blobLength = (int)buffer.GetBlobLength(m_BlobColumnIndex);  
        byte[] blobData = buffer.GetBlobData(m_BlobColumnIndex, 0, blobLength);  
  
        strFileName = TranslateFileName(strFileName);  
  
        // Make sure directory exists before creating file.  
        FileInfo fi = new FileInfo(strFileName);  
        if (!fi.Directory.Exists)  
          fi.Directory.Create();  
  
        // Write the data to the file.  
        FileStream fs = new FileStream(strFileName, FileMode.Create, FileAccess.Write, FileShare.None);  
        fs.Write(blobData, 0, blobLength);  
        fs.Close();  
      }  
    }  
  
    private string TranslateFileName(string fileName)  
    {  
      if (fileName.Length > 2 && fileName[1] == ':')  
        return m_DestDir + fileName.Substring(3, fileName.Length - 3);  
      else  
        return m_DestDir + fileName;  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.IO   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Namespace BlobDst   
  
 <DtsPipelineComponent(DisplayName="BLOB Extractor Destination", Description="Writes values of BLOB columns to files")> _   
 Public Class BlobDst   
 Inherits PipelineComponent   
   Private m_DestDir As String   
   Private m_FileNameColumnIndex As Integer = -1   
   Private m_BlobColumnIndex As Integer = -1   
  
   Public  Overrides Sub ProvideComponentProperties()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New   
     input.Name = "BLOB Extractor Destination Input"   
     input.HasSideEffects = True   
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New   
     conn.Name = "FileConnection"   
   End Sub   
  
   Public  Overrides Sub AcquireConnections(ByVal transaction As Object)   
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection(0)   
     m_DestDir = CType(conn.ConnectionManager.AcquireConnection(Nothing), String)   
     If m_DestDir.Length > 0 AndAlso Not (m_DestDir(m_DestDir.Length - 1) = "\"C) Then   
       m_DestDir += "\"   
     End If   
   End Sub   
  
   Public  Overrides Function SetUsageType(ByVal inputID As Integer, ByVal virtualInput As IDTSVirtualInput100, ByVal lineageID As Integer, ByVal usageType As DTSUsageType) As IDTSInputColumn100   
     Dim inputColumn As IDTSInputColumn100 = MyBase.SetUsageType(inputID, virtualInput, lineageID, usageType)   
     Dim custProp As IDTSCustomProperty100   
     custProp = inputColumn.CustomPropertyCollection.New   
     custProp.Name = "IsFileName"   
     custProp.Value = CType(False, Object)   
     custProp = inputColumn.CustomPropertyCollection.New   
     custProp.Name = "IsBLOB"   
     custProp.Value = CType(False, Object)   
     Return inputColumn   
   End Function   
  
   Public  Overrides Sub PreExecute()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
     Dim inputColumns As IDTSInputColumnCollection100 = input.InputColumnCollection   
     Dim custProp As IDTSCustomProperty100   
     For Each column As IDTSInputColumn100 In inputColumns   
       custProp = column.CustomPropertyCollection("IsFileName")   
       If CType(custProp.Value, Boolean) = True Then   
         m_FileNameColumnIndex = CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer)   
       End If   
       custProp = column.CustomPropertyCollection("IsBLOB")   
       If CType(custProp.Value, Boolean) = True Then   
         m_BlobColumnIndex = CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer)   
       End If   
     Next   
   End Sub   
  
   Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
     While buffer.NextRow   
       Dim strFileName As String = buffer.GetString(m_FileNameColumnIndex)   
       Dim blobLength As Integer = CType(buffer.GetBlobLength(m_BlobColumnIndex), Integer)   
       Dim blobData As Byte() = buffer.GetBlobData(m_BlobColumnIndex, 0, blobLength)   
       strFileName = TranslateFileName(strFileName)   
       Dim fi As FileInfo = New FileInfo(strFileName)   
       ' Make sure directory exists before creating file.  
       If Not fi.Directory.Exists Then   
         fi.Directory.Create   
       End If   
       ' Write the data to the file.  
       Dim fs As FileStream = New FileStream(strFileName, FileMode.Create, FileAccess.Write, FileShare.None)   
       fs.Write(blobData, 0, blobLength)   
       fs.Close   
     End While   
   End Sub   
  
   Private Function TranslateFileName(ByVal fileName As String) As String   
     If fileName.Length > 2 AndAlso fileName(1) = ":"C Then   
       Return m_DestDir + fileName.Substring(3, fileName.Length - 3)   
     Else   
       Return m_DestDir + fileName   
     End If   
   End Function   
 End Class   
End Namespace  
```  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um componente de origem personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)   
 [Criar um destino com o componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
