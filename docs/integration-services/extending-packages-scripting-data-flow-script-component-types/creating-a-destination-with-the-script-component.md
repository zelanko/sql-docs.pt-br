---
title: Criando um destino com o componente Script | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7680aac73590f92eadd615b9d164967e61877664
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-destination-with-the-script-component"></a>Criando um destino com o componente Script
  Você usa um componente de destino no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para salvar dados recebidos de fontes upstream e transformações em uma fonte de dados. Em geral, o componente de destino se conecta à fonte de dados através de um gerenciador de conexões existente.  
  
 Para obter uma visão geral do componente Script, consulte [estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler as etapas para desenvolver um componentes de fluxo de dados personalizados no [desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) seção e especialmente [Desenvolvendo um componente de destino personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md).  
  
## <a name="getting-started-with-a-destination-component"></a>Guia de Introdução com um componente Destino  
 Quando você adiciona um componente Script à guia fluxo de dados de [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, o **Selecionar tipo de componente de Script** caixa de diálogo é aberta e solicita que você selecione um **fonte**, **destino **, ou **transformação** script. Na caixa de diálogo, selecione **destino**.  
  
 Depois, conecte a saída de uma transformação ao componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Como teste, você pode conectar uma origem diretamente a um destino, sem qualquer transformação.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>Configurando um componente Destino no modo do design de metadados  
 Depois de selecionar a opção para criar um componente de destino, configure o componente usando o **Editor de transformação scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para selecionar a linguagem de script que o destino Script utilizará, defina o **ScriptLanguage** propriedade o **Script** página do **Editor de transformação scripts** caixa de diálogo.  
  
> [!NOTE]  
>  Para definir a linguagem padrão de script para o componente Script, use o **linguagem de script** opção o **geral** página do **opções** caixa de diálogo. Para obter mais informações, consulte [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
 Um componente de destino de fluxo de dados tem uma entrada e nenhuma saída. Configuração de entrada do componente é uma das etapas que você deve concluir no modo de design de metadados, usando o **Editor de transformação scripts**, antes de escrever seu script personalizado.  
  
### <a name="adding-connection-managers"></a>Adicionando gerenciadores de conexões  
 Em geral, um componente de destino usa um gerenciador de conexões existente para se conectar à fonte de dados na qual ele salva dados do fluxo de dados. No **gerenciadores de Conexão** página do **Editor de transformação scripts**, clique em **adicionar** para adicionar o Gerenciador de conexão apropriado.  
  
 Contudo, um gerenciador de conexões é apenas uma unidade conveniente que encapsula e armazena as informações necessárias para a conexão a uma fonte de dados de um tipo específico. Escreva seu próprio código personalizado para carregar ou salvar seus dados e, possivelmente, para abrir e fechar a conexão à fonte de dados.  
  
 Para obter informações gerais sobre como usar gerenciadores de conexão com o componente Script, consulte [se conectar a fontes de dados no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Para obter mais informações sobre o **gerenciadores de Conexão** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; Página gerenciadores de Conexão &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>Configurando entradas e colunas de entrada  
 Um componente de destino tem uma entrada e nenhuma saída.  
  
 Sobre o **colunas de entrada** página do **Editor de transformação scripts**, a lista de colunas mostra as colunas disponíveis da saída do componente upstream no fluxo de dados. Selecione as colunas a serem salvas.  
  
 Para obter mais informações sobre o **colunas de entrada** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; página colunas de entrada &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md).  
  
 O **entradas e saídas** página do **Editor de transformação scripts** mostra uma única entrada, o que pode ser renomeado. Você fará referência à entrada pelo nome em seu script usando a propriedade de acessador criada no código gerado automaticamente.  
  
 Para obter mais informações sobre o **entradas e saídas** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; entradas e saídas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Se você quiser usar variáveis existentes em seu script, você pode adicioná-las a **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade o **Script** página das **Editor de transformação scripts**.  
  
 Ao adicionar diversas variáveis aos campos de propriedade, separe os nomes das variáveis com vírgulas. Você também pode selecionar diversas variáveis clicando no botão de reticências (**... **) ao lado de **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade e, em seguida, selecione as variáveis no **selecionar variáveis** caixa de diálogo.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre o **Script** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; Script de página &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>Gerando scripts de um componente de destino em modo do design de código  
 Depois de configurar os metadados do seu componente, você poderá escrever seu script personalizado. No **Editor de transformação scripts**, no **Script** , clique em **Editar Script** para abrir o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE onde você pode adicionar seu script personalizado. A linguagem de script que você usa depende se você selecionou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c# como a linguagem de script para o **ScriptLanguage** propriedade o **Script** página.  
  
 Para obter informações importantes que se aplica a todos os tipos de componentes criados usando o componente Script, consulte [codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o VSTA IDE depois de criar e configurar um componente de destino, o editável **ScriptMain** classe aparece no editor de códigos com um stub para o **ProcessInputRow** método. O **ScriptMain** classe é onde você escreverá seu código personalizado, e **ProcessInputRow** é o método mais importante em um componente de destino.  
  
 Se você abrir o **Explorador de projeto** janela no VSTA, você pode ver que o componente Script também gerou somente leitura **BufferWrapper** e **ComponentWrapper** projeto itens. O **ScriptMain** classe herda de **UserComponent** classe no **ComponentWrapper** item de projeto.  
  
 Em tempo de execução, o mecanismo de fluxo de dados invoca o **ProcessInput** método no **UserComponent** de classe que substitui o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> método do <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> classe pai. O **ProcessInput** método por sua vez percorre as linhas no buffer de entrada e chama o **ProcessInputRow** método uma vez para cada linha.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Para concluir a criação de um componente de destino personalizado, talvez você queira gravar o script nos métodos a seguir disponíveis no **ScriptMain** classe.  
  
1.  Substituir o **AcquireConnections** método para se conectar à fonte de dados externa. Extraia o objeto de conexão, ou as informações de conexão requeridas, do gerenciador de conexões.  
  
2.  Substituir o **PreExecute** método para se preparar para salvar os dados. Por exemplo, você talvez queira criar e configurar um **SqlCommand** e seus parâmetros nesse método.  
  
3.  Use substituído **ProcessInputRow** método para copiar cada linha de entrada para a fonte de dados externa. Por exemplo, para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, você pode copiar os valores de coluna para os parâmetros de um **SqlCommand** e execute o comando uma vez para cada linha. Para um destino de arquivo simples, você pode escrever os valores para cada coluna a um **StreamWriter**, separando os valores com o delimitador de coluna.  
  
4.  Substituir o **PostExecute** método para se desconectar da fonte de dados externos, se necessário e para executar qualquer outra limpeza necessária.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o código que é necessário o **ScriptMain** classe para criar um componente de destino.  
  
> [!NOTE]  
>  Esses exemplos usam o **Person. address** tabela o **AdventureWorks** banco de dados de exemplo e passam a primeira e a quarta colunas, o * *int*AddressID ** * e **nvarchar (30) Cidade** colunas, por meio do fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
### <a name="adonet-destination-example"></a>Exemplo de destino ADO.NET  
 Este exemplo demonstra um componente de destino que usa um existente [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão para salvar os dados de fluxo de dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Criar um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão que usa o **SqlClient** provedor conectar-se para o **AdventureWorks** banco de dados.  
  
2.  Criar uma tabela de destino executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] do **AdventureWorks** banco de dados:  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Adicione um novo componente Script à superfície do designer de Fluxo de Dados e configure-o como um destino.  
  
4.  Conecte a saída de uma origem ou transformação upstream para o componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Essa saída deve fornecer dados a partir de **Person. address** tabela do **AdventureWorks** banco de dados de exemplo que contém pelo menos o **AddressID** e ** Cidade** colunas.  
  
5.  Abra o **Editor de transformação scripts**. Sobre o **colunas de entrada** página, selecione o **AddressID** e **City** colunas de entrada.  
  
6.  Sobre o **entradas e saídas** página, renomeie a entrada com um nome mais descritivo, como **MyAddressInput**.  
  
7.  Sobre o **gerenciadores de Conexão** página, adicione ou crie o [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão com um nome como **MyADONETConnectionManager**.  
  
8.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script.  
  
9. Fechar o **Editor de transformação scripts** e executar o exemplo.  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
    End Sub  
  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.Data.SqlClient;  
public class ScriptMain:  
    UserComponent  
  
{  
    IDTSConnectionManager100 connMgr;  
    SqlConnection sqlConn;  
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>Exemplo de Destino de Arquivos Simples  
 Esse exemplo demonstra um componente de destino que usa um gerenciador de conexões de arquivos simples existente para salvar dados do fluxo de dados em um arquivo simples.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Crie um gerenciador de conexões de arquivos simples que se conecte a um arquivo de destino. Não é necessário que o arquivo já exista; o componente de destino irá criá-lo. Configurar o arquivo de destino como um arquivo delimitado por vírgulas que contém o **AddressID** e **City** colunas.  
  
2.  Adicione um novo componente Script à superfície do designer de Fluxo de Dados e configure-o como um destino.  
  
3.  Conecte a saída de uma origem ou transformação upstream para o componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Essa saída deve fornecer dados a partir de **Person. address** tabela do **AdventureWorks** banco de dados de exemplo e deve conter pelo menos o **AddressID** e **City** colunas.  
  
4.  Abra o **Editor de transformação scripts**. Sobre o **colunas de entrada** página, selecione o **AddressID** e **City** colunas.  
  
5.  Sobre o **entradas e saídas** página, renomeie a entrada com um nome mais descritivo, como **MyAddressInput**.  
  
6.  Sobre o **gerenciadores de Conexão** página, adicione ou crie a conexão de arquivo simples manager com um nome descritivo, como **MyFlatFileDestConnectionManager**.  
  
7.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script.  
  
8.  Fechar o **Editor de transformação scripts** e executar o exemplo.  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma fonte com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [Desenvolvendo um componente de destino personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
