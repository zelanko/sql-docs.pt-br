---
title: Criando um destino com o componente Script | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 206a91032b0eb2e1928846ebcdbfcb97f04ba12c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768952"
---
# <a name="creating-a-destination-with-the-script-component"></a>Criando um destino com o componente Script
  Você usa um componente de destino no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para salvar dados recebidos de fontes upstream e transformações em uma fonte de dados. Em geral, o componente de destino se conecta à fonte de dados através de um gerenciador de conexões existente.  
  
 Para obter uma visão geral do componente Script, consulte [estendendo o fluxo de dados com o componente Script] (... / extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md.  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. No entanto, para entender como funciona o componente Script, talvez seja útil ler as etapas de como desenvolver componentes de fluxo de dados personalizados na seção [Desenvolvendo um componente de fluxo de dados personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) e, especialmente, [Desenvolvendo um componente de destino personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md).  
  
## <a name="getting-started-with-a-destination-component"></a>Guia de Introdução com um componente Destino  
 Quando você adiciona um componente Script à guia Fluxo de Dados do Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], a caixa de diálogo **Selecionar Tipo de Componente Script** é aberta e solicita a seleção de um script **Origem**, **Destino** ou **Transformação**. Nessa caixa de diálogo, selecione **Destino**.  
  
 Depois, conecte a saída de uma transformação ao componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Como teste, você pode conectar uma origem diretamente a um destino, sem qualquer transformação.  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>Configurando um componente Destino no modo do design de metadados  
 Depois de selecionar a opção para criar um componente de destino, configure o componente usando o **Editor de Transformação Scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de Componente Script](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Para selecionar a linguagem de script que será usada pelo destino Script, defina a propriedade **ScriptLanguage** na página **Script** da caixa de diálogo **Editor de Transformação Scripts**.  
  
> [!NOTE]  
>  Para definir a linguagem de scripts padrão para o componente Script, use a opção **Linguagem de scripts** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [General Page](../general-page-of-integration-services-designers-options.md).  
  
 Um componente de destino de fluxo de dados tem uma entrada e nenhuma saída. A configuração da entrada do componente é uma das etapas que devem ser concluídas no modo de design de metadados, usando o **Editor de Transformação Scripts**, antes de escrever o script personalizado.  
  
### <a name="adding-connection-managers"></a>Adicionando gerenciadores de conexões  
 Em geral, um componente de destino usa um gerenciador de conexões existente para se conectar à fonte de dados na qual ele salva dados do fluxo de dados. Na página **Gerenciadores de Conexões** do **Editor de Transformação Scripts**, clique em **Adicionar** para adicionar o gerenciador de conexões apropriado.  
  
 Contudo, um gerenciador de conexões é apenas uma unidade conveniente que encapsula e armazena as informações necessárias para a conexão a uma fonte de dados de um tipo específico. Escreva seu próprio código personalizado para carregar ou salvar seus dados e, possivelmente, para abrir e fechar a conexão à fonte de dados.  
  
 Para obter informações gerais sobre como usar gerenciadores de conexões com o componente Script, consulte [Conectando-se a fontes de dados no componente Script](../extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Para obter mais informações sobre a página **Gerenciadores de Conexões** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;Página Gerenciadores de Conexões&#41;](../script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>Configurando entradas e colunas de entrada  
 Um componente de destino tem uma entrada e nenhuma saída.  
  
 Na página **Colunas de Entrada** do **Editor de Transformação Scripts**, a lista de colunas mostra as colunas disponíveis da saída do componente upstream no fluxo de dados. Selecione as colunas a serem salvas.  
  
 Para obter mais informações sobre a página **Colunas de Entrada** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Colunas de Entrada&#41;](../script-transformation-editor-input-columns-page.md).  
  
 A página **Entradas e Saídas** do **Editor de Transformação Scripts** mostra uma única entrada, que pode ser renomeada. Você fará referência à entrada pelo nome em seu script usando a propriedade de acessador criada no código gerado automaticamente.  
  
 Para obter mais informações sobre a página **Entradas e Saídas** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Entradas e Saídas&#41;](../script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Se você quiser usar variáveis existentes em seu script, você pode adicioná-las a `ReadOnlyVariables` e `ReadWriteVariables` campos de propriedade a **Script** página da **Editor de transformação scripts**.  
  
 Ao adicionar diversas variáveis aos campos de propriedade, separe os nomes das variáveis com vírgulas. Você também pode selecionar diversas variáveis clicando no botão de reticências ( **...** ) botão ao lado de `ReadOnlyVariables` e `ReadWriteVariables` campos de propriedade e, em seguida, selecionar as variáveis na **selecionar variáveis** caixa de diálogo.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [Usando variáveis no componente Script](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre a página **Script** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;Página Script&#41;](../script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>Gerando scripts de um componente de destino em modo do design de código  
 Depois de configurar os metadados do seu componente, você poderá escrever seu script personalizado. No **Editor de Transformação Scripts**, na página **Script**, clique em **Editar Script** para abrir o IDE do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications), no qual você pode adicionar o script personalizado. A linguagem de scripts usada depende se você selecionou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# como a linguagem de scripts para a propriedade **ScriptLanguage** na página **Script**.  
  
 Para obter informações importantes que se aplicam a todos os tipos de componentes criados por meio do componente Script, consulte [Codificando e depurando o componente Script](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o VSTA IDE depois de criar e configurar um componente de destino, a classe `ScriptMain` editável aparece no editor de códigos com um stub para o método `ProcessInputRow`. A classe `ScriptMain` é onde você escreverá seu código personalizado, e `ProcessInputRow` é o método mais importante em um componente de destino.  
  
 Se você abrir o **Explorador de projeto** janela no VSTA, você pode ver que o componente Script também gerou somente leitura `BufferWrapper` e `ComponentWrapper` itens de projeto. A classe `ScriptMain` herda da classe `UserComponent` no item de projeto `ComponentWrapper`.  
  
 Em tempo de execução, o mecanismo de fluxo de dados invoca o método `ProcessInput` na classe `UserComponent`, que substitui o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> da classe pai <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O método `ProcessInput`, por sua vez, executa um loop nas linhas do buffer de entrada e chama o método `ProcessInputRow` uma vez para cada linha.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Para terminar de criar um componente de destino personalizado, você pode escrever um script nos métodos a seguir disponíveis na classe `ScriptMain`.  
  
1.  Substitua o método `AcquireConnections` para se conectar à fonte de dados externa. Extraia o objeto de conexão, ou as informações de conexão requeridas, do gerenciador de conexões.  
  
2.  Substitua o método `PreExecute` como preparo para salvar os dados. Por exemplo, talvez você queira criar e configurar um `SqlCommand` e seus parâmetros nesse método.  
  
3.  Use o método `ProcessInputRow` substituído para copiar cada linha de entrada para a fonte de dados externa. Por exemplo, para um destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode copiar os valores de coluna nos parâmetros de um `SqlCommand` e executar o comando uma vez para cada linha. Para um destino de arquivo simples, você pode escrever os valores de cada coluna para um `StreamWriter`, separando-os com o delimitador de colunas.  
  
4.  Substitua o método `PostExecute` para desconectar-se da fonte de dados externa, caso necessário, e executar qualquer outra limpeza exigeida.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o código que é exigido na classe `ScriptMain` para criar um componente de destino.  
  
> [!NOTE]
>  Esses exemplos usam o **Person. address** na tabela a `AdventureWorks` banco de dados de exemplo e passam a primeira e a quarta colunas, o **int * AddressID*** e **nvarchar (30) Cidade**colunas de, pelo fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
### <a name="adonet-destination-example"></a>Exemplo de destino ADO.NET  
 Esse exemplo demonstra um componente de destino que usa um gerenciador de conexões existente do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para salvar dados do fluxo de dados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Criar uma [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão que usa o `SqlClient` provedor para conectar-se para o `AdventureWorks` banco de dados.  
  
2.  Crie uma tabela de destino executando o seguinte comando [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados `AdventureWorks`:  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Adicione um novo componente Script à superfície do designer de Fluxo de Dados e configure-o como um destino.  
  
4.  Conecte a saída de uma origem ou transformação upstream para o componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Essa saída deve fornecer dados a partir o **Person. address** tabela da `AdventureWorks` banco de dados de exemplo que contém pelo menos as **AddressID** e **Cidade** colunas.  
  
5.  Abra o **Editor de Transformação Scripts**. Na página **Colunas de Entrada**, selecione as colunas de entrada **AddressID** e **City**.  
  
6.  Na página **Entradas e Saídas**, renomeie a entrada com um nome mais descritivo, como **MyAddressInput**.  
  
7.  Na página **Gerenciadores de Conexões**, adicione ou crie o gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] com um nome como **MyADONETConnectionManager**.  
  
8.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script.  
  
9. Feche o **Editor de Transformação Scripts** e execute a amostra.  
  
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
  
1.  Crie um gerenciador de conexões de arquivos simples que se conecte a um arquivo de destino. Não é necessário que o arquivo já exista; o componente de destino irá criá-lo. Configure o arquivo de destino como um arquivo delimitado por vírgula que contém as colunas **AddressID** e **City**.  
  
2.  Adicione um novo componente Script à superfície do designer de Fluxo de Dados e configure-o como um destino.  
  
3.  Conecte a saída de uma origem ou transformação upstream para o componente de destino no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Essa saída deve fornecer dados a partir o **Person. address** tabela da `AdventureWorks` banco de dados de exemplo e deve conter pelo menos as **AddressID** e **Cidade** colunas.  
  
4.  Abra o **Editor de Transformação Scripts**. Na página **Colunas de Entrada**, selecione as colunas **AddressID** e **City**.  
  
5.  Na página **Entradas e Saídas**, renomeie a entrada com um nome mais descritivo, como **MyAddressInput**.  
  
6.  Na página **Gerenciadores de Conexões**, adicione ou crie o gerenciador de conexões de Arquivos Simples com um nome descritivo como **MyFlatFileDestConnectionManager**.  
  
7.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script.  
  
8.  Feche o **Editor de Transformação Scripts** e execute a amostra.  
  
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
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma origem com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [Desenvolvendo um componente de destino personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
