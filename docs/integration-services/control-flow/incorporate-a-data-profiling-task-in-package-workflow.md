---
title: Incorporar uma tarefa Criação de Perfil de Dados no fluxo de trabalho do pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a0b1b7e7a0cecb2f71d8e326615bb25259ca0fcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727639"
---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>Incorporar uma tarefa Criação de Perfil de Dados no fluxo de trabalho do pacote

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  As tarefas de criação de perfil e limpeza de dados não são candidatas a um processo automatizado em seus estágios iniciais. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a saída da tarefa Criação de Perfil de Dados normalmente exige uma análise visual e uma opinião humana para determinar se as violações relatadas são significativas ou demasiadas. Mesmo depois de reconhecer os problemas de qualidade dos dados, ainda é necessário fazer um planejamento cuidadoso para escolher a melhor abordagem de limpeza.  
  
 No entanto, depois de estabelecer os critérios de qualidade dos dados, você talvez queira automatizar a análise e limpeza periódicas da fonte de dados. Considere estes cenários:  
  
-   **Verificando a qualidade dos dados antes de uma carga incremental**. Use a tarefa Criação de Perfil de Dados para calcular o Perfil de Razão Nula de Coluna dos novos dados previstos para a coluna CustomerName em uma tabela Clientes. Se a porcentagem dos valores nulos for superior a 20%, envie uma mensagem de email com a saída de perfil para o operador e encerre o pacote. Caso contrário, continue a carga incremental.  
  
-   **Automatizando a limpeza quando as condições especificadas são atendidas**. Use a tarefa Criação de Perfil de Dados para calcular o Perfil de Inclusão de Valor da coluna Estado de uma tabela de pesquisa de estados e da coluna Código Postal/CEP de uma coluna de pesquisa de códigos postais. Se a intensidade de inclusão dos valores de estado for inferior a 80%, mas a intensidade de inclusão dos valores de código postal/CEP for superior a 99%, esses resultados indicam duas coisas. Primeiro, os dados de estado são incorretos. Segundo, os dados de código postal/CEP são corretos. Inicie uma tarefa Fluxo de Dados que limpa os dados de estado executando uma pesquisa do valor de estado correto a partir do valor de código postal/CEP atual.  
  
 Depois de estabelecer um fluxo de trabalho no qual é possível incorporar a tarefa Fluxo de Dados, você precisa entender as etapas necessárias para adicionar essa tarefa. A próxima seção descreve o processo geral de incorporação da tarefa Fluxo de Dados. As duas seções finais descrevem como conectar a tarefa Fluxo de Dados diretamente a uma fonte de dados ou aos dados transformados do Fluxo de Dados.  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>Definindo um fluxo de trabalho geral para a tarefa Fluxo de Dados  
 O procedimento a seguir descreve a abordagem geral de uso da saída da tarefa Criação de Perfil de Dados no fluxo de trabalho de um pacote.  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>Para usar a saída da tarefa Criação de Perfil de Dados programaticamente em um pacote  
  
1.  Adicione e configure a tarefa Criação de Perfil de Dados em um pacote.  
  
2.  Configure as variáveis de pacote para manter os valores que deseja recuperar dos resultados de perfil.  
  
3.  Adicione e configure uma tarefa Script. Conecte a tarefa Script à tarefa Criação de Perfil de Dados. Na tarefa Script, grave o código que lê os valores desejados do arquivo de saída da tarefa Criação de Perfil de Dados e preencha as variáveis de pacote.  
  
4.  Nas restrições de precedência que conectam a tarefa Script às ramificações de downstream do fluxo de trabalho, grave expressões que usem os valores das variáveis para dirigir o fluxo de trabalho.  
  
 Ao incorporar a tarefa Criação de Perfil de Dados no fluxo de trabalho de um pacote, tenha esses dois recursos da tarefa em mente:  
  
-   **Saída da tarefa**. A tarefa Criação de Perfil de Dados grava sua saída em um arquivo ou uma variável de pacote em formato XML, de acordo com o esquema DataProfile.xsd. Portanto, é necessário consultar a saída XML se você desejar usar os resultados de perfil no fluxo de trabalho condicional de um pacote. Você pode usar a linguagem de consulta Xpath facilmente para consultar essa saída XML. Para estudar a estrutura dessa saída XML, você pode abrir um arquivo de saída de amostra ou o próprio esquema. Para abrir o arquivo de saída ou o esquema, use o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], outro editor de XML, ou um editor de texto como o Bloco de Notas.  
  
    > [!NOTE]  
    >  Alguns resultados de perfil exibidos no Visualizador de Perfil de Dados são valores calculados que não são encontrados diretamente na saída. Por exemplo, a saída do Perfil de Razão Nula de Coluna contém o número total de linhas e o número de linhas que contêm valores nulos. É necessário consultar esses dois valores e, em seguida, calcular a porcentagem de linhas que contêm valores nulos para obter a razão nula de consulta.  
  
-   **Entrada da tarefa**. A tarefa Criação de Perfil de Dados lê sua entrada a partir de tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Portanto, é necessário salvar os dados que estejam na memória nas tabelas de preparação se você desejar criar perfis de dados que já tenham sido carregados e transformados no fluxo de dados.  
  
 As seções a seguir aplicam esse fluxo de trabalho geral à criação de perfis de dados oriundos diretamente de uma fonte de dados externa ou transformados a partir da tarefa Fluxo de Dados. Essas seções também mostram como controlar os requisitos de entrada e saída da tarefa Fluxo de Dados.  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>Conectando a tarefa Criação de Perfil de Dados diretamente a uma fonte de dados externa  
 A tarefa Criação de Perfil de Dados pode criar perfis de dados oriundos diretamente de uma fonte de dados.  Para ilustrar esse recurso, o exemplo a seguir usa a tarefa Criação de Perfil de Dados para calcular um Perfil de Razão Nula de Coluna nas colunas da tabela Person.Address no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Em seguida, esse exemplo usa uma tarefa Script para recuperar os resultados do arquivo de saída e popular as variáveis de pacote que podem ser usadas para direcionar o fluxo de trabalho.  
  
> [!NOTE]  
>  A coluna AddressLine2 foi selecionada para este exemplo porque contém uma porcentagem alta de valores nulos.  
  
 Este exemplo consiste nas seguintes etapas:  
  
-   Configuração de gerenciadores de conexões que se conectam à fonte de dados externa e ao arquivo de saída que vai conter os resultados do perfil.  
  
-   Configuração das variáveis de pacote que vão manter os valores exigidos pela tarefa Criação de Perfil de Dados.  
  
-   Configuração da tarefa Criação de Perfil de Dados para calcular o Perfil de Razão Nula de Coluna.  
  
-   Configuração da tarefa Script para funcionar na saída XML da tarefa Criação de Perfil de Dados.  
  
-   Configuração das restrições de precedência que vão controlar quais ramificações de downstream do fluxo de trabalho são executadas com base nos resultados da tarefa Criação de Perfil de Dados.  
  
### <a name="configure-the-connection-managers"></a>Configurar os gerenciadores de conexões  
 Para este exemplo, há dois gerenciadores de conexões:  
  
-   Um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que se conecta ao banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
-   Um gerenciador de conexões de arquivos que cria o arquivo de saída que armazenará os resultados da tarefa Criação de Perfil de Dados.  
  
##### <a name="to-configure-the-connection-managers"></a>Para configurar os gerenciadores de conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], crie um novo pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Adicione um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] ao pacote. Configure esse gerenciador de conexões para usar o Provedor de Dados NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) e conecte-o a uma instância disponível do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
     Por padrão, o gerenciador de conexões tem o seguinte nome: \<nome do servidor>.AdventureWorks1.  
  
3.  Adicione um gerenciador de conexões de arquivos ao pacote. Configure esse gerenciador de conexões para criar o arquivo de saída para a tarefa Criação de Perfil de Dados.  
  
     Este exemplo usa o nome de arquivo DataProfile1.xml. Por padrão, o gerenciador de conexões tem o mesmo nome do arquivo.  
  
### <a name="configure-the-package-variables"></a>Configure as variáveis de pacote  
 Este exemplo usa duas variáveis de pacote:  
  
-   A variável ProfileConnectionName passa o nome do gerenciador de conexões de arquivos para a tarefa Script.  
  
-   A variável AddressLine2NullRatio retira a razão nula calculada para esta coluna da tarefa Script do pacote.  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>Para configurar as variáveis de pacote que armazenarão os resultados de perfil  
  
-   Na janela **Variáveis** , adicione e configure as duas seguintes variáveis de pacote:  
  
    -   Insira o nome, **ProfileConnectionName**, para uma das variáveis e defina o tipo dessa variável como **String**.  
  
    -   Insira o nome, **AddressLine2NullRatio**, para a outra variável e defina o tipo dessa variável como **Double**.  
  
### <a name="configure-the-data-profiling-task"></a>Configurar a tarefa Criação de Perfil de Dados  
 A tarefa Criação de Perfil de Dados deve ser configurada do seguinte modo:  
  
-   Para usar os dados fornecidos pelo gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] como entrada.  
  
-   Para executar um Perfil de Razão Nula de Coluna nos dados de entrada.  
  
-   Para salvar os resultados de perfil no arquivo que é associado ao gerenciador de conexões de arquivos.  
  
##### <a name="to-configure-the-data-profiling-task"></a>Para configurar a tarefa Criação de Perfil de Dados  
  
1.  Para o Fluxo de Controle, adicione uma tarefa Criação de Perfil de Dados.  
  
2.  Abra o **Editor de Tarefa Criação de Perfil de Dados** para configurar a tarefa.  
  
3.  Na página **Geral** do editor, para **Destino**, selecione o nome do gerenciador de conexões de arquivos configurado anteriormente.  
  
4.  Na página **Solicitações de Perfil** do editor, crie um novo Perfil de Razão Nula de Coluna.  
  
5.  No painel **Propriedades da solicitação** , para **ConnectionManager**, selecione o gerenciador de conexões do [!INCLUDE[vstecado](../../includes/vstecado-md.md)] configurado anteriormente. Em seguida, para **TableOrView**, selecione Person.Address.  
  
6.  Feche o Editor de Tarefa Criação de Perfil de Dados.  
  
### <a name="configure-the-script-task"></a>Configurar a tarefa Script  
 A tarefa Script deve ser configurada para recuperar os resultados do arquivo de saída e preencher as variáveis de pacote que foram configuradas anteriormente.  
  
##### <a name="to-configure-the-script-task"></a>Para configurar a tarefa Script  
  
1.  Para o Fluxo de Controle, adicione uma tarefa Script.  
  
2.  Conecte a tarefa Script à tarefa Criação de Perfil de Dados.  
  
3.  Abra o **Editor da Tarefa Script** para configurar a tarefa.  
  
4.  Na página **Script** , selecione a linguagem de programação desejada. Em seguida, disponibilize as duas variáveis de pacote para o script:  
  
    1.  Para **ReadOnlyVariables**, selecione **ProfileConnectionName**.  
  
    2.  Para **ReadWriteVariables**, selecione **AddressLine2NullRatio**.  
  
5.  Selecione **Editar Script** para abrir o ambiente de desenvolvimento de script.  
  
6.  Adicione uma referência ao namespace System.Xml.  
  
7.  Insira o código de amostra que corresponde à sua linguagem de programação:  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "https://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "https://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  O código de amostra exibido neste procedimento demonstra como carregar a saída da tarefa Criação de Perfil de Dados de um arquivo. Para carregar a saída da tarefa Criação de Perfil de Dados a partir de uma variável de pacote, veja o código de amostra alternativo exibido depois desse procedimento.  
  
8.  Feche o ambiente de desenvolvimento de script e, em seguida, o Editor da Tarefa Script.  
  
#### <a name="alternative-code-reading-the-profile-output-from-a-variable"></a>Código alternativo – Lendo a saída de perfil com base em uma variável  
 O procedimento anterior mostra como carregar a saída da tarefa Criação de Perfil de Dados com base em um arquivo. No entanto, como método alternativo, você pode carregar essa saída a partir de uma variável de pacote. Para carregar a saída a partir de uma variável, faça as seguintes alterações no código de amostra:  
  
-   Chame o método **LoadXml** da classe **XmlDocument** em vez do método **Load** .  
  
-   No Editor da Tarefa Script, adicione o nome da variável de pacote que contém a saída de perfil à lista **ReadOnlyVariables** da tarefa.  
  
-   Passe o valor de cadeia da variável ao método **LoadXML** , como mostrado no código de exemplo a seguir. (Este exemplo usa “ProfileOutput” como o nome da variável de pacote que contém a saída de perfil.)  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>Configurar as restrições de precedência  
 As restrições de precedência devem ser configuradas para controlar quais ramificações de downstream do fluxo de trabalho são executadas com base nos resultados da tarefa Criação de Perfil de Dados.  
  
##### <a name="to-configure-the-precedence-constraints"></a>Para configurar as restrições de precedência  
  
-   Nas restrições de precedência que conectam a tarefa Script às ramificações de downstream do fluxo de trabalho, grave expressões que usem os valores das variáveis para dirigir o fluxo de trabalho.  
  
     Por exemplo, você pode definir a **Operação de avaliação** da restrição de precedência como **Expressão e Restrição**. Em seguida, você pode usar `@AddressLine2NullRatio < .90` como o valor da expressão. Desse modo, o fluxo de trabalho segue o caminho selecionado quando as tarefas anteriores são executadas com êxito e quando a porcentagem de valores nulos na coluna selecionada é inferior a 90%.  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>Conectando a tarefa Criação de Perfil de Dados aos dados transformados do fluxo de dados  
 Em vez de criar um perfil de dados diretamente a partir de uma fonte de dados, você pode salvar os dados que já tenham sido carregados e transformados no fluxo de dados. No entanto, a tarefa Criação de Perfil de Dados funciona somente com dados persistidos, não com dados da memória. Portanto, você deve primeiro usar um componente de destino para salvar os dados transformados em uma tabela de preparação.  
  
> [!NOTE]  
>  Ao configurar a tarefa Criação de Perfil de Dados, é necessário selecionar tabelas e colunas existentes. Portanto, você deve criar a tabela de preparação em tempo de design antes de configurar a tarefa. Em outras palavras, esse cenário não permite o uso de uma tabela temporária criada em tempo de execução.  
  
 Depois de salvar os dados em uma tabela de preparação, você pode fazer o seguinte:  
  
-   Usar a tarefa Criação de Perfil de Dados para criar perfis de dados.  
  
-   Usar uma tarefa Script para ler os resultados conforme descrito anteriormente neste tópico.  
  
-   Usar esses resultados para dirigir o fluxo de trabalho subsequente do pacote.  
  
 O procedimento a seguir fornece a abordagem geral de uso da tarefa Criação de Perfil de Dados para criar perfis dos dados que foram transformados pelo fluxo de dados. Muitas etapas são similares às descritas anteriormente para criar perfis de dados oriundos diretamente de uma fonte de dados externa. Consulte as etapas anteriores se desejar obter mais informações sobre como configurar os diversos componentes.  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>Para usar a tarefa Criação de Perfil de Dados no fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], crie um pacote.  
  
2.  No Fluxo de Dados, adicione, configure e conecte as origens e transformações adequadas.  
  
3.  No Fluxo de Dados, adicione, configure e conecte um componente de destino que salva os dados transformados em uma tabela de preparação.  
  
4.  No Fluxo de Controle, adicione e configure uma tarefa Criação de Perfil de Dados que calcule os perfis desejados para os dados transformados na tabela de preparação. Conecte a tarefa Criação de Perfil de Dados à tarefa Fluxo de Dados.  
  
5.  Configure as variáveis de pacote para manter os valores que deseja recuperar dos resultados de perfil.  
  
6.  Adicione e configure uma tarefa Script. Conecte a tarefa Script à tarefa Criação de Perfil de Dados. Na tarefa Script, grave o código que lê os valores desejados da saída da tarefa Criação de Perfil de Dados e preencha as variáveis de pacote.  
  
7.  Nas restrições de precedência que conectam a tarefa Script às ramificações de downstream do fluxo de trabalho, grave expressões que usem os valores das variáveis para dirigir o fluxo de trabalho.  
  
## <a name="see-also"></a>Consulte Também  
 [Configuração da tarefa Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)   
 [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md)  
  
  
