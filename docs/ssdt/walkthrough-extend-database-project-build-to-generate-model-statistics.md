---
title: 'Passo a passo: estender a compilação do projeto de banco de dados para gerar as estatísticas do modelo | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d44935ce-63bf-46df-976a-5a54866c8119
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6433702a0b265053d8a6124adcca065b3f876f25
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093670"
---
# <a name="walkthrough-extend-database-project-build-to-generate-model-statistics"></a>Passo a passo: Estenda a Compilação do Projeto de Banco de Dados para Gerar as Estatísticas do Modelo
Você pode criar um colaborador de compilação para executar ações personalizadas ao compilar um projeto de banco de dados. Neste passo a passo, você cria um colaborador de compilação chamado ModelStatistics que gera estatísticas do modelo de banco de dados SQL quando você cria um projeto de banco de dados. Como esse colaborador de compilação usa parâmetros quando você compila, algumas etapas adicionais serão necessárias.  
  
Neste passo a passo, você realizará as tarefas principais a seguir:  
  
-   [Criar um colaborador de compilação](#CreateBuildContributor)  
  
-   [Instalar o colaborador de compilação](#InstallBuildContributor)  
  
-   [Testar seu colaborador de compilação](#TestBuildContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
Você precisará dos seguintes componentes para concluir este passo a passo:  
  
-   Você deverá ter instalada uma versão do Visual Studio que inclui o SSDT (SQL Server Data Tools) e dá suporte ao desenvolvimento em C# ou VB.  
  
-   Você deve ter um projeto SQL que contenha objetos de SQL.  
  
> [!NOTE]  
> Este passo a passo é destinado a usuários que já estão familiarizados com os recursos do SQL do SSDT. Você também já deverá estar familiarizado com os conceitos básicos do Visual Studio, por exemplo, como criar uma biblioteca de classe e como usar o editor de código para adicionar código a uma classe.  
  
## <a name="build-contributor-background"></a>Plano de fundo do colaborador de compilação  
Os colaboradores de compilação são executados durante a compilação do projeto, depois que o modelo que representa o projeto tiver sido gerado, mas antes de o projeto ser salvo no disco. Eles podem ser usados para diversos cenários, como  
  
-   Validando o conteúdo do modelo e relatando erros de validação para o chamador. Isso pode ser feito adicionando erros a uma lista passada como um parâmetro para o método OnExecute.  
  
-   Gerando as estatísticas do modelo e relatando-as ao usuário. Esse é o exemplo mostrado aqui.  
  
O ponto de entrada principal para colaboradores de compilação é o método OnExecute. Todas as classes que herdam do BuildContributor devem implementar esse método. Um objeto BuildContributorContext é passado para este método – ele contém todos os dados relevantes para a compilação, como um modelo de banco de dados, as propriedades de compilação e os argumentos/arquivos a serem usados por colaboradores de compilação.  
  
**TSqlModel e a API do modelo de banco de dados**  
  
O objeto mais útil será o modelo de banco de dados, representado por um objeto TSqlModel. Esta é uma representação lógica de um banco de dados, incluindo todas as tabelas, exibições e outros elementos, mais as relações entre eles. Há um esquema fortemente tipado que pode ser usado para consultar tipos específicos de elementos e relações interessantes completas. Você verá exemplos de como isso é usado no código de instruções passo a passo.  
  
Veja alguns dos comandos usados pelo colaborador de exemplo neste passo a passo:  
  
|**Classe**|**Método/propriedade**|**Descrição**|  
|-------------|------------------------|-------------------|  
|[TSqlModel](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)|GetObjects()|Consulta o modelo para objetos e é o ponto de entrada principal para a API do modelo. Apenas os tipos de nível superior como uma Tabela ou Exibição podem ser consultados – os tipos como Colunas podem ser encontrados desviando o modelo. Se nenhum filtro ModelTypeClass for especificado, todos os tipos de nível superior serão retornados.|  
|[TSqlObject](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|GetReferencedRelationshipInstances()|Localiza relações para os elementos referenciados pelo TSqlObject atual. Por exemplo, para uma tabela, isto retornará objetos como as colunas da tabela. Nesse caso, um filtro ModelRelationshipClass pode ser usado para especificar relações exatas para a consulta (por exemplo, usar o filtro “Table.Columns” garantiria que apenas as colunas seriam retornadas).<br /><br />Há vários métodos semelhantes, como GetReferencingRelationshipInstances, GetChildren e GetParent. Consulte a documentação da API para obter mais informações.|  
  
**Identificar com exclusividade seu colaborador**  
  
Durante o processo de compilação, os colaboradores personalizados são carregados de um diretório de extensão padrão. Os colaboradores de compilação são identificados por um atributo [ExportBuildContributor](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.exportbuildcontributorattribute.aspx) . Esse atributo é necessário para que os colaboradores possam ser descobertos. Esse atributo deve ser semelhante ao seguinte:  
  
```  
[ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
  
```  
  
Nesse caso, o primeiro parâmetro para o atributo deve ser um identificador exclusivo – isso será usado para identificar seu colaborador em arquivos de projeto. A prática recomendada é combinar o namespace da biblioteca (neste passo a passo, “ExampleContributors") com o nome da classe (neste passo a passo, “ModelStatistics") para gerar o identificador. Você verá como esse namespace é usado para especificar que seu colaboradores deve ser executado posteriormente no passo a passo.  
  
## <a name="CreateBuildContributor"></a>Criar um colaborador de compilação  
Para criar um colaborador de compilação, você deverá realizar as seguintes tarefas:  
  
-   Criar um projeto de biblioteca de classe e adicionar as referências necessárias.  
  
-   Definir uma classe denominada ModelStatistics que herda de [BuildContributor](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx).  
  
-   Substitua o método OnExecute.  
  
-   Adicione alguns métodos auxiliares privados.  
  
-   Compile o assembly resultante.  
  
#### <a name="to-create-a-class-library-project"></a>Para criar um projeto de biblioteca de classe  
  
1.  Crie um projeto de biblioteca de classe do Visual Basic ou Visual C# denominado MyBuildContributor.  
  
2.  Renomeie o arquivo “Class1.cs” para “ModelStatistics.cs”.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e, depois, clique em **Adicionar referência**.  
  
4.  Selecione a entrada **System.ComponentModel.Composition** e clique em **OK**.  
  
5.  Adicione as referências SQL necessárias: clique com o botão direito do mouse no nó do projeto e clique em **Adicionar Referência**. Clique no botão **Procurar** . Navegue até a pasta **C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\DAC\Bin**. Escolha as entradas **Microsoft.SqlServer.Dac.dll**, **Microsoft.SqlServer.Dac.Extensions.dll**e **Microsoft.Data.Tools.Schema.Sql.dll** e clique em **OK**.  
  
    Em seguida, você começa a adicionar o código à classe.  
  
#### <a name="to-define-the-modelstatistics-class"></a>Para definir a classe ModelStatistics  
  
1.  A classe ModelStatistics processa o modelo de banco de dados passado para o método OnExecute e gera um relatório XML que detalha o conteúdo do modelo.  
  
    No editor de código, atualize o arquivo ModelStatistics.cs para corresponder ao seguinte:  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Linq;  
    using System.Xml.Linq;  
    using Microsoft.Data.Schema;  
    using Microsoft.Data.Schema.Build;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema.SchemaModel;  
    using Microsoft.Data.Schema.Sql;  
  
    namespace ExampleContributors  
    {  
    /// <summary>  
        /// A BuildContributor that generates statistics about a model and saves this to the output directory.  
        /// Will only run if a "GenerateModelStatistics=true" contributor argument is set in the project file, or a targets file.   
        /// Statistics can be sorted by "none, "name" or "value", with "none" being the default sort behavior.  
        ///   
        /// To set contributor arguments in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
        ///     </ContributorArguments>  
        /// <PropertyGroup>      
        ///   
        /// This will generate model statistics when building in Debug mode only - remove the condition to generate in all build modes.  
        /// </summary>  
        [ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
        public class ModelStatistics : BuildContributor  
        {  
            public const string GenerateModelStatistics = "ModelStatistics.GenerateModelStatistics";  
            public const string SortModelStatisticsBy = "ModelStatistics.SortModelStatisticsBy";  
            public const string OutDir = "ModelStatistics.OutDir";  
            public const string ModelStatisticsFilename = "ModelStatistics.xml";  
            private enum SortBy { None, Name, Value };  
            private static Dictionary<string, SortBy> SortByMap = new Dictionary<string, SortBy>(StringComparer.OrdinalIgnoreCase)  
            {  
                { "none", SortBy.None },  
                { "name", SortBy.Name },  
                { "value", SortBy.Value },  
            };  
  
            private SortBy _sortBy = SortBy.None;  
  
            /// <summary>  
            /// Override the OnExecute method to perform actions when you build a database project.  
            /// </summary>  
            protected override void OnExecute(BuildContributorContext context, IList<ExtensibilityError> errors)  
            {  
                // handle related arguments, passed in as part of  
                // the context information.  
                bool generateModelStatistics;  
                ParseArguments(context.Arguments, errors, out generateModelStatistics);  
  
                // Only generate statistics if requested to do so  
                if (generateModelStatistics)  
                {  
                    // First, output model-wide information, such  
                    // as the type of database schema provider (DSP)  
                    // and the collation.  
                    StringBuilder statisticsMsg = new StringBuilder();  
                    statisticsMsg.AppendLine(" ")  
                                 .AppendLine("Model Statistics:")  
                                 .AppendLine("===")  
                                 .AppendLine(" ");  
                    errors.Add(new ExtensibilityError(statisticsMsg.ToString(), Severity.Message));  
  
                    var model = context.Model;  
  
                    // Start building up the XML that will later  
                    // be serialized.  
                    var xRoot = new XElement("ModelStatistics");  
  
                    SummarizeModelInfo(model, xRoot, errors);  
  
                    // First, count the elements that are contained   
                    // in this model.  
                    IList<TSqlObject> elements = model.GetObjects(DacQueryScopes.UserDefined).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "UserDefinedElements", xRoot, errors);  
  
                    // Now, count the elements that are defined in  
                    // another model. Examples include built-in types,  
                    // roles, filegroups, assemblies, and any   
                    // referenced objects from another database.  
                    elements = model.GetObjects(DacQueryScopes.BuiltIn | DacQueryScopes.SameDatabase | DacQueryScopes.System).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "OtherElements", xRoot, errors);  
  
                    // Now, count the number of each type  
                    // of relationship in the model.  
                    SurveyRelationships(model, xRoot, errors);  
  
                    // Determine where the user wants to save  
                    // the serialized XML file.  
                    string outDir;  
                    if (context.Arguments.TryGetValue(OutDir, out outDir) == false)  
                    {  
                        outDir = ".";  
                    }  
                    string filePath = Path.Combine(outDir, ModelStatisticsFilename);  
                    // Save the XML file and tell the user  
                    // where it was saved.  
                    xRoot.Save(filePath);  
                    ExtensibilityError resultArg = new ExtensibilityError("Result was saved to " + filePath, Severity.Message);  
                    errors.Add(resultArg);  
                }  
            }  
  
            /// <summary>  
            /// Examine the arguments provided by the user  
            /// to determine if model statistics should be generated  
            /// and, if so, how the results should be sorted.  
            /// </summary>  
            private void ParseArguments(IDictionary<string, string> arguments, IList<ExtensibilityError> errors, out bool generateModelStatistics)  
            {  
                // By default, we don't generate model statistics  
                generateModelStatistics = false;  
  
                // see if the user provided the GenerateModelStatistics   
                // option and if so, what value was it given.  
                string valueString;  
                arguments.TryGetValue(GenerateModelStatistics, out valueString);  
                if (string.IsNullOrWhiteSpace(valueString) == false)  
                {  
                    if (bool.TryParse(valueString, out generateModelStatistics) == false)  
                    {  
                        generateModelStatistics = false;  
  
                        // The value was not valid from the end user  
                        ExtensibilityError invalidArg = new ExtensibilityError(  
                            GenerateModelStatistics + "=" + valueString + " was not valid.  It can be true or false", Severity.Error);  
                        errors.Add(invalidArg);  
                        return;  
                    }  
                }  
  
                // Only worry about sort order if the user requested  
                // that we generate model statistics.  
                if (generateModelStatistics)  
                {  
                    // see if the user provided the sort option and  
                    // if so, what value was provided.  
                    arguments.TryGetValue(SortModelStatisticsBy, out valueString);  
                    if (string.IsNullOrWhiteSpace(valueString) == false)  
                    {  
                        SortBy sortBy;  
                        if (SortByMap.TryGetValue(valueString, out sortBy))  
                        {  
                            _sortBy = sortBy;  
                        }  
                        else  
                        {  
                            // The value was not valid from the end user  
                            ExtensibilityError invalidArg = new ExtensibilityError(  
                                SortModelStatisticsBy + "=" + valueString + " was not valid.  It can be none, name, or value", Severity.Error);  
                            errors.Add(invalidArg);  
                        }  
                    }  
                }  
            }  
  
            /// <summary>  
            /// Retrieve the database schema provider for the  
            /// model and the collation of that model.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SummarizeModelInfo(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // use a Dictionary to accumulate the information  
                // that will later be output.  
                var info = new Dictionary<string, string>();  
  
                // Two things of interest: the database schema  
                // provider for the model, and the language id and  
                // case sensitivity of the collation of that  
                // model  
                info.Add("Version", model.Version.ToString());  
  
                TSqlObject options = model.GetObjects(DacQueryScopes.UserDefined, DatabaseOptions.TypeClass).FirstOrDefault();  
                if (options != null)  
                {  
                    info.Add("Collation", options.GetProperty<string>(DatabaseOptions.Collation));  
                }  
  
                // Output the accumulated information and add it to   
                // the XML.  
                OutputResult("Basic model info", info, xContainer, errors);  
            }  
  
            /// <summary>  
            /// For a provided list of model elements, count the number  
            /// of elements for each class name, sorted as specified  
            /// by the user.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private void Summarize<T>(IList<T> set, Func<T, string> groupValue, string category, XElement xContainer, IList<ExtensibilityError> errors)  
            { // Use a Dictionary to keep all summarized information  
                var statistics = new Dictionary<string, int>();  
  
                // For each element in the provided list,  
                // count items based on the specified grouping  
                var groups =  
                    from item in set  
                    group item by groupValue(item) into g  
                    select new { g.Key, Count = g.Count() };  
  
                // order the groups as requested by the user  
                if (this._sortBy == SortBy.Name)  
                {  
                    groups = groups.OrderBy(group => group.Key);  
                }  
                else if (this._sortBy == SortBy.Value)  
                {  
                    groups = groups.OrderBy(group => group.Count);  
                }  
  
                // build the Dictionary of accumulated statistics  
                // that will be passed along to the OutputResult method.  
                foreach (var item in groups)  
                {  
                    statistics.Add(item.Key, item.Count);  
                }  
  
                statistics.Add("subtotal", set.Count);  
                statistics.Add("total items", groups.Count());  
  
                // output the results, and build up the XML  
                OutputResult(category, statistics, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Iterate over all model elements, counting the  
            /// styles and types for relationships that reference each   
            /// element  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SurveyRelationships(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // get a list that contains all elements in the model  
                var elements = model.GetObjects(DacQueryScopes.All);  
                // We are interested in all relationships that  
                // reference each element.  
                var entries =  
                    from element in elements  
                    from entry in element.GetReferencedRelationshipInstances(DacExternalQueryScopes.All)  
                    select entry;  
  
                // initialize our counting buckets  
                var composing = 0;  
                var hierachical = 0;  
                var peer = 0;  
  
                // process each relationship, adding to the   
                // appropriate bucket for style and type.  
                foreach (var entry in entries)  
                {  
                    switch (entry.Relationship.Type)  
                    {  
                        case RelationshipType.Composing:  
                            ++composing;  
                            break;  
                        case RelationshipType.Hierarchical:  
                            ++hierachical;  
                            break;  
                        case RelationshipType.Peer:  
                            ++peer;  
                            break;  
                        default:  
                            break;  
                    }  
                }  
  
                // build a dictionary of data to pass along  
                // to the OutputResult method.  
                var stat = new Dictionary<string, int>  
                {  
                    {"Composing", composing},  
                    {"Hierarchical", hierachical},  
                    {"Peer", peer},  
                    {"subtotal", entries.Count()}  
                };  
  
                OutputResult("Relationships", stat, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Performs the actual output for this contributor,  
            /// writing the specified set of statistics, and adding any   
            /// output information to the XML being constructed.  
            /// </summary>  
            private static void OutputResult<T>(string category, Dictionary<string, T> statistics, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                var maxLen = statistics.Max(stat => stat.Key.Length) + 2;  
                var format = string.Format("{{0, {0}}}: {{1}}", maxLen);  
  
                StringBuilder resultMessage = new StringBuilder();  
                //List<ExtensibilityError> args = new List<ExtensibilityError>();  
                resultMessage.AppendLine(category);  
                resultMessage.AppendLine("-----------------");  
  
                // Remove any blank spaces from the category name  
                var xCategory = new XElement(category.Replace(" ", ""));  
                xContainer.Add(xCategory);  
  
                foreach (var item in statistics)  
                {  
                    //Console.WriteLine(format, item.Key, item.Value);  
                    var entry = string.Format(format, item.Key, item.Value);  
                    resultMessage.AppendLine(entry);  
                    // Replace any blank spaces in the element key with  
                    // underscores.  
                    xCategory.Add(new XElement(item.Key.Replace(' ', '_'), item.Value));  
                }  
                resultMessage.AppendLine(" ");  
                errors.Add(new ExtensibilityError(resultMessage.ToString(), Severity.Message));  
            }  
        }  
    }  
  
    ```  
  
    Em seguida, você criará a biblioteca de classe.  
  
### <a name="to-sign-and-build-the-assembly"></a>Para assinar e criar o assembly  
  
1.  No menu **Projeto** , clique em **Propriedades MyBuildContributor**.  
  
2.  Clique na guia **Assinatura** .  
  
3.  Clique em **Assinar o assembly**.  
  
4.  Em **Escolher um arquivo de chave de nome forte**, clique em **<New>**.  
  
5.  Na caixa de diálogo **Criar Chave de Nome Forte** , em **Nome de arquivo de chave**, digite **MyRefKey**.  
  
6.  (opcional) Você pode especificar uma senha para o arquivo de chave de nome forte.  
  
7.  Clique em **OK**.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
9. No menu **Criar** , clique em **Criar Solução**.  
  
    Em seguida, você deve instalar o assembly de modo que ele seja carregado quando você compilar projetos do SQL.  
  
## <a name="InstallBuildContributor"></a>Instalar um colaborador de compilação  
Para instalar um colaborador de compilação, você deverá copiar o assembly e o arquivo .pdb associado à pasta Extensões.  
  
#### <a name="to-install-the-mybuildcontributor-assembly"></a>Para instalar o assembly MyBuildContributor  
  
1.  Em seguida, você copiará as informações de assembly para o diretório Extensões. Quando o Visual Studio iniciar, ele identificará as extensões no diretório e subdiretórios %Arquivos de Programas%\Microsoft SQL Server\110\DAC\Bin\Extensions e as tornará disponíveis para uso.  
  
2.  Copie o arquivo de assembly **MyBuildContributor.dll** do diretório de saída para o diretório %Arquivos de Programas%Microsoft SQL Server\110\DAC\Bin\Extensions.  
  
    > [!NOTE]  
    > Por padrão, o caminho do seu arquivo compilado .dll é YourSolutionPath\YourProjectPath\bin\Debug ou YourSolutionPath\YourProjectPath\bin\Release.  
  
## <a name="TestBuildContributor"></a>Executar ou testar seu Colaborador de Compilação  
Para executar ou testar seu colaborador de compilação, você deverá realizar as seguintes tarefas:  
  
-   Adicionar propriedades ao arquivo .sqlproj que você planeja criar.  
  
-   Compilar o projeto de banco de dados usando MSBuild e fornecendo os parâmetros apropriados.  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>Adicionar Propriedades ao arquivo de projeto SQL (.sqlproj)  
Você sempre deve atualizar o arquivo de projeto SQL para especificar a ID dos colaboradores que você deseja executar. Além disso, como esse colaborador de compilação aceita parâmetros de linha de comando do MSBuild, você deverá alterar o projeto SQL para permitir que os usuários passem esses parâmetros pelo MSBuild.  
  
É possível fazer isso de duas formas:  
  
-   Você pode modificar manualmente o arquivo .sqlproj para adicionar os argumentos necessários. Você pode escolher fazer isso se não quiser reutilizar o colaborador de compilação em um número grande de projetos. Se você escolher esta opção, adicione as seguintes instruções ao arquivo .sqlproj após o primeiro nó de importação no arquivo  
  
    ```  
    /// <PropertyGroup>  
    ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'”>  
    ///         $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
    ///     </ContributorArguments>  
    /// <PropertyGroup>  
  
    ```  
  
-   O segundo método é criar um arquivo de destino que contém argumentos necessários de colaborador. Isso será útil se você estiver usando o mesmo colaborador para vários projetos, porque isso incluirá os valores padrão.  
  
    Nesse caso, crie um arquivo de destino no caminho de extensões do MSBuild:  
  
    1.  Navegue para %Arquivos de programas%\MSBuild\\.  
  
    2.  Crie uma nova pasta “MyContributors” onde os arquivos de destino serão armazenados.  
  
    3.  Crie um novo arquivo “MyContributors.targets” dentro desse diretório, adicione o seguinte texto e salve o arquivo:  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <BuildContributors>$(BuildContributors);ExampleContributors.ModelStatistics</BuildContributors>  
            <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy=name;</ContributorArguments>  
          </PropertyGroup>  
        </Project>  
        ```  
  
    4.  Dentro do arquivo .sqlproj para qualquer projeto que você quiser executar colaboradores, importe o arquivo de destino adicionando a seguinte instrução ao arquivo .sqlproj após o nó \<<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> no arquivo:  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
        ```  
  
Depois que você tiver seguido uma destas abordagens, poderá usar MSBuild para passar parâmetros para compilações de linha de comando.  
  
> [!NOTE]  
> Você sempre deve atualizar a propriedade “BuildContributors” para especificar sua ID de colaborador. Esta é a mesma ID usada no atributo “ExportBuildContributor” no seu arquivo de origem de colaborador. Sem isso, seu colaborador não será executado ao criar o projeto. A propriedade “ContributorArguments” deverá ser atualizada somente se você tiver os argumentos necessários para seu colaborador ser executado.  
  
### <a name="build-the-sql-project"></a>Crie o projeto SQL.  
  
##### <a name="to-rebuild-your-database-project-by-using-msbuild-and-generate-statistics"></a>Para recriar seu projeto de banco de dados usando MSBuild e gerar estatísticas  
  
1.  No Visual Studio, clique com o botão direito do mouse no projeto e selecione “Recompilar”. Isso recompilará o projeto e você deverá ver as estatísticas de modelo geradas, com a saída incluída na saída da compilação e salva em ModelStatistics.xml. Observe que você pode precisar escolher “Mostrar todos os arquivos” no Gerenciador de Soluções para ver o arquivo XML.  
  
2.  Abra um prompt de comando do Visual Studio: no menu **Iniciar**, clique em **Todos os Programas**, clique em **Microsoft Visual Studio <Visual Studio Version>**, clique em **Ferramentas do Visual Studio** e clique em **Prompt de Comando do Visual Studio (<Visual Studio Version>)**.  
  
3.  No prompt de comando, navegue até a pasta que contém seu projeto SQL.  
  
4.  No prompt de comando, digite o seguinte comando:  
  
    ```  
    MSBuild /t:Rebuild MyDatabaseProject.sqlproj /p:BuildContributors=$(BuildContributors);ExampleContributors.ModelStatistics /p:ContributorArguments=$(ContributorArguments);GenerateModelStatistics=true;SortModelStatisticsBy=name;OutDir=.\;  
    ```  
  
    Substitua *MyDatabaseProject* pelo nome do projeto de banco de dados que você deseja compilar. Se você tiver alterado o projeto após a última compilação, poderá usar /t:Build em vez de /t:Rebuild.  
  
    Dentro da saída, você deverá ver as informações de compilação da seguinte maneira:  
  
```  
Model Statistics:  
===  
  
Basic model info  
-----------------  
    Version: Sql110  
  Collation: SQL_Latin1_General_CP1_CI_AS  
  
UserDefinedElements  
-----------------  
  DatabaseOptions: 1  
         subtotal: 1  
      total items: 1  
  
OtherElements  
-----------------  
                Assembly: 1  
       BuiltInServerRole: 9  
           ClrTypeMethod: 218  
  ClrTypeMethodParameter: 197  
         ClrTypeProperty: 20  
                Contract: 6  
                DataType: 34  
                Endpoint: 5  
               Filegroup: 1  
             MessageType: 14  
                   Queue: 3  
                    Role: 10  
                  Schema: 13  
                 Service: 3  
                    User: 4  
         UserDefinedType: 3  
                subtotal: 541  
             total items: 16  
  
Relationships  
-----------------  
     Composing: 477  
  Hierarchical: 6  
          Peer: 19  
      subtotal: 502  
  
```  
  
1.  Abra ModelStatistics.xml e examine o conteúdo.  
  
    Os resultados que foram reportados também são persistidos no arquivo XML.  
  
## <a name="next-steps"></a>Next Steps  
Você pode criar ferramentas adicionais para executar o processamento do arquivo XML de saída. Isso é apenas um exemplo de um colaborador de compilação. Você pode, por exemplo, para criar um colaborador de compilação para gerar um arquivo de dicionário de dados como parte de sua compilação.  
  
## <a name="see-also"></a>Consulte Também  
[Personalizar a compilação e a implantação do banco de dados usando os colaboradores de compilação e implantação](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[Passo a passo: estender a implantação do projeto de banco de dados para analisar o plano de implantação](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
