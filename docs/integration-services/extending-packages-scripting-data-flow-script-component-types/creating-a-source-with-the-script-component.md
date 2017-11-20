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
- docset-sql-devref
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
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4944c3d5752da21fed90f16a38a33b4fad41515
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-source-with-the-script-component"></a>Criando uma fonte com o componente Script
  Você usa um componente de origem no fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para carregar dados de uma fonte de dados a serem passados para transformações e destinos downstream. Normalmente, você se conecta à fonte de dados por um gerenciador de conexões existente.  
  
 Para obter uma visão geral do componente Script, consulte [estendendo o fluxo de dados com o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 O componente Script e o código de infraestrutura gerado para você simplificam significativamente o processo de desenvolvimento de um componente de fluxo de dados personalizado. Contudo, para compreender o funcionamento do componente Script, talvez seja útil ler as etapas envolvidas no desenvolvimento de um componente de fluxo de dados personalizado. Consulte a seção [desenvolvendo um componente de fluxo de dados personalizada](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), especialmente o tópico [desenvolvendo um componente de origem personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md).  
  
## <a name="getting-started-with-a-source-component"></a>Guia de introdução com um componente de origem  
 Quando você adiciona um componente Script ao painel fluxo de dados do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, o **Selecionar tipo de componente de Script** caixa de diálogo é aberta e solicita que você selecione um script de origem, destino ou transformação. Na caixa de diálogo, selecione **fonte**.  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>Configurando um componente de origem em modo do design de metadados  
 Depois de selecionar esta opção para criar um componente de origem, você deve configurar o componente usando o **Editor de transformação scripts**. Para obter mais informações, consulte [Configurando o componente Script no Editor de componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Um componente de origem de fluxo de dados não tem entradas e dá suporte a uma ou mais saídas. Configurar as saídas do componente é uma das etapas que você deve concluir no modo de design de metadados, usando o **Editor de transformação scripts**, antes de escrever seu script personalizado.  
  
 Você também pode especificar a linguagem de script definindo a **ScriptLanguage** propriedade o **Script** página do **Editor de transformação scripts**.  
  
> [!NOTE]  
>  Para definir a linguagem de script padrão para componentes de Script e tarefas de Script, use o **linguagem de script** opção o **geral** página do **opções** caixa de diálogo. Para obter mais informações, consulte [General Page](~/integration-services/control-flow/script-task-editor-general-page.md).  
  
### <a name="adding-connection-managers"></a>Adicionando gerenciadores de conexões  
 Em geral, um componente de origem usa um gerenciador de conexões existente para se conectar à fonte de dados da qual ele carrega dados para o fluxo de dados. No **gerenciadores de Conexão** página do **Editor de transformação scripts**, clique em **adicionar** para adicionar o Gerenciador de conexão apropriado.  
  
 Contudo, um gerenciador de conexões é apenas uma unidade conveniente que encapsula e armazena as informações necessárias para a conexão a uma fonte de dados de um tipo específico. Escreva seu próprio código personalizado para carregar ou salvar seus dados e, possivelmente, para também abrir e fechar a conexão à fonte de dados.  
  
 Para obter informações gerais sobre como usar gerenciadores de conexão com o componente Script, consulte [se conectar a fontes de dados no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
 Para obter mais informações sobre o **gerenciadores de Conexão** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; Página gerenciadores de Conexão &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>Configurando saídas e colunas de saída  
 Um componente de origem não tem nenhuma entrada e dá suporte a uma ou mais saídas. No **entradas e saídas** página do **Editor de transformação scripts**, uma única saída foi criada por padrão, mas nenhuma coluna de saída foi criada. Nessa página do editor, você pode precisar ou querer configurar os itens a seguir.  
  
-   Adicione e configure colunas de saída manualmente para cada saída. Selecione a pasta de colunas de saída para cada saída e, em seguida, use o **adicionar coluna** e **Remover coluna** botões para gerenciar as colunas de saída para cada saída do componente de origem. Posteriormente, você fará referência às colunas de saída do seu script pelos nomes atribuídos aqui, usando as propriedades de acessador digitadas criadas para você no código gerado automaticamente.  
  
-   Talvez você queira criar uma ou mais saídas adicionais, tais como uma saída de erro simulada para linhas que contêm valores inesperados. Use o **adicionar saída** e **remover saída** botões para gerenciar as saídas do componente de origem. Todas as linhas de entrada são direcionadas para todas as saídas disponíveis, a menos que você também especificar um valor diferente de zero idêntico para o **ExclusionGroup** propriedade das saídas onde você pretende direcionar cada linha a apenas uma das saídas que compartilham o mesmo **ExclusionGroup** valor. O valor de inteiro específico selecionado para identificar o **ExclusionGroup** não é significativa.  
  
    > [!NOTE]  
    >  Você também pode usar uma diferente de zero **ExclusionGroup** valor da propriedade com uma única saída quando você não deseja que todas as linhas de saída. Nesse caso, no entanto, você deve chamar explicitamente o **DirectRowTo\<outputbuffer >** método para cada linha que você deseja enviar para a saída.  
  
-   Talvez você queira atribuir um nome amigável às saídas. Posteriormente, você fará referência às saídas pelos nomes no seu script, usando as propriedades de acessador digitadas, criadas para você no código gerado automaticamente.  
  
-   Normalmente a várias saídas no mesmo **ExclusionGroup** têm as mesmas colunas de saída. Porém, se você estiver criando uma saída de erro simulada, talvez queira adicionar mais colunas para armazenar informações de erro. Para obter informações sobre como o mecanismo de fluxo de dados processa linhas de erro, consulte [usando saídas de erro em um componente de fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md). No componente Script, contudo, escreva seu próprio código para preencher as colunas adicionais com informações de erro apropriadas. Para obter mais informações, consulte [simulando uma saída de erro para o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Para obter mais informações sobre o **entradas e saídas** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; entradas e saídas de página &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md).  
  
### <a name="adding-variables"></a>Adicionando variáveis  
 Se houver qualquer variáveis cujos valores você deseja usar em seu script, você pode adicioná-las a **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade de **Script** página do **Editor de transformação scripts**.  
  
 Ao inserir diversas variáveis nos campos de propriedade, separe os nomes delas por vírgulas. Você também pode inserir diversas variáveis clicando no botão de reticências (**...** ) ao lado de **ReadOnlyVariables** e **ReadWriteVariables** campos de propriedade e selecionar as variáveis no **selecionar variáveis** caixa de diálogo .  
  
 Para obter informações gerais sobre como usar variáveis com o componente Script, consulte [usando variáveis no componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Para obter mais informações sobre o **Script** página do **Editor de transformação scripts**, consulte [Editor de transformação scripts &#40; Script de página &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>Gerando scripts de um componente de origem em modo do design de código  
 Depois que você configurou os metadados para seu componente, abra o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE para codificar seu script personalizado. Para abrir o VSTA, clique em **Editar Script** no **Script** página do **Editor de transformação scripts**. Você pode escrever seu script usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual c#, dependendo da linguagem de script selecionada para o **ScriptLanguage** propriedade.  
  
 Para obter informações importantes que se aplica a todos os tipos de componentes criados usando o componente Script, consulte [codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Compreendendo o código gerado automaticamente  
 Quando você abre o VSTA IDE depois de criar e configurar um componente de origem, o editável **ScriptMain** classe aparece no editor de código. Você escreve seu código personalizado **ScriptMain** classe.  
  
 O **ScriptMain** classe inclui um stub para o **CreateNewOutputRows** método. O **CreateNewOutputRows** é o método mais importante em um componente de origem.  
  
 Se você abrir o **Explorador de projeto** janela no VSTA, você pode ver que o componente Script também gerou somente leitura **BufferWrapper** e **ComponentWrapper** projeto itens. O **ScriptMain** classe herda de **UserComponent** classe no **ComponentWrapper** item de projeto.  
  
 Em tempo de execução, o mecanismo de fluxo de dados invoca o **PrimeOutput** método no **UserComponent** de classe que substitui o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> método do <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> classe pai. O **PrimeOutput** método por sua vez chama os seguintes métodos:  
  
1.  O **CreateNewOutputRows** método, o que você substitui em **ScriptMain** para adicionar linhas da fonte de dados para a saída de buffers, que são vazios no início.  
  
2.  O **FinishOutputs** método, que é vazio por padrão. Substitua este método em **ScriptMain** para executar qualquer processamento que é necessário para concluir a saída.  
  
3.  Particular **MarkOutputsAsFinished** método, que chama o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> método o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> pai classe para indicar ao mecanismo de fluxo de dados que a saída está concluída. Você não precisa chamar **SetEndOfRowset** explicitamente em seu próprio código.  
  
### <a name="writing-your-custom-code"></a>Escrevendo seu código personalizado  
 Para concluir a criação de um componente de origem personalizado, talvez você queira gravar o script nos métodos a seguir disponíveis no **ScriptMain** classe.  
  
1.  Substituir o **AcquireConnections** método para se conectar à fonte de dados externa. Extraia o objeto de conexão, ou as informações de conexão requeridas, do gerenciador de conexões.  
  
2.  Substituir o **PreExecute** método para carregar dados, se você pode carregar todos os dados de origem ao mesmo tempo. Por exemplo, você pode executar um **SqlCommand** contra um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados e carregar todos os dados de origem ao mesmo tempo em um **SqlDataReader**. Se você precisar carregar o código-fonte dados, uma linha por vez (por exemplo, ao ler um arquivo de texto), você pode carregar os dados como loop pelas linhas **CreateNewOutputRows**.  
  
3.  Use substituído **CreateNewOutputRows** método para adicionar novas linhas aos buffers de saída vazios e preencher os valores de cada coluna nas novas linhas de saída. Use o **AddRow** método de cada buffer de saída para adicionar uma linha nova vazia e, em seguida, defina os valores de cada coluna. Em geral, você copia valores das colunas carregadas a partir da origem externa.  
  
4.  Substituir o **PostExecute** método para concluir o processamento de dados. Por exemplo, você pode fechar o **SqlDataReader** que você usou para carregar dados.  
  
5.  Substituir o **ReleaseConnections** método para desconectar da fonte de dados externa, caso necessário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o código personalizado que é necessário o **ScriptMain** classe para criar um componente de origem.  
  
> [!NOTE]  
>  Esses exemplos usam o **Person. address** tabela o **AdventureWorks** banco de dados de exemplo e passam a primeira e a quarta colunas, o **intAddressID** e  **Cidade nvarchar (30)** colunas, por meio do fluxo de dados. Os mesmos dados são usados nos exemplos de origem, transformação e destino nessa seção. Pré-requisitos e suposições adicionais são documentados para cada exemplo.  
  
### <a name="adonet-source-example"></a>Exemplo de origem do ADO.NET  
 Este exemplo demonstra um componente de origem que usa um existente [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão para carregar dados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela no fluxo de dados.  
  
 Se você quiser executar esse código de exemplo, configure o pacote e o componente desta forma:  
  
1.  Criar um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão que usa o **SqlClient** provedor conectar-se para o **AdventureWorks** banco de dados.  
  
2.  Adicione um novo componente Script à superfície do designer Fluxo de Dados e configure-o como uma origem.  
  
3.  Abra o **Editor de transformação scripts**. Sobre o **entradas e saídas** página, renomeie a saída padrão com um nome mais descritivo, como **MyAddressOutput**e adicione e configure as duas colunas de saída, **AddressID**e **City**.  
  
    > [!NOTE]  
    >  Certifique-se de alterar o tipo de dados de **City** coluna de saída para DT_WSTR.  
  
4.  Sobre o **gerenciadores de Conexão** página, adicione ou crie o [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Gerenciador de conexão e dê a ele um nome, como **MyADONETConnection**.  
  
5.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de transformação scripts**.  
  
6.  Criar e configurar um componente de destino, como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino ou o componente de destino de exemplo demonstrado em [criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md), que espera o  **AddressID** e **City** colunas. Depois, conecte o componente de origem ao destino. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Você pode criar uma tabela de destino executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] do **AdventureWorks** banco de dados:  
  
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
  
1.  Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação para exportar o **Person. address** tabela o **AdventureWorks** banco de dados de exemplo em um arquivo simples delimitado por vírgulas. Esse exemplo usa o nome de arquivo ExportedAddresses.txt.  
  
2.  Crie um gerenciador de conexões de arquivos simples que se conecta ao arquivo de dados exportado.  
  
3.  Adicione um novo componente Script à superfície do designer Fluxo de Dados e configure-o como uma origem.  
  
4.  Abra o **Editor de transformação scripts**. Sobre o **entradas e saídas** página, renomeie a saída padrão com um nome mais descritivo, como **MyAddressOutput**. Adicionar e configurar as duas colunas de saída, **AddressID** e **City**.  
  
5.  Sobre o **gerenciadores de Conexão** página, adicione ou crie a conexão de arquivo simples gerenciador, usando um nome descritivo, como **MyFlatFileSrcConnectionManager**.  
  
6.  Sobre o **Script** , clique em **Editar Script** e insira o script seguinte. Em seguida, feche o ambiente de desenvolvimento de script e o **Editor de transformação scripts**.  
  
7.  Criar e configurar um componente de destino, como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino ou o componente de destino de exemplo demonstrado em [criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Depois, conecte o componente de origem ao destino. (Você pode conectar uma origem diretamente a um destino, sem transformações.) Você pode criar uma tabela de destino executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] do **AdventureWorks** banco de dados:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Criando um destino com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [Desenvolvendo um componente de origem personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  

