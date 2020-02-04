---
title: Estender a implantação do projeto de banco de dados para analisar o plano de implantação
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9ead8470-93ba-44e3-8848-b59322e37621
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 5e51dddb7635ba0f50dfdd7566722b170be9f48a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75242679"
---
# <a name="walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan"></a>Passo a passo: estenda a implantação do projeto de banco de dados para analisar o plano de implantação

Você pode criar colaboradores de implantação para executar ações personalizadas ao implantar um projeto SQL. Você pode criar um DeploymentPlanModifier ou um DeploymentPlanExecutor. Use um DeploymentPlanModifier para alterar o plano antes de ser executado e um DeploymentPlanExecutor para realizar operações enquanto o plano está sendo executado. Neste passo a passo, você cria um DeploymentPlanExecutor chamado DeploymentUpdateReportContributor que cria um relatório das ações executadas quando você implanta um projeto de banco de dados. Como esse colaborador de compilação aceita um parâmetro para controlar se o relatório é gerado, você deverá executar uma etapa necessária adicional.  
  
Neste passo a passo, você realizará as tarefas principais a seguir:  
  
-   [Criar o tipo DeploymentPlanExecutor do colaborador de implantação](#CreateDeploymentContributor)  
  
-   [Instalar o colaborador de implantação](#InstallDeploymentContributor)  
  
-   [Testar seu colaborador de implantação](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
Você precisará dos seguintes componentes para concluir este passo a passo:  
  
-   Você deverá ter instalada uma versão do Visual Studio que inclui o SSDT (SQL Server Data Tools) e dá suporte ao desenvolvimento em C# ou VB.  
  
-   Você deve ter um projeto SQL que contenha objetos de SQL.  
  
-   Uma instância do SQL Server ao qual você poderá implantar um projeto de banco de dados.  
  
> [!NOTE]  
> Este passo a passo é destinado a usuários que já estão familiarizados com os recursos do SQL do SSDT. Você também já deverá estar familiarizado com os conceitos básicos do Visual Studio, por exemplo, como criar uma biblioteca de classe e como usar o editor de código para adicionar código a uma classe.  
  
## <a name="CreateDeploymentContributor"></a>Criar um colaborador de implantação  
Para criar um colaborador de implantação, você deverá realizar as seguintes tarefas:  
  
-   Criar um projeto de biblioteca de classe e adicionar as referências necessárias.  
  
-   Definir uma classe denominada DeploymentUpdateReportContributor que herda de [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx).  
  
-   Substitua o método OnExecute.  
  
-   Adicione uma classe auxiliar privada.  
  
-   Compile o assembly resultante.  
  
#### <a name="to-create-a-class-library-project"></a>Para criar um projeto de biblioteca de classe  
  
1.  Crie um projeto de biblioteca de classe do Visual Basic ou Visual C# denominado MyDeploymentContributor.  
  
2.  Renomeie o arquivo “Class1.cs” para “DeploymentUpdateReportContributor.cs”.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e, depois, clique em **Adicionar referência**.  
  
4.  Selecione **System.ComponentModel.Composition** na guia Estruturas.  
  
5.  Adicione as referências SQL necessárias: clique com o botão direito do mouse no nó do projeto e clique em **Adicionar Referência**. Clique em **Procurar** e navegue até a pasta **C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\DAC\Bin**. Escolha as entradas **Microsoft.SqlServer.Dac.dll**, **Microsoft.SqlServer.Dac.Extensions.dll** e **Microsoft.Data.Tools.Schema.Sql.dll**, clique em **Adicionar** e clique em **OK**.  
  
    Em seguida, comece a adicionar código à classe.  
  
#### <a name="to-define-the-deploymentupdatereportcontributor-class"></a>Par definir a classe DeploymentUpdateReportContributor  
  
1.  No editor de código, atualize o arquivo DeploymentUpdateReportContributor.cs para corresponder às instruções **using** a seguir:  
  
    ```csharp  
    using System;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Extensibility;  
    using Microsoft.SqlServer.Dac.Model;  
  
    ```  
  
2.  Atualize a definição de classe para corresponder ao seguinte:  
  
    ```csharp  
    /// <summary>  
        /// An executor that generates a report detailing the steps in the deployment plan. Will only run  
        /// if a "GenerateUpdateReport=true" contributor argument is set in the project file, in a targets file or  
        /// passed as an additional argument to the DacServices API. To set in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;  
        ///     </ContributorArguments>  
        /// <PropertyGroup>  
        ///   
        /// </summary>  
        [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
        public class DeploymentUpdateReportContributor : DeploymentPlanExecutor  
        {  
        }  
  
    ```  
  
    Agora você definiu o colaborador de implantação que herda de DeploymentPlanExecutor. Durante os processos de compilação e implantação, os colaboradores personalizados são carregados de um diretório de extensão padrão. Os colaboradores do executor do plano de implantação são identificados por um atributo [ExportDeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanexecutorattribute.aspx).  
  
    Esse atributo é necessário para que os colaboradores possam ser descobertos. Ela deve parecer com o seguinte:  
  
    ```csharp  
    [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
  
    ```  
  
    Nesse caso, o primeiro parâmetro para o atributo deve ser um identificador exclusivo – isso será usado para identificar seu colaborador em arquivos de projeto. Uma melhor prática é combinar o namespace da biblioteca (neste passo a passo, MyDeploymentContributor) com o nome de classe (neste passo a passo, DeploymentUpdateReportContributor) para produzir o identificador.  
  
3.  Em seguida, adicione o seguinte membro que você usará para habilitar esse provedor para aceitar um parâmetro de linha de comando:  
  
    ```csharp  
    public const string GenerateUpdateReport = "DeploymentUpdateReportContributor.GenerateUpdateReport";  
    ```  
  
    Esse membro permite que o usuário especifique se o relatório deve ser gerado usando a opção GenerateUpdateReport.  
  
    Em seguida, substitua o método OnExecute para adicionar o código que você quer executar quando um projeto de banco de dados é implantado.  
  
#### <a name="to-override-onexecute"></a>Para substituir OnExecute  
  
-   Adicione o seguinte método para sua classe DeploymentUpdateReportContributor:  
  
    ```csharp  
    /// <summary>  
            /// Override the OnExecute method to perform actions when you execute the deployment plan for  
            /// a database project.  
            /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                ExtensibilityError reportMsg = new ExtensibilityError(msg, Severity.Message);  
                base.PublishMessage(reportMsg);  
            }  
        /// <summary>  
        /// Override the OnExecute method to perform actions when you execute the deployment plan for  
        /// a database project.  
        /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                DataSchemaError reportMsg = new DataSchemaError(msg, ErrorSeverity.Message);  
                base.PublishMessage(reportMsg);  
            }  
    ```  
  
    No método OnExecute é passado um objeto [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) que fornece acesso a todos os argumentos especificados, o modelo de banco de dados de origem e destino, as propriedades de compilação e os arquivos de extensão. Neste exemplo, recebemos o modelo e chamamos as funções auxiliares para gerar informações sobre o modelo. Usamos o método auxiliar PublishMessage na classe base para relatar todos os erros que ocorrem.  
  
    Os tipos e métodos adicionais de interesse incluem: [TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx), [ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx), [DeploymentPlanHandle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanhandle.aspx) e [SqlDeploymentOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqldeploymentoptions.aspx).  
  
    Em seguida, você define a classe auxiliar que obtém mais detalhes do plano de implantação.  
  
#### <a name="to-add-the-helper-class-that-generates-the-report-body"></a>Para adicionar a classe auxiliar que gera o corpo do relatório  
  
-   Adicione a classe auxiliar e seus métodos adicionando o seguinte código:  
  
    ```csharp  
    /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                readonly TSqlModel _sourceModel;  
                readonly ModelComparisonResult _diff;  
                readonly DeploymentStep _planHead;  
  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
                    if (context == null)  
                    {  
                        throw new ArgumentNullException("context");  
                    }  
  
                    // save the source model, source/target differences,  
                    // and the beginning of the deployment plan.  
                    _sourceModel = context.Source;  
                    _diff = context.ComparisonResult;  
                    _planHead = context.PlanHandle.Head;  
                }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {// Assumes that we have a valid report file  
                    if (reportFile == null)  
                    {  
                        throw new ArgumentNullException("reportFile");  
                    }  
  
                    // set up the XML writer  
                    XmlWriterSettings xmlws = new XmlWriterSettings();  
                    // Indentation makes it a bit more readable  
                    xmlws.Indent = true;  
                    FileStream fs = new FileStream(reportFile.FullName, FileMode.Create, FileAccess.Write, FileShare.ReadWrite);  
                    XmlWriter xmlw = XmlWriter.Create(fs, xmlws);  
  
                    try  
                    {  
                        xmlw.WriteStartDocument(true);  
                        xmlw.WriteStartElement("DeploymentReport");  
  
                        // Summary report of the operations that  
                        // are contained in the plan.  
                        ReportPlanOperations(xmlw);  
  
                        // You could add a method call here  
                        // to produce a detailed listing of the   
                        // differences between the source and  
                        // target model.  
                        xmlw.WriteEndElement();  
                        xmlw.WriteEndDocument();  
                        xmlw.Flush();  
                        fs.Flush();  
                    }  
                    finally  
                    {  
                        xmlw.Close();  
                        fs.Dispose();  
                    }  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {// write the node to indicate the start  
                    // of the list of operations.  
                    xmlw.WriteStartElement("Operations");  
  
                    // Loop through the steps in the plan,  
                    // starting at the beginning.  
                    DeploymentStep currentStep = _planHead;  
                    while (currentStep != null)  
                    {  
                        // Report the type of step  
                        xmlw.WriteStartElement(currentStep.GetType().Name);  
  
                        // based on the type of step, report  
                        // the relevant information.  
                        // Note that this procedure only handles   
                        // a subset of all step types.  
                        if (currentStep is SqlRenameStep)  
                        {  
                            SqlRenameStep renameStep = (SqlRenameStep)currentStep;  
                            xmlw.WriteAttributeString("OriginalName", renameStep.OldName);  
                            xmlw.WriteAttributeString("NewName", renameStep.NewName);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(renameStep.RenamedElement));  
                        }  
                        else if (currentStep is SqlMoveSchemaStep)  
                        {  
                            SqlMoveSchemaStep moveStep = (SqlMoveSchemaStep)currentStep;  
                            xmlw.WriteAttributeString("OrignalName", moveStep.PreviousName);  
                            xmlw.WriteAttributeString("NewSchema", moveStep.NewSchema);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(moveStep.MovedElement));  
                        }  
                        else if (currentStep is SqlTableMigrationStep)  
                        {  
                            SqlTableMigrationStep dmStep = (SqlTableMigrationStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dmStep.SourceTable));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dmStep.SourceElement));  
                        }  
                        else if (currentStep is CreateElementStep)  
                        {  
                            CreateElementStep createStep = (CreateElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(createStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(createStep.SourceElement));  
                        }  
                        else if (currentStep is AlterElementStep)  
                        {  
                            AlterElementStep alterStep = (AlterElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(alterStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(alterStep.SourceElement));  
                        }  
                        else if (currentStep is DropElementStep)  
                        {  
                            DropElementStep dropStep = (DropElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dropStep.TargetElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dropStep.TargetElement));  
                        }  
  
                        // If the script bodies are to be included,  
                        // add them to the report.  
                        if (this.IncludeScripts)  
                        {  
                            using (StringWriter sw = new StringWriter())  
                            {  
                                currentStep.GenerateBatchScript(sw);  
                                string tsqlBody = sw.ToString();  
                                if (string.IsNullOrEmpty(tsqlBody) == false)  
                                {  
                                    xmlw.WriteCData(tsqlBody);  
                                }  
                            }  
                        }  
  
                        // close off the current step  
                        xmlw.WriteEndElement();  
                        currentStep = currentStep.Next;  
                    }  
                    xmlw.WriteEndElement();  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(TSqlObject element)  
                {  
                    return element.ObjectType.Name;  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private static string GetElementName(TSqlObject element)  
                {  
                    StringBuilder name = new StringBuilder();  
                    if (element.Name.HasExternalParts)  
                    {  
                        foreach (string part in element.Name.ExternalParts)  
                        {  
                            if (name.Length > 0)  
                            {  
                                name.Append('.');  
                            }  
                            name.AppendFormat("[{0}]", part);  
                        }  
                    }  
  
                    foreach (string part in element.Name.Parts)  
                    {  
                        if (name.Length > 0)  
                        {  
                            name.Append('.');  
                        }  
                        name.AppendFormat("[{0}]", part);  
                    }  
  
                    return name.ToString();  
                }  
            }        /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
               }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(IModelElement element)  
                {  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementName(IModelElement element)  
                {  
                }  
            }  
    ```  
  
-   Salve as alterações no arquivo de classe. Um número de tipos úteis são referenciados na classe auxiliar:  
  
    |**Área de código**|**Tipos úteis**|  
    |-----------------|--------------------|  
    |Membros de classe|[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx), [ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx), [DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx)|  
    |Método WriteReport|XmlWriter e XmlWriterSettings|  
    |Método ReportPlanOperations|Os tipos de interesse incluem o seguinte: [DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx), [SqlRenameStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlrenamestep.aspx), [SqlMoveSchemaStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlmoveschemastep.aspx), [SqlTableMigrationStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqltablemigrationstep.aspx), [CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx), [AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx), [DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx).<br /><br />Há várias outras etapas – consulte a documentação da API para obter uma lista completa de etapas.|  
    |GetElementCategory|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
    |GetElementName|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
  
    Em seguida, crie a biblioteca de classe.  
  
#### <a name="to-sign-and-build-the-assembly"></a>Para assinar e criar o assembly  
  
1.  No menu **Projeto**, clique em **Propriedades MyDeploymentContributor**.  
  
2.  Clique na guia **Assinatura** .  
  
3.  Clique em **Assinar o assembly**.  
  
4.  Em **Escolher um arquivo de chave de nome forte**, clique em **<New>** .  
  
5.  Na caixa de diálogo **Criar Chave de Nome Forte** , em **Nome de arquivo de chave**, digite **MyRefKey**.  
  
6.  (opcional) Você pode especificar uma senha para o arquivo de chave de nome forte.  
  
7.  Clique em **OK**.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
9. No menu **Compilar**, clique em **Compilar Solução**.  
  
Em seguida, você deve instalar o assembly de modo que ele seja carregado quando você compilar e implantar projetos do SQL.  
  
## <a name="InstallDeploymentContributor"></a>Instalar um colaborador de implantação  
Para instalar um colaborador de implantação, você deverá copiar o assembly e o arquivo .pdb associado à pasta Extensões.  
  
#### <a name="to-install-the-mydeploymentcontributor-assembly"></a>Para instalar o assembly MyDeploymentContributor  
  
-   Em seguida, você copiará as informações de assembly para o diretório Extensões. Quando o Visual Studio iniciar, ele identificará as extensões no diretório e subdiretórios %Arquivos de Programas%\Microsoft SQL Server\110\DAC\Bin\Extensions e as tornará disponíveis para uso:  
  
-   Copie o arquivo de assembly **MyDeploymentContributor.dll** do diretório de saída para o diretório %Arquivos de Programas%Microsoft SQL Server\110\DAC\Bin\Extensions. Por padrão, o caminho do seu arquivo compilado .dll é YourSolutionPath\YourProjectPath\bin\Debug ou YourSolutionPath\YourProjectPath\bin\Release.  
  
## <a name="TestDeploymentContributor"></a>Testar seu colaborador de implantação  
Para testar seu colaborador de implantação, você deverá realizar as seguintes tarefas:  
  
-   Adicionar propriedades ao arquivo .sqlproj que você planeja implantar.  
  
-   Implantar o projeto usando MSBuild e fornecendo o parâmetro apropriado.  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>Adicionar Propriedades ao arquivo de projeto SQL (.sqlproj)  
Você sempre deve atualizar o arquivo de projeto SQL para especificar a ID dos colaboradores que você deseja executar. Além disso, como esse colaborador espera um argumento “GenerateUpdateReport”, isso deve ser especificado como um argumento de colaborador.  
  
É possível fazer isso de duas formas. Você pode modificar manualmente o arquivo .sqlproj para adicionar os argumentos necessários. Você pode escolher fazer isso se seu colaborador não tiver nenhum argumento de colaborador necessário para configuração ou se você não quiser reutilizar o colaborador em um número grande de projetos. Se você escolher esta opção, adicione as seguintes instruções ao arquivo .sqlproj após o primeiro nó de importação no arquivo:  
  
```  
<PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors); MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
<ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
  </PropertyGroup>  
```  
  
O segundo método é criar um arquivo de destino que contém argumentos necessários de colaborador. Isso será útil se você estiver usando o mesmo colaborador para vários projetos e tiver argumentos de colaborador necessários, porque isso incluirá os valores padrão. Nesse caso, crie um arquivo de destino no caminho de extensões do MSBuild.  
  
1.  Navegue para %Arquivos de programas%\MSBuild.  
  
2.  Crie uma nova pasta "MyContributors" na qual os arquivos de destino serão armazenados.  
  
3.  Crie um novo arquivo "MyContributors.targets" dentro desse diretório, adicione o seguinte texto e salve o arquivo:  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
  
    <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors);MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
    <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments); DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
      </PropertyGroup>  
    </Project>  
    ```  
  
4.  Dentro do arquivo .sqlproj para qualquer projeto que você quiser executar colaboradores, importe o arquivo de destino adicionando a seguinte instrução ao arquivo .sqlproj após o nó \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> no arquivo:  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
    ```  
  
Depois que você tiver seguido uma destas abordagens, poderá usar MSBuild para passar parâmetros para compilações de linha de comando.  
  
> [!NOTE]  
> Você sempre deve atualizar a propriedade “DeploymentContributors” para especificar sua ID de colaborador. Esta é a mesma ID usada no atributo “ExportDeploymentPlanExecutor” no seu arquivo de origem de colaborador. Sem isso, seu colaborador não será executado ao criar o projeto. A propriedade "ContributorArguments" precisará ser atualizada somente se você tiver os argumentos necessários para seu colaborador ser executado.  
  
### <a name="deploy-the-database-project"></a>Implantar o projeto de banco de dados  
Seu projeto pode ser publicado ou implantado normalmente dentro do Visual Studio. Basta abrir uma solução contendo seu projeto SQL e escolher a opção “Publicar...” no menu de contexto do projeto aberto ao clicar com o botão direito do mouse ou usar F5 para uma implantação de depuração para o LocalDB. Neste exemplo, usaremos a caixa de diálogo "Publicar…" para gerar um script de implantação.  
  
##### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>Para implantar o projeto SQL e gerar um relatório de implantação  
  
1.  Abra o Visual Studio e abra a solução que contém o seu projeto SQL.  
  
2.  Selecione seu projeto e pressione “F5” para fazer uma implantação de depuração. Observação: como o elemento ContributorArguments é definido apenas para ser incluído se a configuração for “Depurar”, por enquanto, o relatório de implantação é gerado apenas para implantações de depuração. Para alterar isso, remova a instrução Condition="'$(Configuration)' == 'Debug'" da definição ContributorArguments.  
  
3.  A saída como a seguinte deve estar presente na janela de saída:  
  
    ```  
    ------ Deploy started: Project: Database1, Configuration: Debug Any CPU ------  
    Finished verifying cached model in 00:00:00  
    Deployment reports ->  
  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.summary.xml  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.details.xml  
  
      Deployment script generated to:  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyDatabaseProject.sql  
  
    ```  
  
4.  Abra MyTargetDatabase.summary.xml e examine o conteúdo. O arquivo é semelhante ao exemplo seguinte que mostra uma nova implantação de banco de dados:  
  
    ```  
    <?xml version="1.0" encoding="utf-8" standalone="yes"?>  
    <DeploymentReport>  
      <Operations>  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <BeginPreDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPreDeploymentScriptStep />  
        <SqlBeginPreservationStep />  
        <SqlEndPreservationStep />  
        <SqlBeginDropsStep />  
        <SqlEndDropsStep />  
        <SqlBeginAltersStep />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales" Category="Schema" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Customer" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Customer_CustID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Orders" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Orders_OrderID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDOrders" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDSales" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_OrderDate" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_Status" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.FK_Orders_Customer_CustID" Category="Foreign Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_FilledDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_OrderDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspCancelOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspFillOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspNewCustomer" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspPlaceNewOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspShowOrderDetails" Category="Procedure" />  
        <SqlEndAltersStep />  
        <DeploymentScriptStep />  
        <BeginPostDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPostDeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
      </Operations>  
    </DeploymentReport>  
  
    ```  
  
    > [!NOTE]  
    > Se você implantar um projeto de banco de dados que seja idêntico ao banco de dados de destino, o relatório resultante não será muito significativo. Para obter mais resultados significativos, implante as alterações em um banco de dados ou implante um novo banco de dados.  
  
5.  Abra MyTargetDatabase.details.xml e examine o conteúdo. Uma pequena seção do arquivo de detalhes mostra as entradas e o script que cria o esquema de vendas, que imprime uma mensagem sobre a criação de uma tabela e que cria a tabela:  
  
    ```  
    <CreateElementStep Name="Sales" Category="Schema"><![CDATA[CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
  
    ]]></CreateElementStep>  
        <SqlPrintStep><![CDATA[PRINT N'Creating [Sales].[Customer]...';  
  
    ]]></SqlPrintStep>  
        <CreateElementStep Name="Sales.Customer" Category="Table"><![CDATA[CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
  
    ]]></CreateElementStep>  
  
    ```  
  
    Ao analisar o plano de implantação como ele é executado, você poderá relatar todas as informações que estão contidas na implantação e poderá realizar as ações adicionais com base nas etapas desse plano.  
  
## <a name="next-steps"></a>Próximas etapas  
Você pode criar ferramentas adicionais para executar o processamento dos arquivos XML de saída. Isso é apenas um exemplo de um [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx). Você também pode criar um [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) para modificar um plano de implantação antes de ser executado.  
  
## <a name="see-also"></a>Consulte Também  
[Passo a passo: estender a compilação do projeto de banco de dados para gerar as estatísticas do modelo](https://msdn.microsoft.com/library/ee461508(v=vs.100).aspx)  
[Passo a passo: estender a implantação do projeto de banco de dados para modificar o plano de implantação](https://msdn.microsoft.com/library/ee461507(v=vs.100).aspx)  
[Personalizar a compilação e a implantação do banco de dados usando os colaboradores de compilação e implantação](https://msdn.microsoft.com/library/ee461505(v=vs.100).aspx)  
  
