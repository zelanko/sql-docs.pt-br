---
title: Criando uma fonte com o componente Script | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b31d28b646ff7f1727809179398906a3bab75e61
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="creating-a-source-with-the-script-component"></a>Criando uma fonte com o componente Script
  Você usa um componente de origem no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para carregar dados de uma fonte de dados a serem passados para transformações e destinos downstream. Normalmente, você se conecta à fonte de dados por um gerenciador de conexões existente.  
  
 Para obter uma visão geral do componente Script, consulte [Estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. Contudo, para compreender o funcionamento do componente Script, talvez seja útil ler as etapas envolvidas no desenvolvimento de um componente de fluxo de dados personalizado. Consulte a seção [Desenvolvendo um componente de fluxo de dados personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), especialmente o tópico [Desenvolvendo um componente de origem personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md).  
  
## <a name="getting-started-with-a-source-component"></a>Guia de introdução com um componente de origem  
 Quando você adiciona um componente Script ao painel Fluxo de Dados do Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], a caixa de diálogo **Selecionar Tipo de Componente Script** é aberta e solicita a seleção de um script de Origem, Destino ou Transformação. Nessa caixa de diálogo, selecione **Origem**.  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>Configurando um componente de origem em modo do design de metadados  
 Depois de selecionar que deseja criar um componente de origem, configure o componente usando o **Editor de Transformação Scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de Componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Um componente de origem de fluxo de dados não tem entradas e dá suporte a uma ou mais saídas. A configuração das saídas do componente é uma das etapas que devem ser concluídas no modo de design de metadados, usando o **Editor de Transformação Scripts**, antes de escrever o script personalizado.  
  
 Você também pode especificar a linguagem de script configurando a propriedade **ScriptLanguage** na página **Script** do **Editor de Transformação Scripts**.  
  
> [!NOTE]  
>  Para definir a linguagem de scripts padrão para componentes de Script e Tarefas de Script, use a opção **Linguagem de scripts** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [General Page](~/integration-services/control-flow/script-task-editor-general-page.md).  
  
### <a name="adding-connection-managers"></a>Adicionando gerenciadores de conexões  
 Em geral, um componente de origem usa um gerenciador de conexões existente para se conectar à fonte de dados da qual ele carrega dados para o fluxo de dados. Na página **Gerenciadores de Conexões** do **Editor de Transformação Scripts**, clique em **Adicionar** para adicionar o gerenciador de conexões apropriado.  
  
 Contudo, um gerenciador de conexões é apenas uma unidade conveniente que encapsula e armazena as informações necessárias para a conexão a uma fonte de dados de um tipo específico. Escreva seu próprio código personalizado para carregar ou salvar seus dados e, possivelmente, para também abrir e fechar a conexão à fonte de dados.  
  
 Para obter informações gerais sobre como usar gerenciadores de conexões com o componente Script, consulte [Conectando-se a fontes de dados no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Para obter mais informações sobre a página **Gerenciadores de Conexões** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;Página Gerenciadores de Conexões&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>Configurando saídas e colunas de saída  
 Um componente de origem não tem nenhuma entrada e dá suporte a uma ou mais saídas. Na página **Entradas e Saídas** do **Editor de Transformação Scripts**, uma única saída foi criada por padrão, mas nenhuma coluna de saída foi criada. Nessa página do editor, você pode precisar ou querer configurar os itens a seguir.  
  
-   Adicione e configure colunas de saída manualmente para cada saída. Selecione a pasta Colunas de Saída para cada saída e, em seguida, use os botões **Adicionar Coluna** e **Remover Coluna** para gerenciar as colunas de saída para cada saída do componente de origem. Posteriormente, você fará referência às colunas de saída do seu script pelos nomes atribuídos aqui, usando as propriedades de acessador digitadas criadas para você no código gerado automaticamente.  
  
-   Talvez você queira criar uma ou mais saídas adicionais, tais como uma saída de erro simulada para linhas que contêm valores inesperados. Use os botões **Adicionar Saída** e **Remover Saída** para gerenciar as saídas do componente de origem. Todas as linhas de entrada são direcionadas a todas as saídas disponíveis, a menos que você também especifique um valor idêntico diferente de zero para a propriedade **ExclusionGroup** das saídas nas quais você pretende direcionar cada linha a apenas uma das saídas que compartilham o mesmo valor **ExclusionGroup**. O valor inteiro específico selecionado para identificar o **ExclusionGroup** não é significativo.  
  
    > [!NOTE]  
    >  Também use um valor da propriedade **ExclusionGroup** diferente de zero com uma única saída quando não desejar gerar todas as linhas. Porém, nesse caso, você deve chamar explicitamente o método **DirectRowTo\<outputbuffer>** para cada linha que deseja enviar à saída.  
  
-   Talvez você queira atribuir um nome amigável às saídas. Posteriormente, você fará referência às saídas pelos nomes no seu script, usando as propriedades de acessador digitadas, criadas para você no código gerado automaticamente.  
  
-   Em geral, várias saídas no mesmo **ExclusionGroup** têm as mesmas colunas de saída. Porém, se você estiver criando uma saída de erro simulada, talvez queira adicionar mais colunas para armazenar informações de erro. Para obter informações sobre como o mecanismo de fluxo de dados processa linhas de erro, consulte [Usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). No componente Script, contudo, escreva seu próprio código para preencher as colunas adicionais com informações de erro apropriadas. Para obter mais informações, consulte [Simulando uma saída de erro para o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obter mais informações sobre a página **Entradas e Saídas** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;página Entradas e Saídas&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Caso existam variáveis cujos valores você deseja usar no script, adicione-as aos campos de propriedade **ReadOnlyVariables** e **ReadWriteVariables** da página **Script** do **Editor de Transformação Scripts**.  
  
 Ao inserir diversas variáveis nos campos de propriedade, separe os nomes delas por vírgulas. Outra alternativa é inserir diversas variáveis clicando no botão de reticências (**…**) ao lado dos campos de propriedade **ReadOnlyVariables** e **ReadWriteVariables** e selecionar as variáveis na caixa de diálogo **Selecionar variáveis**.  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [Usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre a página **Script** do **Editor de Transformação Scripts**, consulte [Editor de Transformação Scripts &#40;Página Script&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>Gerando scripts de um componente de origem em modo do design de código  
 Depois de configurar os metadados para o componente, abra o IDE do VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) para codificar o script personalizado. Para abrir o VSTA, clique em **Editar Script** na página **Script** do **Editor de Transformação Scripts**. Escreva seu script usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#, dependendo da linguagem de script selecionada para a propriedade **ScriptLanguage**.  
  
 Para obter informações importantes que se aplicam a todos os tipos de componentes criados por meio do componente Script, consulte [Codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abrir o IDE do VSTA depois de criar e configurar um componente de origem, a classe editável **ScriptMain** será exibida no editor de códigos. Escreva seu código personalizado na classe **ScriptMain**.  
  
 A classe **ScriptMain** inclui um stub para o método **CreateNewOutputRows**. O **CreateNewOutputRows** é o método mais importante em um componente de origem.  
  
 Se você abrir a janela **Explorador de Projeto** no VSTA, verá que o componente Script também gerou os itens de projeto **BufferWrapper** e **ComponentWrapper** somente leitura. A classe **ScriptMain** herda da classe **UserComponent** no item de projeto **ComponentWrapper**.  
  
 Em tempo de execução, o mecanismo de fluxo de dados invoca o método **PrimeOutput** na classe **UserComponent**, que substitui o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> da classe pai <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. O método **PrimeOutput**, por sua vez, chama os seguintes métodos:  
  
1.  O método **CreateNewOutputRows**, que é substituído em **ScriptMain** para adicionar linhas da fonte de dados aos buffers de saída, que estão vazios no início.  
  
2.  O método **FinishOutputs**, que é vazio por padrão. Substitua esse método em **ScriptMain** para executar qualquer processamento necessário para concluir a saída.  
  
3.  O método **MarkOutputsAsFinished** particular, que chama o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> da classe pai <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> para indicar ao mecanismo de fluxo de dados que a saída está concluída. Não é necessário chamar o **SetEndOfRowset** explicitamente no próprio código.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Para concluir a criação de um componente de origem personalizado, é recomendável escrever o script nos métodos a seguir disponíveis na classe **ScriptMain**.  
  
1.  Substitua o método **AcquireConnections** para se conectar à fonte de dados externa. Extraia o objeto de conexão, ou as informações de conexão requeridas, do gerenciador de conexões.  
  
2.  Substitua o método **PreExecute** para carregar dados, caso possa carregar todos os dados de origem ao mesmo tempo. Por exemplo, você pode executar um **SqlCommand** em uma conexão do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] com um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e carregar todos os dados de origem ao mesmo tempo em um **SqlDataReader**. Se precisar carregar os dados de origem uma linha por vez (por exemplo, ao ler um arquivo de texto), carregue os dados ao executar um loop pelas linhas em **CreateNewOutputRows**.  
  
3.  Use o método **CreateNewOutputRows** substituído para adicionar novas linhas aos buffers de saída vazios e preencher os valores de cada coluna nas novas linhas de saída. Use o método **AddRow** de cada buffer de saída para adicionar uma linha nova vazia e, depois, defina os valores de cada coluna. Em geral, você copia valores das colunas carregadas a partir da origem externa.  
  
4.  Substitua o método **PostExecute** para concluir o processamento dos dados. Por exemplo, feche o **SqlDataReader** usado para carregar os dados.  
  
5.  Substitua o método **ReleaseConnections** para se desconectar da fonte de dados externa, caso necessário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o código personalizado necessário na classe **ScriptMain** para criar um componente de origem.  
  
> [!NOTE]  
>  Esses exemplos usam a tabela **Person.Address** no banco de dados de exemplo **AdventureWorks** e passam sua primeira e quarta colunas, as colunas **intAddressID** e **nvarchar(30)City**, pelo fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
### <a name="adonet-source-example"></a>Exemplo de origem do ADO.NET  
 Esse exemplo demonstra um componente de origem que usa um gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente para carregar dados de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no fluxo de dados.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Crie um gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que usa o provedor **SqlClient** para se conectar ao banco de dados **AdventureWorks**.  
  
2.  Adicione um novo componente Script à superfície do designer Fluxo de Dados e configure-o como uma origem.  
  
3.  Abra o **Editor de Transformação Scripts**. Na página **Entradas e Saídas**, renomeie a saída padrão com um nome mais descritivo, como **MyAddressOutput** e adicione e configure as duas colunas de saída, **AddressID** e **City**.  
  
    > [!NOTE]  
    >  Altere o tipo de dados da coluna de saída **City** para DT_WSTR.  
  
4.  Na página **Gerenciadores de Conexões**, adicione ou crie o gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e dê a ele um nome como **MyADONETConnection**.  
  
5.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de Transformação Scripts**.  
  
6.  Crie e configure um componente de destino, como um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o componente de destino de exemplo demonstrado em [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md), que espera as colunas **AddressID** e **City**. Depois, conecte o componente de origem ao destino. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Crie uma tabela de destino executando o seguinte comando [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados **AdventureWorks**:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  Execute o exemplo.  
  
    ```vb  
    Imports System.Data.SqlClient  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim connMgr As IDTSConnectionManager100  
        Dim sqlConn As SqlConnection  
        Dim sqlReader As SqlDataReader  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            connMgr = Me.Connections.MyADONETConnection  
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)  
            sqlReader = cmd.ExecuteReader  
  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Do While sqlReader.Read  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = sqlReader.GetInt32(0)  
                    .City = sqlReader.GetString(1)  
                End With  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
  
            sqlReader.Close()  
  
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
        SqlDataReader sqlReader;  
  
        public override void AcquireConnections(object Transaction)  
        {  
            connMgr = this.Connections.MyADONETConnection;  
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
  
            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);  
            sqlReader = cmd.ExecuteReader();  
  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            while (sqlReader.Read())  
            {  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);  
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);  
                }  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            sqlReader.Close();  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            connMgr.ReleaseConnection(sqlConn);  
  
        }  
  
    }  
    ```  
  
### <a name="flat-file-source-example"></a>Exemplo de fonte de arquivos simples  
 Esse exemplo demonstra um componente de origem que usa um gerenciador de conexões de arquivos simples existente para carregar dados de um arquivo simples no fluxo de dados. Os dados de fonte de arquivo simples são criados através de sua exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Use o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exportar a tabela **Person.Address** do banco de dados de exemplo **AdventureWorks** para um arquivo simples delimitado por vírgula. Esse exemplo usa o nome de arquivo ExportedAddresses.txt.  
  
2.  Crie um gerenciador de conexões de arquivos simples que se conecta ao arquivo de dados exportado.  
  
3.  Adicione um novo componente Script à superfície do designer Fluxo de Dados e configure-o como uma origem.  
  
4.  Abra o **Editor de Transformação Scripts**. Na página **Entradas e Saídas**, renomeie a saída padrão com um nome mais descritivo, como **MyAddressOutput**. Adicione e configure as duas colunas de saída, **AddressID** e **City**.  
  
5.  Na página **Gerenciadores de Conexões**, adicione ou crie o gerenciador de conexões de Arquivos Simples usando um nome descritivo como **MyFlatFileSrcConnectionManager**.  
  
6.  Na página **Script**, clique em **Editar Script** e insira o script a seguir. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de Transformação Scripts**.  
  
7.  Crie e configure um componente de destino, como um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o componente de destino de exemplo demonstrado em [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Depois, conecte o componente de origem ao destino. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Crie uma tabela de destino executando o seguinte comando [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados **AdventureWorks**:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Execute o exemplo.  
  
    ```vb  
    Imports System.IO  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Private textReader As StreamReader  
        Private exportedAddressFile As String  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connMgr As IDTSConnectionManager100 = _  
                Me.Connections.MyFlatFileSrcConnectionManager  
            exportedAddressFile = _  
                CType(connMgr.AcquireConnection(Nothing), String)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
            MyBase.PreExecute()  
            textReader = New StreamReader(exportedAddressFile)  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Dim nextLine As String  
            Dim columns As String()  
  
            Dim delimiters As Char()  
            delimiters = ",".ToCharArray  
  
            nextLine = textReader.ReadLine  
            Do While nextLine IsNot Nothing  
                columns = nextLine.Split(delimiters)  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = columns(0)  
                    .City = columns(3)  
                End With  
                nextLine = textReader.ReadLine  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
            MyBase.PostExecute()  
            textReader.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.IO;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        private StreamReader textReader;  
        private string exportedAddressFile;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;  
            exportedAddressFile = (string)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
            base.PreExecute();  
            textReader = new StreamReader(exportedAddressFile);  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            string nextLine;  
            string[] columns;  
  
            char[] delimiters;  
            delimiters = ",".ToCharArray();  
  
            nextLine = textReader.ReadLine();  
            while (nextLine != null)  
            {  
                columns = nextLine.Split(delimiters);  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = columns[0];  
                    MyAddressOutputBuffer.City = columns[3];  
                }  
                nextLine = textReader.ReadLine();  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            base.PostExecute();  
            textReader.Close();  
  
        }  
  
    }  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [Desenvolvendo um componente de origem personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  
