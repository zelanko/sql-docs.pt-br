---
title: Compreender o Component Object Model do Script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa6235337aab70ed826a5507e7bd8ff2a45c4636
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286585"
---
# <a name="understanding-the-script-component-object-model"></a>Compreendendo o Component Object Model Script

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Conforme discutido em [Codificar e depurar o componente Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md), o projeto do componente Script contém três itens de projeto:  
  
1.  O item **ScriptMain**, que contém a classe **ScriptMain** na qual você escreve seu código. A classe **ScriptMain** herda a classe **UserComponent**.  
  
2.  O item **ComponentWrapper**, que contém a classe **UserComponent**, uma instância do <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> que contém os métodos e propriedades que você utilizará para processar dados e interagir com o pacote. O item **ComponentWrapper** também contém as classes de coleção **Connections** e **Variables**.  
  
3.  O item **BufferWrapper**, que contém classes herdadas de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para cada entrada e saída, bem como as propriedades digitadas para cada coluna.  
  
 À medida que você escrever seu código no item **ScriptMain**, usará os objetos, métodos e propriedades discutidos nesse tópico. Cada componente não usará todos os métodos listados aqui; porém, quando usados, eles obedecerão à sequência mostrada.  
  
 A classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> não contém códigos de implementação para os métodos discutidos nesse tópico. Portanto, é desnecessário, mas inofensivo, adicionar uma chamada à implementação de classe base na sua própria implementação do método.  
  
 Para obter informações sobre como usar os métodos e propriedades dessas classes em um tipo específico de componente Script, consulte a seção [Exemplos adicionais de componente de script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Os tópicos de exemplo também contêm exemplos de código completos.  
  
## <a name="acquireconnections-method"></a>Método AcquireConnections  
 Origens e destinos geralmente precisam se conectar a uma fonte de dados externa. Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para recuperar a conexão ou as informações de conexão do gerenciador de conexões apropriado.  
  
 O exemplo a seguir retorna um **System.Data.SqlClient.SqlConnection** de um gerenciador de conexões ADO.NET.  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 O exemplo a seguir retorna um caminho completo e o nome de arquivo de um Gerenciador de Conexões de Arquivo Simples e, em seguida, abre o arquivo por meio de um **System.IO.StreamReader**.  
  
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
 Para cada entrada configurada, o item de projeto **BufferWrapper** contém uma classe que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> e tem o mesmo nome que a entrada. Cada classe de buffer de entrada contém as seguintes propriedades, funções e métodos:  
  
-   Propriedades de acessador nomeadas, digitadas para cada coluna de entrada selecionada. Essas propriedades são somente leitura ou de leitura/gravação, dependendo do **Tipo de Uso** especificado para a coluna na página **Colunas de Entrada** do **Editor de Transformação Scripts**.  
  
-   Uma propriedade **\<coluna>_IsNull** para cada coluna de entrada selecionada. Essa propriedade também é somente leitura ou de leitura/gravação, dependendo do **Tipo de Uso** especificado para a coluna.  
  
-   Um método **DirectRowTo\<bufferdesaída>** para cada saída configurada. Você usará esses métodos ao filtrar linhas para uma das várias saídas no mesmo **ExclusionGroup**.  
  
-   Uma função **NextRow** para obter a próxima linha de entrada e uma função **EndOfRowset** para determinar se o último buffer de dados foi processado. Em geral, você não precisa dessas funções ao usar os métodos de processamento de entrada implementados na classe base **UserComponent**. A próxima seção fornece mais informações sobre a classe base **UserComponent**.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>O que o item de projeto ComponentWrapper fornece  
 O item de projeto ComponentWrapper contém uma classe nomeada **UserComponent** que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. A classe **ScriptMain** na qual você escreve seu código personalizado, por sua vez, deriva de **UserComponent**. A classe **UserComponent** contém os seguintes métodos:  
  
-   Uma implementação substituída do método **ProcessInput**. Esse é o método que o mecanismo de fluxo de dados chama em seguida no tempo de execução, depois do método **PreExecute** e ele pode ser chamado várias vezes. **ProcessInput** entrega o processamento para o método **\<bufferdeentrada>_ProcessInput**. Depois, o método **ProcessInput** verifica se o buffer de entrada chegou ao final e, em caso positivo, chama o método substituível **FinishOutputs** e o método particular **MarkOutputsAsFinished**. O método **MarkOutputsAsFinished**, em seguida, chama **SetEndOfRowset** no último buffer de saída.  
  
-   Uma implementação substituível do método **\<bufferdeentrada>_ProcessInput**. Essa implementação padrão simplesmente executa um loop em cada linha de entrada e chama **\<inputbuffer>_ProcessInputRow**.  
  
-   Uma implementação substituível do método **\<inputbuffer>_ProcessInputRow**. A implementação padrão é vazia. Esse é o método que, em geral, você substituirá para escrever seu código de processamento de dados personalizado.  
  
#### <a name="what-your-custom-code-should-do"></a>O que seu código personalizado deve fazer  
 Você pode usar os seguintes métodos para processar a entrada na classe **ScriptMain**:  
  
-   Substitua o **\<bufferdeentrada>_ProcessInputRow** para processar os dados em cada linha de entrada conforme ela passa.  
  
-   Só substitua o **\<bufferdeentrada>_ProcessInput** se você precisar fazer algo adicional enquanto executa um loop em linhas de entrada. (Por exemplo, verifique se o **EndOfRowset** executa outra ação após o processamento de todas as linhas.) Chame **\<bufferdeentrada>_ProcessInputRow** para executar o processamento de linha.  
  
-   Substitua **FinishOutputs** se precisar fazer algo nas saídas antes de seu fechamento.  
  
 O método **ProcessInput** garante que esses métodos sejam chamados nos momentos apropriados.  
  
### <a name="processing-outputs"></a>Processando saídas  
 Componentes Script configurados como origens ou transformações têm uma ou mais saídas.  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>O que o item de projeto BufferWrapper fornece  
 Para cada saída configurada, o item de projeto BufferWrapper contém uma classe que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> e possui o mesmo nome que a saída. Cada classe de buffer de entrada contém as seguintes propriedades e métodos:  
  
-   Propriedades do acessador nomeado, digitado, somente gravação para cada coluna de saída.  
  
-   Uma propriedade **\<coluna>_IsNull** somente gravação para cada coluna de saída selecionada que você pode usar para definir o valor de coluna como **nulo**.  
  
-   Um método **AddRow** para adicionar uma linha nova vazia ao buffer de saída.  
  
-   Um método **SetEndOfRowset** para notificar o mecanismo de fluxo de dados buffers de que dados não são mais esperados. Também há uma função **EndOfRowset** para determinar se o buffer atual é o último buffer de dados. Em geral, você não precisa dessas funções ao usar os métodos de processamento de entrada implementados na classe base **UserComponent**.  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>O que o item de projeto ComponentWrapper fornece  
 O item de projeto ComponentWrapper contém uma classe nomeada **UserComponent** que deriva de <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. A classe **ScriptMain** na qual você escreve seu código personalizado, por sua vez, deriva de **UserComponent**. A classe **UserComponent** contém os seguintes métodos:  
  
-   Uma implementação substituída do método **PrimeOutput**. O mecanismo de fluxo de dados chama esse método antes do **ProcessInput** em tempo de execução e ele é chamado apenas uma vez. **PrimeOutput** entrega o processamento para o método **CreateNewOutputRows**. Depois, se o componente for uma origem (ou seja, se o componente não tiver entradas), o **PrimeOutput** chamará o método substituível **FinishOutputs** e o método particular **MarkOutputsAsFinished**. O método **MarkOutputsAsFinished** chama **SetEndOfRowset** no último buffer de saída.  
  
-   Uma implementação substituível do método **CreateNewOutputRows**. A implementação padrão é vazia. Esse é o método que, em geral, você substituirá para escrever seu código de processamento de dados personalizado.  
  
#### <a name="what-your-custom-code-should-do"></a>O que seu código personalizado deve fazer  
 Você pode usar os seguintes métodos para processar saídas na classe **ScriptMain**:  
  
-   Substitua **CreateNewOutputRows** apenas quando você puder adicionar e preencher linhas de saída antes de processar linhas de entrada. Por exemplo, você pode usar o **CreateNewOutputRows** em uma origem. Mas em uma transformação com saídas assíncronas, chame o **AddRow** durante ou depois do processamento de dados de entrada.  
  
-   Substitua **FinishOutputs** se precisar fazer algo nas saídas antes de seu fechamento.  
  
 O método **PrimeOutput** garante que esses métodos sejam chamados nos momentos apropriados.  
  
## <a name="postexecute-method"></a>Método PostExecute  
 Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> sempre que houver processamento a ser executado uma só vez após o processamento das linhas de dados. Por exemplo, em uma origem, talvez você queira fechar o **System.Data.SqlClient.SqlDataReader** usado para carregar dados no fluxo de dados.  
  
> [!IMPORTANT]  
>  A coleção de **ReadWriteVariables** está disponível apenas no método **PostExecute**. Portanto, não será possível incrementar diretamente o valor de uma variável de pacote ao processar cada linha de dados. Em vez disso, incremente o valor de uma variável local e defina o valor da variável do pacote como o valor da variável local no método **PostExecute** depois de todos os dados terem sido processados.  
  
## <a name="releaseconnections-method"></a>Método ReleaseConnections  
 Origens e destinos geralmente precisam se conectar a uma fonte de dados externa. Substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> para fechar e liberar a conexão aberta anteriormente no método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A>.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o componente de Script no Editor de Componentes de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [Codificar e depurar o componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
