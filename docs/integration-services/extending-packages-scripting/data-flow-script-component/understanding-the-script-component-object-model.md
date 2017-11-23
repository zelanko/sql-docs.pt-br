---
title: "Noções básicas sobre o modelo de objeto do componente Script | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09de00344fe94087b6287b07c4b1ffe933d27b7c
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="understanding-the-script-component-object-model"></a>Compreendendo o Component Object Model Script
  Conforme discutido em [codificando e depurando o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md), o projeto de componente de Script contém três itens de projeto:  
  
1.  O **ScriptMain** item, que contém o **ScriptMain** classe na qual você escreve seu código. O **ScriptMain** classe herda o **UserComponent** classe.  
  
2.  O **ComponentWrapper** item, que contém o **UserComponent** uma instância da classe <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> que contém os métodos e propriedades que você usará para processar dados e interagir com o pacote. O **ComponentWrapper** item também contém **conexões** e **variáveis** classes de coleção.  
  
3.  O **BufferWrapper** item, que contém classes que herda de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada propriedades de entrada e saída e tipado para cada coluna.  
  
 Enquanto você escreve seu código **ScriptMain** item, você usará os objetos, métodos e propriedades discutidas neste tópico. Cada componente não usará todos os métodos listados aqui; porém, quando usados, eles obedecerão à sequência mostrada.  
  
 A classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> não contém códigos de implementação para os métodos discutidos nesse tópico. Portanto, é desnecessário, mas inofensivo, adicionar uma chamada à implementação de classe base na sua própria implementação do método.  
  
 Para obter informações sobre como usar os métodos e propriedades dessas classes em um tipo específico de componente Script, consulte a seção [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Os tópicos de exemplo também contêm exemplos de código completos.  
  
## <a name="acquireconnections-method"></a>Método AcquireConnections  
 Origens e destinos geralmente precisam se conectar a uma fonte de dados externa. Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para recuperar a conexão ou as informações de conexão do gerenciador de conexões apropriado.  
  
 O exemplo a seguir retorna um **SqlConnection** de um Gerenciador de conexão ADO.NET.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 O exemplo a seguir retorna um caminho completo e nome de arquivo de um Gerenciador de Conexão de arquivo simples e, em seguida, abre o arquivo usando um **System.IO.StreamReader**.  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>Método PreExecute  
 Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> sempre que existir um processamento que precisa ser executado apenas uma vez antes de iniciar o processamento de linhas de dados. Por exemplo, em um destino, talvez você queira configurar o comando com parâmetros que o destino utilizará para inserir cada linha de dados na fonte de dados.  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>Processando entradas e saídas  
  
### <a name="processing-inputs"></a>Processando entradas  
 Componentes Script que são configurados como transformações ou destinos têm uma entrada.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>O que o item de projeto BufferWrapper fornece  
 Para cada entrada que você tenha configurado, o **BufferWrapper** item de projeto contém uma classe que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> e tem o mesmo nome que a entrada. Cada classe de buffer de entrada contém as seguintes propriedades, funções e métodos:  
  
-   Propriedades de acessador nomeadas, digitadas para cada coluna de entrada selecionada. Essas propriedades são somente leitura ou leitura/gravação, dependendo do **tipo de uso** especificado para a coluna no **colunas de entrada** página do **Editor de transformação scripts**.  
  
-   Um  **\<coluna > IsNull** coluna de propriedade para cada selecionado de entrada. Essa propriedade também é somente leitura ou leitura/gravação, dependendo do **tipo de uso** especificado para a coluna.  
  
-   Um **DirectRowTo\<outputbuffer >** configurado de método para cada saída. Você usará esses métodos ao filtrar linhas para uma das várias saídas no mesmo **ExclusionGroup**.  
  
-   Um **NextRow** função para obter a próxima linha de entrada e um **EndOfRowset** função para determinar se o último buffer de dados foi processado. Você normalmente não precisa dessas funções ao usar a métodos implementados em de processamento de entrada de **UserComponent** classe base. A próxima seção fornece mais informações sobre o **UserComponent** classe base.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>O que o item de projeto ComponentWrapper fornece  
 O item de projeto ComponentWrapper contém uma classe denominada **UserComponent** que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O **ScriptMain** classe na qual você escreve seu código personalizado por sua vez deriva de **UserComponent**. O **UserComponent** classe contém os seguintes métodos:  
  
-   Uma implementação substituída do **ProcessInput** método. Esse é o método que o fluxo de dados chamadas de mecanismo lado em tempo de execução após o **PreExecute** método e ele pode ser chamado várias vezes. **ProcessInput** entrega o processamento para o  **\<inputbuffer > _ProcessInput** método. Em seguida, o **ProcessInput** método verifica o final do buffer de entrada e, se o final do buffer foi atingido, chama o substituível **FinishOutputs** método e particular **MarkOutputsAsFinished** método. O **MarkOutputsAsFinished** , em seguida, chama um método **SetEndOfRowset** no último buffer de saída.  
  
-   Uma implementação substituível do  **\<inputbuffer > _ProcessInput** método. Esta implementação padrão simplesmente executa um loop em cada linha de entrada e chama  **\<inputbuffer > _ProcessInputRow**.  
  
-   Uma implementação substituível do  **\<inputbuffer > _ProcessInputRow** método. A implementação padrão é vazia. Esse é o método que, em geral, você substituirá para escrever seu código de processamento de dados personalizado.  
  
#### <a name="what-your-custom-code-should-do"></a>O que seu código personalizado deve fazer  
 Você pode usar os seguintes métodos para processar a entrada no **ScriptMain** classe:  
  
-   Substituir  **\<inputbuffer > _ProcessInputRow** para processar os dados em cada linha de entrada percorrida.  
  
-   Substituir  **\<inputbuffer > _ProcessInput** somente se você precisar fazer algo adicional enquanto executa um loop em linhas de entrada. (Por exemplo, você precisa testar **EndOfRowset** para executar alguma outra ação depois que todas as linhas forem processadas.) Chamar  **\<inputbuffer > _ProcessInputRow** para executar o processamento de linha.  
  
-   Substituir **FinishOutputs** se você precisar fazer algo nas saídas antes de serem fechadas.  
  
 O **ProcessInput** método garante que esses métodos são chamados nos momentos apropriados.  
  
### <a name="processing-outputs"></a>Processando saídas  
 Componentes Script configurados como origens ou transformações têm uma ou mais saídas.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>O que o item de projeto BufferWrapper fornece  
 Para cada saída configurada, o item de projeto BufferWrapper contém uma classe que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> e possui o mesmo nome que a saída. Cada classe de buffer de entrada contém as seguintes propriedades e métodos:  
  
-   Propriedades do acessador nomeado, digitado, somente gravação para cada coluna de saída.  
  
-   Uma gravação somente  **\<coluna > IsNull** propriedade para cada coluna de saída selecionada que você pode usar para definir o valor da coluna como **nulo**.  
  
-   Um **AddRow** método para adicionar uma linha nova vazia ao buffer de saída.  
  
-   Um **SetEndOfRowset** método para informar o mecanismo de fluxo de dados que não há mais buffers de dados são esperados. Também há um **EndOfRowset** função para determinar se o buffer atual é o último buffer de dados. Você geralmente não precisa dessas funções ao usar a métodos implementados em de processamento de entrada de **UserComponent** classe base.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>O que o item de projeto ComponentWrapper fornece  
 O item de projeto ComponentWrapper contém uma classe denominada **UserComponent** que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O **ScriptMain** classe na qual você escreve seu código personalizado por sua vez deriva de **UserComponent**. O **UserComponent** classe contém os seguintes métodos:  
  
-   Uma implementação substituída do **PrimeOutput** método. O mecanismo de fluxo de dados chama esse método antes **ProcessInput** em tempo de execução, e ele é chamado apenas uma vez. **PrimeOutput** entrega o processamento para o **CreateNewOutputRows** método. Então, se o componente é uma origem (ou seja, o componente não tem entradas), **PrimeOutput** chama o substituível **FinishOutputs** método e particular **MarkOutputsAsFinished** método. O **MarkOutputsAsFinished** chamadas de método **SetEndOfRowset** no último buffer de saída.  
  
-   Uma implementação substituível do **CreateNewOutputRows** método. A implementação padrão é vazia. Esse é o método que, em geral, você substituirá para escrever seu código de processamento de dados personalizado.  
  
#### <a name="what-your-custom-code-should-do"></a>O que seu código personalizado deve fazer  
 Você pode usar os seguintes métodos para processar saídas no **ScriptMain** classe:  
  
-   Substituir **CreateNewOutputRows** somente quando você pode adicionar e preencher as linhas de saída antes de processar linhas de entrada. Por exemplo, você pode usar **CreateNewOutputRows** em uma fonte, mas em uma transformação com saídas assíncronas, você deve chamar **AddRow** durante ou após o processamento de dados de entrada.  
  
-   Substituir **FinishOutputs** se você precisar fazer algo nas saídas antes de serem fechadas.  
  
 O **PrimeOutput** método garante que esses métodos são chamados nos momentos apropriados.  
  
## <a name="postexecute-method"></a>Método PostExecute  
 Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> sempre que houver processamento a ser executado uma só vez após o processamento das linhas de dados. Por exemplo, em uma fonte, convém fechar o **System.Data.SqlClient.SqlDataReader** que você usou para carregar dados no fluxo de dados.  
  
> [!IMPORTANT]  
>  A coleção de **ReadWriteVariables** está disponível apenas no **PostExecute** método. Portanto, não será possível incrementar diretamente o valor de uma variável de pacote ao processar cada linha de dados. Em vez disso, incremente o valor de uma variável local e defina o valor da variável de pacote para o valor da variável local no **PostExecute** método depois que todos os dados foram processado.  
  
## <a name="releaseconnections-method"></a>Método ReleaseConnections  
 Origens e destinos geralmente devem se conectar a uma fonte de dados externa. Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para fechar e liberar a conexão aberta anteriormente no método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>.  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Configurando o componente Script no Editor de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [Codificando e depurando o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

