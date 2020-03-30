---
title: Estender a implantação do projeto de banco de dados para modificar o plano de implantação
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 22b077b1-fa25-49ff-94f6-6d0d196d870a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 1f4c73d02d131a0399fd8dde7698592629ef2726
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242671"
---
# <a name="walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan"></a>Passo a passo: estenda a implantação do projeto de banco de dados para modificar o plano de implantação

Você pode criar colaboradores de implantação para executar ações personalizadas ao implantar um projeto SQL. Você pode criar um [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) ou um [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx). Use um [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) para alterar o plano antes de ser executado e um [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) para realizar operações enquanto o plano está sendo executado. Nesse passo a passo, você cria um [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) chamado SqlRestartableScriptContributor que adiciona instruções IF aos lotes no script de implantação para habilitar o script para ser executado novamente até que seja concluído se um erro ocorrer durante a execução.  
  
Neste passo a passo, você realizará as tarefas principais a seguir:  
  
-   [Criar o tipo DeploymentPlanModifier do colaborador de implantação](#CreateDeploymentContributor)  
  
-   [Instalar o colaborador de implantação](#InstallDeploymentContributor)  
  
-   [Executar ou testar seu Colaborador de Implantação](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
Você precisará dos seguintes componentes para concluir este passo a passo:  
  
-   Você deverá ter instalada uma versão do Visual Studio que inclui o SQL Server Data Tools e dá suporte ao desenvolvimento em C# ou VB.  
  
-   Você deve ter um projeto SQL que contenha objetos de SQL.  
  
-   Uma instância do SQL Server ao qual você poderá implantar um projeto de banco de dados.  
  
> [!NOTE]  
> Este passo a passo é destinado a usuários que já estão familiarizados com os recursos do SQL Server Data Tools. Você também já deverá estar familiarizado com os conceitos básicos do Visual Studio, por exemplo, como criar uma biblioteca de classe e como usar o editor de código para adicionar código a uma classe.  
  
## <a name="create-a-deployment-contributor"></a><a name="CreateDeploymentContributor"></a>Criar um colaborador de implantação  
Para criar um colaborador de implantação, você deverá realizar as seguintes tarefas:  
  
-   Criar um projeto de biblioteca de classe e adicionar as referências necessárias.  
  
-   Definir uma classe denominada SqlRestartableScriptContributor que herda de [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx).  
  
-   Substitua o método [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx).  
  
-   Adicionar métodos auxiliares privados.  
  
-   Compile o assembly resultante.  
  
#### <a name="to-create-a-class-library-project"></a>Para criar um projeto de biblioteca de classe  
  
1.  Crie um projeto de biblioteca de classe do Visual C# ou Visual Basic chamado MyOtherDeploymentContributor.  
  
2.  Renomeie o arquivo "Class1.cs" para "SqlRestartableScriptContributor.cs".  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e, depois, clique em **Adicionar referência**.  
  
4.  Selecione **System.ComponentModel.Composition** na guia Estruturas.  
  
5.  Clique em **Procurar** e navegue até o diretório **C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\SDK\Assemblies**, selecione **Microsoft.SqlServer.TransactSql.ScriptDom.dll** e clique em **OK**.  
  
6.  Adicione as referências SQL necessárias: clique com o botão direito do mouse no nó do projeto e clique em **Adicionar Referência**. Clique em **Procurar** e navegue até a pasta **C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\DAC\Bin**. Escolha as entradas **Microsoft.SqlServer.Dac.dll**, **Microsoft.SqlServer.Dac.Extensions.dll** e **Microsoft.Data.Tools.Schema.Sql.dll**, clique em **Adicionar** e em **OK**.  
  
Em seguida, comece a adicionar código à classe.  
  
#### <a name="to-define-the-sqlrestartablescriptcontributor-class"></a>Para definir a classe SqlRestartableScriptContributor  
  
1.  No editor de código, atualize o arquivo class1.cs para corresponder às seguintes instruções **using**:  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;  
    using System.Text;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    ```  
  
2.  Atualize a definição de classe para corresponder ao exemplo a seguir:  
  
    ```csharp  
        /// <summary>  
    /// This deployment contributor modifies a deployment plan by adding if statements  
    /// to the existing batches in order to make a deployment script able to be rerun to completion  
    /// if an error is encountered during execution  
    /// </summary>  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
    public class SqlRestartableScriptContributor : DeploymentPlanModifier  
    {  
    }  
  
    ```  
  
    Agora você definiu o colaborador de implantação que herda de [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx). Durante os processos de compilação e implantação, os colaboradores personalizados são carregados de um diretório de extensão padrão. Os colaboradores de modificação de plano de implantação são identificados por um atributo [ExportDeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanmodifierattribute.aspx). Esse atributo é necessário para que os colaboradores possam ser descobertos. Esse atributo deve ser semelhante ao seguinte:  
  
    ```csharp  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
  
    ```  
  
3.  Adicione as seguintes declarações de membro:  
  
    ```vb  
         private const string BatchIdColumnName = "BatchId";  
            private const string DescriptionColumnName = "Description";  
  
            private const string CompletedBatchesVariableName = "CompletedBatches";  
            private const string CompletedBatchesVariable = "$(CompletedBatches)";  
            private const string CompletedBatchesSqlCmd = @":setvar " + CompletedBatchesVariableName + " __completedBatches_{0}_{1}";  
            private const string TotalBatchCountSqlCmd = @":setvar TotalBatchCount {0}";  
            private const string CreateCompletedBatchesTable = @"  
    if OBJECT_ID(N'tempdb.dbo." + CompletedBatchesVariable + @"', N'U') is null  
    begin  
    use tempdb  
    create table [dbo].[$(CompletedBatches)]  
    (  
    BatchId int primary key,  
    Description nvarchar(300)  
    )  
    use [$(DatabaseName)]  
    end  
    ";  
  
    ```  
  
    Em seguida, substitua o método OnExecute para adicionar o código que você quer executar quando um projeto de banco de dados é implantado.  
  
#### <a name="to-override-onexecute"></a>Para substituir OnExecute  
  
1.  Adicione o seguinte método à sua classe SqlRestartableScriptContributor:  
  
    ```csharp  
    /// <summary>  
    /// You override the OnExecute method to do the real work of the contributor.  
    /// </summary>  
    /// <param name="context"></param>  
    protected override void OnExecute(DeploymentPlanContributorContext context)  
    {  
         // Replace this with the method body  
    }  
  
    ```  
  
    Substitua o método [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) da classe base, [DeploymentPlanContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.aspx), que é a classe base para [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) e [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx). O método OnExecute passou um objeto [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) que fornece acesso a qualquer argumento especificado, o modelo de banco de dados de origem e destino, o plano de implantação e as opções de implantação. Neste exemplo, obtemos o plano de implantação e o nome do banco de dados de destino.  
  
2.  Agora adicione os inícios de um corpo ao método OnExecute:  
  
    ```vb  
    // Obtain the first step in the Plan from the provided context  
    DeploymentStep nextStep = context.PlanHandle.Head;  
    int batchId = 0;  
    BeginPreDeploymentScriptStep beforePreDeploy = null;  
  
    // Loop through all steps in the deployment plan  
    while (nextStep != null)  
    {  
        // Increment the step pointer, saving both the current and next steps  
        DeploymentStep currentStep = nextStep;  
        nextStep = currentStep.Next;  
  
        // Add additional step processing here  
    }  
  
    // if we found steps that required processing, set up a temporary table to track the work that you are doing  
    if (beforePreDeploy != null)  
    {  
        // Add additional post-processing here  
    }  
  
    // Cleanup and drop the table   
    DeploymentScriptStep dropStep = new DeploymentScriptStep(DropCompletedBatchesTable);  
    base.AddAfter(context.PlanHandle, context.PlanHandle.Tail, dropStep);  
  
    ```  
  
    Nesse código, definimos algumas variáveis locais e configuramos o loop que tratará o processamento de todas as etapas no plano de implantação. Depois que o loop estiver concluído, teremos que fazer um pós-processamento e, em seguida, descartaremos a tabela temporária que criamos durante a implantação para rastrear o andamento à medida que o plano é executado. Os principais tipos aqui são: [DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx) e [DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx). Um método importante é o AddAfter.  
  
3.  Agora adicione o processamento de etapa adicional para substituir o comentário "Adicione o processamento de etapa adicional aqui":  
  
    ```csharp  
    // Look for steps that mark the pre/post deployment scripts  
    // These steps will always be in the deployment plan even if the  
    // user's project does not have a pre/post deployment script  
    if (currentStep is BeginPreDeploymentScriptStep)  
    {  
        // This step marks the beginning of the predeployment script.  
        // Save the step and move on.  
        beforePreDeploy = (BeginPreDeploymentScriptStep)currentStep;  
        continue;  
    }  
    if (currentStep is BeginPostDeploymentScriptStep)  
    {  
        // This is the step that marks the beginning of the post deployment script.    
        // We do not continue processing after this point.  
        break;  
    }  
    if (currentStep is SqlPrintStep)  
    {  
        // We do not need to put if statements around these  
        continue;  
    }  
  
    // if we have not yet found the beginning of the pre-deployment script steps,   
    // skip to the next step.  
    if (beforePreDeploy == null)  
    {  
        // We only surround the "main" statement block with conditional  
        // statements  
        continue;  
    }  
  
    // Determine if this is a step that we need to surround with a conditional statement  
    DeploymentScriptDomStep domStep = currentStep as DeploymentScriptDomStep;  
    if (domStep == null)  
    {  
        // This step is not a step that we know how to modify,  
        // so skip to the next step.  
        continue;  
    }  
  
    TSqlScript script = domStep.Script as TSqlScript;  
    if (script == null)  
    {  
        // The script dom step does not have a script with batches - skip  
        continue;  
    }  
  
        // Loop through all the batches in the script for this step.  All the statements  
        // in the batch will be enclosed in an if statement that will check the  
        // table to ensure that the batch has not already been executed  
        TSqlObject sqlObject;  
        string stepDescription;  
        GetStepInfo(domStep, out stepDescription, out sqlObject);  
        int batchCount = script.Batches.Count;  
  
    for (int batchIndex = 0; batchIndex < batchCount; batchIndex++)  
    {  
        // Add batch processing here  
    }  
  
    ```  
  
    Os comentários do código explicam o processamento. Em um nível superior, esse código procura as etapas que você desejar, ignorando outras e parando quando você atingir o início das etapas de pós-implantação. Se a etapa contiver instruções que devemos cercar com condicionais, realizaremos processamento adicional. Entre os principais tipos, métodos e propriedades estão: [BeginPreDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpredeploymentscriptstep.aspx), [BeginPostDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpostdeploymentscriptstep.aspx), [TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx), [TSqlScript](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlscript.aspx), Script, [DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx) e [SqlPrintStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlprintstep.aspx).  
  
4.  Agora adicione o código de processamento em lote substituindo o comentário "Adicione o processamento em lote aqui":  
  
    ```csharp  
        // Create the if statement that will contain the batch's contents  
        IfStatement ifBatchNotExecutedStatement = CreateIfNotExecutedStatement(batchId);  
        BeginEndBlockStatement statementBlock = new BeginEndBlockStatement();  
        ifBatchNotExecutedStatement.ThenStatement = statementBlock;  
        statementBlock.StatementList = new StatementList();  
  
        TSqlBatch batch = script.Batches[batchIndex];  
        int statementCount = batch.Statements.Count;  
  
        // Loop through all statements in the batch, embedding those in an sp_execsql  
        // statement that must be handled this way (schemas, stored procedures,   
        // views, functions, and triggers).  
        for (int statementIndex = 0; statementIndex < statementCount; statementIndex++)  
        {  
            // Add additional statement processing here  
        }  
  
        // Add an insert statement to track that all the statements in this  
        // batch were executed.  Turn on nocount to improve performance by  
        // avoiding row inserted messages from the server  
        string batchDescription = string.Format(CultureInfo.InvariantCulture,  
            "{0} batch {1}", stepDescription, batchIndex);  
  
        PredicateSetStatement noCountOff = new PredicateSetStatement();  
        noCountOff.IsOn = false;  
        noCountOff.Options = SetOptions.NoCount;  
  
        PredicateSetStatement noCountOn = new PredicateSetStatement();  
        noCountOn.IsOn = true;  
        noCountOn.Options = SetOptions.NoCount;   
        InsertStatement batchCompleteInsert = CreateBatchCompleteInsert(batchId, batchDescription);  
        statementBlock.StatementList.Statements.Add(noCountOn);  
    statementBlock.StatementList.Statements.Add(batchCompleteInsert);  
        statementBlock.StatementList.Statements.Add(noCountOff);  
  
        // Remove all the statements from the batch (they are now in the if block) and add the if statement  
        // as the sole statement in the batch  
        batch.Statements.Clear();  
        batch.Statements.Add(ifBatchNotExecutedStatement);  
  
        // Next batch  
        batchId++;  
  
    ```  
  
    Esse código cria uma instrução IF junto com um bloco BEGIN/END. Em seguida, realizamos o processamento adicional nas instruções no lote. Assim que estiver concluído, adicionamos uma instrução INSERT para adicionar informações à tabela temporária que rastreia o progresso da execução do script. Finalmente, atualize o lote, substituindo as instruções que estavam lá com o novo IF que contém essas instruções dentro dela. Os principais tipos, métodos e propriedades incluem: [IfStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.ifstatement.aspx), [BeginEndBlockStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.beginendblockstatement.aspx), [StatementList](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.statementlist.aspx), [TSqlBatch](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlbatch.aspx), [PredicateSetStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.predicatesetstatement.aspx), [SetOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.setoptions.aspx) e [InsertStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.insertstatement.aspx).  
  
5.  Agora, adicione o corpo do loop de processamento da instrução. Substitua o comentário "Adicione o processamento de instrução adicional aqui":  
  
    ```csharp  
    TSqlStatement smnt = batch.Statements[statementIndex];  
  
    if (IsStatementEscaped(sqlObject))  
    {  
        // "escape" this statement by embedding it in a sp_executesql statement  
        string statementScript;  
        domStep.ScriptGenerator.GenerateScript(smnt, out statementScript);  
        ExecuteStatement spExecuteSql = CreateExecuteSql(statementScript);  
        smnt = spExecuteSql;  
    }  
  
    statementBlock.StatementList.Statements.Add(smnt);  
  
    ```  
  
    Para cada instrução no lote, se a instrução for de um tipo que deve ser encapsulado com uma instrução sp_executesql, modifique a instrução de acordo. O código em seguida adiciona a instrução à lista de instrução para o bloco BEGIN/END criado. Os principais tipos, métodos e propriedades incluem [TSqlStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlstatement.aspx) e [ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx).  
  
6.  Finalmente, adicione a seção de pós-processamento no lugar do comentário "Adicione o pós-processamento adicional aqui":  
  
    ```csharp  
    // Declare a SqlCmd variables.  
    //  
    // CompletedBatches variable - defines the name of the table in tempdb that will track  
    // all the completed batches.  The temporary table's name has the target database name and  
    // a guid embedded in it so that:  
    // * Multiple deployment scripts targeting different DBs on the same server  
    // * Failed deployments with old tables do not conflict with more recent deployments  
    //  
    // TotalBatchCount variable - the total number of batches surrounded by if statements.  Using this  
    // variable pre/post deployment scripts can also use the CompletedBatches table to make their  
    // script rerunnable if there is an error during execution  
    StringBuilder sqlcmdVars = new StringBuilder();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, CompletedBatchesSqlCmd,  
        context.Options.TargetDatabaseName, Guid.NewGuid().ToString("D"));  
    sqlcmdVars.AppendLine();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, TotalBatchCountSqlCmd, batchId);  
  
    DeploymentScriptStep completedBatchesSetVarStep = new DeploymentScriptStep(sqlcmdVars.ToString());  
    base.AddBefore(context.PlanHandle, beforePreDeploy, completedBatchesSetVarStep);  
  
    // Create the temporary table we will use to track the work that we are doing  
    DeploymentScriptStep createStatusTableStep = new DeploymentScriptStep(CreateCompletedBatchesTable);  
    base.AddBefore(context.PlanHandle, beforePreDeploy, createStatusTableStep);  
  
    ```  
  
    Se nosso processamento tiver encontrado uma ou mais etapas que cercamos com uma instrução condicional, deveremos adicionar instruções ao script de implantação para definir as variáveis SQLCMD. A primeira variável, CompletedBatches, contém um nome exclusivo para a tabela temporária que o script de implantação usa para controlar quais lotes foram concluídos com sucesso quando o script foi executado. A segunda variável, TotalBatchCount, contém o número total de lotes no script de implantação.  
  
    Tipos, propriedades e métodos de interesse adicionais incluem:  
  
    StringBuilder, [DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx) e AddBefore.  
  
    Em seguida, você define os métodos auxiliares chamados por esse método.  
  
#### <a name="to-add-the-helper-methods"></a>Para adicionar os métodos auxiliares  
  
-   Vários métodos auxiliares devem ser definidos. Os métodos importantes incluem:  
  
    |**Método**|**Descrição**|  
    |--------------|-------------------|  
    |CreateExecuteSQL|Definir o método CreateExecuteSQL para cercar uma instrução fornecida com uma instrução EXEC sp_executesql. Os principais tipos, métodos e propriedades incluem o seguinte: [ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx), [ExecutableProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executableprocedurereference.aspx), [SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx), [ProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.procedurereference.aspx) e [ExecuteParameter](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executeparameter.aspx).|  
    |CreateCompletedBatchesName|Definir o método CreateCompletedBatchesName. Este método cria o nome que será inserido na tabela temporária para um lote. Os principais tipos, métodos e propriedades incluem o seguinte: [SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx).|  
    |IsStatementEscaped|Definir o método IsStatementEscaped. Este método determina se o tipo de elemento de modelo exige que a instrução seja encapsulada em uma instrução EXEC sp_executesql antes de ser incluída dentro de uma instrução IF. Tipos de chaves, métodos e propriedades incluem o seguinte: TSqlObject.ObjectType, ModelTypeClass e a propriedade TypeClass para os seguintes tipos de modelo: esquema, procedimento, exibição, TableValuedFunction, ScalarFunction, DatabaseDdlTrigger, DmlTrigger, ServerDdlTrigger.|  
    |CreateBatchCompleteInsert|Definir o método CreateBatchCompleteInsert. Este método cria a instrução INSERT que será adicionada ao script de implantação para rastrear o andamento da execução do script. Os principais tipos de chaves, métodos e propriedades incluem o seguinte: InsertStatement, NamedTableReference, ColumnReferenceExpression, ValuesInsertSource e RowValue.|  
    |CreateIfNotExecutedStatement|Definir o método CreateIfNotExecutedStatement. Esse método gera UMA instrução IF que verifica se os lotes temporários que executam a tabela indicam que esse lote já foi executado. Os principais tipos de chaves, métodos e propriedades incluem o seguinte: IfStatement, ExistsPredicate, ScalarSubquery, NamedTableReference, WhereClause, ColumnReferenceExpression, IntegerLiteral, BooleanComparisonExpression e BooleanNotExpression.|  
    |GetStepInfo|Definir o método GetStepInfo. Esse método extrai informações sobre o elemento de modelo usado para criar o script da etapa, além do nome da etapa. Os tipos e os métodos de interesse incluem o seguinte: [DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx), [DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx), [TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx), [CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx), [AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx) e [DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx).|  
    |GetElementName|Cria um nome formatado para um TSqlObject.|  
  
1.  Adicione o código a seguir para definir os métodos auxiliares:  
  
    ```csharp  
  
    /// <summary>  
    /// The CreateExecuteSql method "wraps" the provided statement script in an "sp_executesql" statement  
    /// Examples of statements that must be so wrapped include: stored procedures, views, and functions  
    /// </summary>  
    private static ExecuteStatement CreateExecuteSql(string statementScript)  
    {  
        // define a new Exec statement  
        ExecuteStatement executeSp = new ExecuteStatement();  
        ExecutableProcedureReference spExecute = new ExecutableProcedureReference();  
        executeSp.ExecuteSpecification = new ExecuteSpecification { ExecutableEntity = spExecute };  
  
        // define the name of the procedure that you want to execute, in this case sp_executesql  
        SchemaObjectName procName = new SchemaObjectName();  
        procName.Identifiers.Add(CreateIdentifier("sp_executesql", QuoteType.NotQuoted));  
        ProcedureReference procRef = new ProcedureReference { Name = procName };  
  
        spExecute.ProcedureReference = new ProcedureReferenceName { ProcedureReference = procRef };  
  
        // add the script parameter, constructed from the provided statement script  
        ExecuteParameter scriptParam = new ExecuteParameter();  
        spExecute.Parameters.Add(scriptParam);  
        scriptParam.ParameterValue = new StringLiteral { Value = statementScript };  
        scriptParam.Variable = new VariableReference { Name = "@stmt" };  
        return executeSp;  
    }  
  
    /// <summary>  
    /// The CreateIdentifier method returns a Identifier with the specified value and quoting type  
    /// </summary>  
    private static Identifier CreateIdentifier(string value, QuoteType quoteType)  
    {  
        return new Identifier { Value = value, QuoteType = quoteType };  
    }  
  
    /// <summary>  
    /// The CreateCompletedBatchesName method creates the name that will be inserted  
    /// into the temporary table for a batch.  
    /// </summary>  
    private static SchemaObjectName CreateCompletedBatchesName()  
    {  
        SchemaObjectName name = new SchemaObjectName();  
        name.Identifiers.Add(CreateIdentifier("tempdb", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier("dbo", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier(CompletedBatchesVariable, QuoteType.SquareBracket));  
        return name;  
    }  
  
    /// <summary>  
    /// Helper method that determins whether the specified statement needs to  
    /// be escaped  
    /// </summary>  
    /// <param name="sqlObject"></param>  
    /// <returns></returns>  
    private static bool IsStatementEscaped(TSqlObject sqlObject)  
    {  
        HashSet<ModelTypeClass> escapedTypes = new HashSet<ModelTypeClass>  
        {  
            Schema.TypeClass,  
            Procedure.TypeClass,  
            View.TypeClass,  
            TableValuedFunction.TypeClass,  
            ScalarFunction.TypeClass,  
            DatabaseDdlTrigger.TypeClass,  
            DmlTrigger.TypeClass,  
            ServerDdlTrigger.TypeClass  
        };  
        return escapedTypes.Contains(sqlObject.ObjectType);  
    }  
  
    /// <summary>  
    /// Helper method that creates an INSERT statement to track a batch being completed  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <param name="batchDescription"></param>  
    /// <returns></returns>  
    private static InsertStatement CreateBatchCompleteInsert(int batchId, string batchDescription)  
    {  
        InsertStatement insert = new InsertStatement();  
        NamedTableReference batchesCompleted = new NamedTableReference();  
        insert.InsertSpecification = new InsertSpecification();  
        insert.InsertSpecification.Target = batchesCompleted;  
        batchesCompleted.SchemaObject = CreateCompletedBatchesName();  
  
        // Build the columns inserted into  
        ColumnReferenceExpression batchIdColumn = new ColumnReferenceExpression();  
        batchIdColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        batchIdColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(BatchIdColumnName, QuoteType.NotQuoted));  
  
        ColumnReferenceExpression descriptionColumn = new ColumnReferenceExpression();  
        descriptionColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        descriptionColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(DescriptionColumnName, QuoteType.NotQuoted));  
  
        insert.InsertSpecification.Columns.Add(batchIdColumn);  
        insert.InsertSpecification.Columns.Add(descriptionColumn);  
  
        // Build the values inserted  
        ValuesInsertSource valueSource = new ValuesInsertSource();  
        insert.InsertSpecification.InsertSource = valueSource;  
  
        RowValue values = new RowValue();  
        values.ColumnValues.Add(new IntegerLiteral { Value = batchId.ToString() });  
        values.ColumnValues.Add(new StringLiteral { Value = batchDescription });  
        valueSource.RowValues.Add(values);  
  
        return insert;  
    }  
  
    /// <summary>  
    /// This is a helper method that generates an if statement that checks the batches executed  
    /// table to see if the current batch has been executed.  The if statement will look like this  
    ///   
    /// if not exists(select 1 from [tempdb].[dbo].[$(CompletedBatches)]   
    ///                where BatchId = batchId)  
    /// begin  
    /// end  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <returns></returns>  
    private static IfStatement CreateIfNotExecutedStatement(int batchId)  
    {  
        // Create the exists/select statement  
        ExistsPredicate existsExp = new ExistsPredicate();  
        ScalarSubquery subQuery = new ScalarSubquery();  
        existsExp.Subquery = subQuery;  
  
        subQuery.QueryExpression = new QuerySpecification  
        {  
            SelectElements =  
            {  
                new SelectScalarExpression  { Expression = new IntegerLiteral { Value ="1" } }  
            },  
            FromClause = new FromClause  
            {  
                TableReferences =  
                    {  
                        new NamedTableReference() { SchemaObject = CreateCompletedBatchesName() }  
                    }  
            },  
            WhereClause = new WhereClause  
            {  
                SearchCondition = new BooleanComparisonExpression  
                {  
                    ComparisonType = BooleanComparisonType.Equals,  
                    FirstExpression = new ColumnReferenceExpression  
                    {  
                        MultiPartIdentifier = new MultiPartIdentifier  
                        {  
                            Identifiers = { CreateIdentifier(BatchIdColumnName, QuoteType.SquareBracket) }  
                        }  
                    },  
                    SecondExpression = new IntegerLiteral { Value = batchId.ToString() }  
                }  
            }  
        };  
  
        // Put together the rest of the statement  
        IfStatement ifNotExists = new IfStatement  
        {  
            Predicate = new BooleanNotExpression  
            {  
                Expression = existsExp  
            }  
        };  
  
        return ifNotExists;  
    }  
  
    /// <summary>  
    /// Helper method that generates a useful description of the step.  
    /// </summary>  
    private static void GetStepInfo(  
        DeploymentScriptDomStep domStep,  
        out string stepDescription,  
        out TSqlObject element)  
    {  
        element = null;  
  
        // figure out what type of step we've got, and retrieve  
        // either the source or target element.  
        if (domStep is CreateElementStep)  
        {  
            element = ((CreateElementStep)domStep).SourceElement;  
        }  
        else if (domStep is AlterElementStep)  
        {  
            element = ((AlterElementStep)domStep).SourceElement;  
        }  
        else if (domStep is DropElementStep)  
        {  
            element = ((DropElementStep)domStep).TargetElement;  
        }  
  
        // construct the step description by concatenating the type and the fully qualified  
        // name of the associated element.  
        string stepTypeName = domStep.GetType().Name;  
        if (element != null)  
        {  
            string elementName = GetElementName(element);  
  
            stepDescription = string.Format(CultureInfo.InvariantCulture, "{0} {1}",  
                stepTypeName, elementName);  
        }  
        else  
        {  
            // if the step has no associated element, just use the step type as the description  
            stepDescription = stepTypeName;  
        }  
    }  
  
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
  
    ```  
  
2.  Salve as alterações para SqlRestartableScriptContributor.cs.  
  
Em seguida, crie a biblioteca de classe.  
  
#### <a name="to-sign-and-build-the-assembly"></a>Para assinar e criar o assembly  
  
1.  No menu **Projeto**, clique em **Propriedades MyOtherDeploymentContributor**.  
  
2.  Clique na guia **Assinatura** .  
  
3.  Clique em **Assinar o assembly**.  
  
4.  Em **Escolher um arquivo de chave de nome forte**, clique em **<New>** .  
  
5.  Na caixa de diálogo **Criar Chave de Nome Forte** , em **Nome de arquivo de chave**, digite **MyRefKey**.  
  
6.  (opcional) Você pode especificar uma senha para o arquivo de chave de nome forte.  
  
7.  Clique em **OK**.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
9. No menu **Compilar**, clique em **Compilar Solução**.  
  
    Em seguida, você deve instalar o assembly de modo que ele seja carregado quando você implantar projetos do SQL.  
  
## <a name="install-a-deployment-contributor"></a><a name="InstallDeploymentContributor"></a>Instalar um colaborador de implantação  
Para instalar um colaborador de implantação, você deverá copiar o assembly e o arquivo .pdb associado à pasta Extensões.  
  
#### <a name="to-install-the-myotherdeploymentcontributor-assembly"></a>Para instalar o assembly MyOtherDeploymentContributor  
  
1.  Em seguida, você copiará as informações de assembly para o diretório Extensões. Quando o Visual Studio iniciar, ele identificará as extensões no diretório e subdiretórios %Arquivos de Programas%\Microsoft SQL Server\110\DAC\Bin\Extensions e as tornará disponíveis para uso.  
  
2.  Copie o arquivo de assembly **MyOtherDeploymentContributor.dll** do diretório de saída para o diretório %Arquivos de Programas%Microsoft SQL Server\110\DAC\Bin\Extensions. Por padrão, o caminho do seu arquivo compilado .dll é YourSolutionPath\YourProjectPath\bin\Debug ou YourSolutionPath\YourProjectPath\bin\Release.  
  
## <a name="run-or-test-your-deployment-contributor"></a><a name="TestDeploymentContributor"></a>Executar ou testar seu Colaborador de Implantação  
Para executar ou testar seu colaborador de implantação, você deverá realizar as seguintes tarefas:  
  
-   Adicionar propriedades ao arquivo .sqlproj que você planeja criar.  
  
-   Implantar o projeto de banco de dados usando MSBuild e fornecendo os parâmetros apropriados.  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>Adicionar Propriedades ao arquivo de projeto SQL (.sqlproj)  
Você sempre deve atualizar o arquivo de projeto SQL para especificar a ID dos colaboradores que você deseja executar. É possível fazer isso de duas formas:  
  
1.  Você pode modificar manualmente o arquivo .sqlproj para adicionar os argumentos necessários. Você pode escolher fazer isso se seu colaborador não tiver nenhum argumento de colaborador necessário para configuração ou se você não quiser reutilizar o colaborador de compilação em um número grande de projetos. Se você escolher esta opção, adicione as seguintes instruções ao arquivo .sqlproj após o primeiro nó de importação no arquivo:  
  
    ```  
    <PropertyGroup>  
      <DeploymentContributors>  
        $(DeploymentContributors); MyOtherDeploymentContributor.RestartableScriptContributor  
      </DeploymentContributors>  
    </PropertyGroup>  
    ```  
  
2.  O segundo método é criar um arquivo de destino que contém argumentos necessários de colaborador. Isso será útil se você estiver usando o mesmo colaborador para vários projetos e tiver argumentos de colaborador necessários, porque isso incluirá os valores padrão. Nesse caso, crie um arquivo de destino no caminho de extensões do MSBuild:  
  
    1.  Navegue para %Arquivos de programas%\MSBuild.  
  
    2.  Crie uma nova pasta "MyContributors" na qual os arquivos de destino serão armazenados.  
  
    3.  Crie um novo arquivo "MyContributors.targets" dentro desse diretório, adicione o seguinte texto e salve o arquivo:  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <DeploymentContributors>$(DeploymentContributors);MyOtherDeploymentContributor.RestartableScriptContributor</DeploymentContributors>  
          </PropertyGroup>  
        </Project>  
  
        ```  
  
    4.  Dentro do arquivo .sqlproj para qualquer projeto que você quiser executar colaboradores, importe o arquivo de destino adicionando a seguinte instrução ao arquivo .sqlproj após o nó \<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> no arquivo:  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
  
        ```  
  
Depois que você tiver seguido uma destas abordagens, poderá usar MSBuild para passar parâmetros para compilações de linha de comando.  
  
> [!NOTE]  
> Você sempre deve atualizar a propriedade “DeploymentContributors” para especificar sua ID de colaborador. Esta é a mesma ID usada no atributo "ExportDeploymentPlanModifier" no seu arquivo de origem de colaborador. Sem isso, seu colaborador não será executado ao criar o projeto. A propriedade "ContributorArguments" precisará ser atualizada somente se você tiver os argumentos necessários para seu colaborador ser executado.  
  
## <a name="deploy-the-database-project"></a>Implantar o projeto de banco de dados  
  
#### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>Para implantar o projeto SQL e gerar um relatório de implantação  
  
-   Seu projeto pode ser publicado ou implantado normalmente dentro do Visual Studio. Basta abrir uma solução contendo seu projeto SQL e escolher a opção Publicar… no menu de contexto aberto clicando com o botão direito do mouse para o projeto ou usar F5 para uma implantação de depuração para o LocalDB. Neste exemplo, usaremos a caixa de diálogo "Publicar…" para gerar um script de implantação.  
  
    1.  Abra o Visual Studio e abra a solução que contém o seu projeto SQL.  
  
    2.  Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha a opção **Publicar...** .  
  
    3.  Defina o nome do servidor e o nome do banco de dados para publicação.  
  
    4.  Escolha **Gerar Script** das opções na parte inferior da caixa de diálogo. Isso criará um script que pode ser usado para implantação. Nós examinaremos isso para verificar se nossas instruções IF foram adicionadas para tornar o script reiniciável.  
  
    5.  Examine o script de implantação resultante. Imediatamente antes da seção rotulada "Modelo de Script de Pré-Implantação", você deverá ver algo que se assemelha à seguinte sintaxe Transact-SQL:  
  
        ```  
        :setvar CompletedBatches __completedBatches_CompareProjectDB_cd1e348a-8f92-44e0-9a96-d25d65900fca  
        :setvar TotalBatchCount 17  
        GO  
  
        if OBJECT_ID(N'tempdb.dbo.$(CompletedBatches)', N'U') is null  
        begin  
        use tempdb  
        create table [dbo].[$(CompletedBatches)]  
        (  
        BatchId int primary key,  
        Description nvarchar(300)  
        )  
        use [$(DatabaseName)]  
        end  
  
        ```  
  
        Posteriormente no script de implantação, em cada lote, você vê uma instrução IF que cerca a instrução original. Por exemplo, o seguinte pode aparecer para uma instrução CREATE SCHEMA:  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 0)  
            BEGIN  
                EXECUTE sp_executesql @stmt = N'CREATE SCHEMA [Sales]  
            AUTHORIZATION [dbo]';  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (0, N'CreateElementStep Sales batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        Observe que CREATE SCHEMA é uma das instruções que devem ser incluídas dentro de uma instrução EXECUTE sp_executesql dentro da instrução IF. As instruções como CREATE TABLE não exigem a instrução EXECUTE sp_executesql e se parecerão com o seguinte exemplo:  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 1)  
            BEGIN  
                CREATE TABLE [Sales].[Customer] (  
                    [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
                    [CustomerName] NVARCHAR (40) NOT NULL,  
                    [YTDOrders]    INT           NOT NULL,  
                    [YTDSales]     INT           NOT NULL  
                );  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (1, N'CreateElementStep Sales.Customer batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        > [!NOTE]  
        > Se você implantar um projeto de banco de dados que seja idêntico ao banco de dados de destino, o relatório resultante não será muito significativo. Para obter mais resultados significativos, implante as alterações em um banco de dados ou implante um novo banco de dados.  
  
## <a name="command-line-deployment-using-generated-dacpac-file"></a>Implantação de linha de comando usando o arquivo dacpac gerado  
Uma vez que um projeto SQL tiver sido compilado, um arquivo dacpac é criado que pode ser usado para implantar o esquema da linha de comando, e que pode habilitar a implantação de um computador diferente como um computador de compilação. O SqlPackage é um utilitário de linha de comando que permite a implantação de dacpacs com uma gama completa de opções que permitem que os usuários implantem um dacpac ou gerem um script de implantação, entre outras ações. Para saber mais, confira [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080(v=VS.103).aspx).  
  
> [!NOTE]  
> Para implantar dacpacs com êxito criados de projetos com a propriedade DeploymentContributors definida, os DLL que contêm os colaboradores de implantação devem ser instalados no computador que está sendo usado. Isso ocorre porque eles foram marcados conforme o necessário para que a implantação fosse concluída com êxito.  
>   
> Para evitar esse requisito, exclua o colaborador de implantação do arquivo .sqlproj. Em vez disso, especifique que os colaboradores sejam executados durante a implantação usando SqlPackage com o parâmetro **AdditionalDeploymentContributors**. Isso é útil em casos em que você deseja usar apenas um colaborador para circunstâncias especiais, como implantação em um servidor específico.  
  
## <a name="next-steps"></a>Próximas etapas  
Você pode fazer experiências com outros tipos de modificações nos planos de implantação antes de serem executados. Alguns outros tipos de modificações que talvez você queira fazer incluem:  
  
-   Adicionar uma propriedade estendida a todos os objetos de banco de dados que associam um número de versão com eles.  
  
-   Adicionar ou remover instruções ou comentários de diagnóstico adicionais dos scripts de implantação.  
  
## <a name="see-also"></a>Consulte Também  
[Personalizar a compilação e a implantação do banco de dados usando os colaboradores de compilação e implantação](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[Passo a passo: estender a compilação do projeto de banco de dados para gerar as estatísticas do modelo](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)  
[Passo a passo: estender a implantação do projeto de banco de dados para analisar o plano de implantação](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
