---
title: Como criar um assembly de regra de análise de código estático personalizado para o SQL Server
description: Saiba como criar regras do Code Analysis no SQL Server. Configure uma regra para evitar declarações WAITFOR DELAY em procedimentos armazenados, gatilhos e funções.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: f7b6ed8c-a4e0-4e33-9858-a8aa40aef309
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c734a2907ec4ad2d312385976013f8c1c39effcc
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987722"
---
# <a name="walkthrough-authoring-a-custom-static-code-analysis-rule-assembly-for-sql-server"></a>Passo a passo da criação de um assembly de regra de análise de código estático personalizado para o SQL Server

Este passo a passo demonstra as etapas usadas para criar uma regra de Análise de Código do SQL Server. A regra criada neste passo a passo é usada para evitar instruções WAITFOR DELAY em procedimentos armazenados, gatilhos e funções.  
  
Neste passo a passo, você criará uma regra personalizada para análise de código estático Transact\-SQL usando os seguintes processos:  
  
1. Crie uma biblioteca de classes, habilite a assinatura para o projeto e adicione as referências necessárias.  
  
2. Crie uma classe de regra personalizada do Visual C\#.  
  
3. Crie duas classes auxiliares de Visual C\#.  
  
4. Copie a DLL resultante criada para o diretório Extensões para instalá-la.  
  
5. Verifique se a nova regra de análise de código está em vigor.  
  
**Pré-requisitos**
  
Você precisará dos seguintes componentes para concluir este passo a passo:  
  
- Você deverá ter instalada uma versão do Visual Studio que inclui o SQL Server Data Tools e dá suporte ao desenvolvimento em Visual C\# ou Visual Basic.  
  
- Você deve ter um projeto do SQL Server que contenha objetos de SQL Server.  
  
- Uma instância do SQL Server ao qual você poderá implantar um projeto de banco de dados.  
  
> [!NOTE]  
> Este passo a passo é destinado a usuários que já estão familiarizados com os recursos de SQL Server do SQL Server Data Tools. Você também já deverá estar familiarizado com os conceitos do Visual Studio, por exemplo, como criar uma biblioteca de classe e como usar o editor de código para adicionar código a uma classe.  
  
## <a name="creating-a-custom-code-analysis-rule-for-sql-server"></a>Criando uma regra de análise de código personalizado para SQL Server  

Em primeiro lugar, crie uma biblioteca de classes. Para criar um projeto de biblioteca de classes:  
  
1. Crie um projeto de biblioteca de classe do Visual Basic ou Visual C\# denominado SampleRules.  
  
2. Renomeie o arquivo Class1.cs para AvoidWaitForDelayRule.cs.  
  
3. No Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e, depois, clique em **Adicionar referência**.  
  
4. Selecione System.ComponentModel.Composition na guia Estruturas.  
  
5. Clique em **Procurar** e navegue até o diretório C:\Arquivos de Programas (x86)\\Microsoft SQL Server\120\SDK\Assemblies, selecione Microsoft.SqlServer.TransactSql.ScriptDom.dll e clique em OK.  
  
6. Em seguida, instale as referências DACFx necessárias. Clique em **Procurar** e navegue até o diretório <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120. Escolha as entradas Microsoft.SqlServer.Dac.dll, Microsoft.SqlServer.Dac.Extensions.dll e Microsoft.Data.Tools.Schema.Sql.dll, clique em **Adicionar** e em **OK**.  
  
    Agora, os binários do DACFx estão instalados em seu diretório de instalação do Visual Studio. Para o Visual Studio 2012, <Visual Studio Install Dir> geralmente será C:\Arquivos de Programas (x86)\\MicrosoftVisual Studio 11.0. Para o Visual Studio 2013, geralmente será C:\Arquivos de Programas (x86)\\MicrosoftVisual Studio 12.0.  
  
Em seguida, você adicionará as classes de suporte que serão usadas pela regra.  
  
## <a name="creating-the-custom-code-analysis-rule-supporting-classes"></a>Criação das Classes de suporte de regra de análise de código personalizado

Antes de criar a classe para a regra em si, você adicionará uma classe do visitante e uma classe de atributo ao projeto. Essas classes podem ser úteis para a criação de regras personalizadas adicionais.  
  
A primeira classe que você deve definir é a classe WaitForDelayVisitor, derivada de [TSqlConcreteFragmentVisitor](/dotnet/api/microsoft.sqlserver.transactsql.scriptdom.tsqlconcretefragmentvisitor). Essa classe fornece acesso às instruções WAITFOR DELAY no modelo. As classes de visitante utilizam as APIs [ScriptDom](/dotnet/api/microsoft.sqlserver.transactsql.scriptdom) fornecidas pelo SQL Server. Nessa API, o código Transact\-SQL é representado como uma AST (árvore de sintaxe abstrata) e as classes de visitante podem ser úteis quando você deseja localizar objetos de sintaxe específica, como as instruções de WAITFORDELAY. Podem ser difíceis de encontrar usando o modelo de objeto, pois não estão associadas a uma propriedade específica de objeto ou relação, mas é fácil encontrá-las usando o padrão do visitante e a API [ScriptDom](/dotnet/api/microsoft.sqlserver.transactsql.scriptdom).  
  
### <a name="defining-the-waitfordelayvisitor-class"></a>Definição da classe WaitForDelayVisitor  
  
1. No **Gerenciador de Soluções**, selecione o projeto SampleRules.  
  
2. No menu **Projeto**, selecione **Adicionar classe**. A caixa de diálogo **Adicionar Novo Item** aparecerá.  
  
3. Na caixa de texto **Nome**, digite WaitForDelayVisitor.cs e, em seguida, clique no botão **Adicionar**. O arquivo WaitForDelayVisitor.cs é adicionado ao projeto no **Gerenciador de Soluções**.  
  
4. Abra o arquivo WaitForDelayVisitor.cs e atualize o conteúdo de acordo com o código a seguir:  
  
    ```  
    using System.Collections.Generic;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    namespace SampleRules {  
        class WaitForDelayVistor {}  
    }  
    ```  
  
5. Na declaração da classe, altere o modificador de acesso para interno e derive a classe de TSqlConcreteFragmentVisitor:  
  
    ```  
    internal class WaitForDelayVisitor : TSqlConcreteFragmentVisitor {}  
    ```  
  
6. Adicione o código a seguir para definir a variável de membro da Lista:  
  
    ```  
    public IList<WaitForStatement> WaitForDelayStatements { get; private set; }  
    ```  
  
7. Defina o construtor da classe adicionando o seguinte código:  
  
    ```  
    public WaitForDelayVisitor() {  
       WaitForDelayStatments = new List<WaitForStatement>();  
    }  
    ```  
  
8. Substitua o método ExplicitVisit, adicionando o seguinte código:  
  
    ```  
    public override void ExplicitVisit(WaitForStatement node) {  
       // We are only interested in WAITFOR DELAY occurrences  
       if (node.WaitForOption == WaitForOption.Delay)  
          WaitForDelayStatments.Add(node);  
    }  
    ```  
  
    Esse método visita as instruções WAITFOR no modelo e adiciona as que têm a opção DELAY especificada para a lista de instruções WAITFOR DELAY. A principal classe mencionada aqui é [WaitForStatement](/dotnet/api/microsoft.sqlserver.transactsql.scriptdom.waitforstatement).  
  
9. No menu **Arquivo** , clique em **Salvar**.  
  
A segunda classe é LocalizedExportCodeAnalysisRuleAttribute.cs. Ela é uma extensão do Microsoft.SqlServer.Dac.CodeAnalysis.ExportCodeAnalysisRuleAttribute interno fornecido pela estrutura e dá suporte à leitura de DisplayName e Description, usada por sua regra de um arquivo de recursos. Essa é uma classe útil se você pretender ter suas regras usadas em vários idiomas.  
  
### <a name="defining-the-localizedexportcodeanalysisruleattribute-class"></a>Definição da classe LocalizedExportCodeAnalysisRuleAttribute  
  
1. No **Gerenciador de Soluções**, selecione o projeto SampleRules.  
  
2. No menu **Projeto**, selecione **Adicionar classe**. A caixa de diálogo **Adicionar Novo Item** aparecerá.  
  
3. Na caixa de texto **Nome**, digite LocalizedExportCodeAnalysisRuleAttribute.cs e clique no botão **Adicionar**. O arquivo é adicionado ao projeto no **Gerenciador de Soluções**.  
  
4. Abra o arquivo e atualize o conteúdo de acordo com o código a seguir:  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using System;  
    using System.Globalization;  
    using System.Reflection;  
    using System.Resources;  
  
    namespace SampleRules  
    {  
  
        internal class LocalizedExportCodeAnalysisRuleAttribute : ExportCodeAnalysisRuleAttribute  
        {  
            private readonly string _resourceBaseName;  
            private readonly string _displayNameResourceId;  
            private readonly string _descriptionResourceId;  
  
            private ResourceManager _resourceManager;  
            private string _displayName;  
            private string _descriptionValue;  
  
            /// <summary>  
            /// Creates the attribute, with the specified rule ID, the fully qualified  
            /// name of the resource file that will be used for looking up display name  
            /// and description, and the Ids of those resources inside the resource file.  
            /// </summary>  
            public LocalizedExportCodeAnalysisRuleAttribute(  
                string id,  
                string resourceBaseName,  
                string displayNameResourceId,  
                string descriptionResourceId)  
                : base(id, null)  
            {  
                _resourceBaseName = resourceBaseName;  
                _displayNameResourceId = displayNameResourceId;  
                _descriptionResourceId = descriptionResourceId;  
            }  
  
            /// <summary>  
            /// Rules in a different assembly would need to overwrite this  
            /// </summary>  
            /// <returns></returns>  
            protected virtual Assembly GetAssembly()  
            {  
                return GetType().Assembly;  
            }  
  
            private void EnsureResourceManagerInitialized()  
            {  
                var resourceAssembly = GetAssembly();  
  
                try  
                {  
                    _resourceManager = new ResourceManager(_resourceBaseName, resourceAssembly);  
                }  
                catch (Exception ex)  
                {  
                    var msg = String.Format(CultureInfo.CurrentCulture, RuleResources.CannotCreateResourceManager, _resourceBaseName, resourceAssembly);  
                    throw new RuleException(msg, ex);  
                }  
            }  
  
            private string GetResourceString(string resourceId)  
            {  
                EnsureResourceManagerInitialized();  
                return _resourceManager.GetString(resourceId, CultureInfo.CurrentUICulture);  
            }  
  
            /// <summary>  
            /// Overrides the standard DisplayName and looks up its value inside a resources file  
            /// </summary>  
            public override string DisplayName  
            {  
                get  
                {  
                    if (_displayName == null)  
                    {  
                        _displayName = GetResourceString(_displayNameResourceId);  
                    }  
                    return _displayName;  
                }  
            }  
  
            /// <summary>  
            /// Overrides the standard Description and looks up its value inside a resources file  
            /// </summary>  
            public override string Description  
            {  
                get  
                {  
                    if (_descriptionValue == null)  
                    {   
                        _descriptionValue = GetResourceString(_descriptionResourceId);  
                    }  
                    return _descriptionValue;  
                }  
            }  
        }  
    }  
    ```  
  
Em seguida, você pode adicionar um arquivo de recurso que definirá o nome da regra, a descrição da regra e a categoria na qual a regra aparecerá na interface de configuração de regra.  
  
### <a name="to-add-a-resource-file-and-three-resource-strings"></a>Para adicionar um arquivo de recurso e três cadeias de caracteres de recurso  
  
1. No **Gerenciador de Soluções**, selecione o projeto SampleRules.  
  
2. No menu **Projeto**, selecione **Adicionar novo item**. A caixa de diálogo **Adicionar Novo Item** aparecerá.  
  
3. Na lista de **Modelos instalados**, clique em **Geral**.  
  
4. No painel de detalhes, clique em **Arquivo de recursos**.  
  
5. Em **Nome**, digite RuleResources.resx. O editor de recurso aparece sem recursos definidos.  
  
6. Defina quatro cadeias de caracteres de recurso da seguinte maneira:  
  
    |Nome|Valor|  
    |--------|---------|  
    |AvoidWaitForDelay_ProblemDescription|A instrução WAITFOR DELAY foi encontrada em {0}.|  
    |AvoidWaitForDelay_RuleName|Evite usar as instruções WaitFor Delay em procedimentos, funções e gatilhos armazenados.|  
    |CategorySamples|SamplesCategory|  
    |CannotCreateResourceManager|Não é possível criar o ResourceManager para {0} de {1}.|  
  
7. No menu **Arquivo**, clique em **Salvar RuleResources.resx**.  
  
Em seguida, defina uma classe que faz referência aos recursos no arquivo de recursos que são usados pelo Visual Studio para exibir informações sobre a regra na interface do usuário.  
  
### <a name="defining-the-sampleconstants-class"></a>Definição da classe SampleConstants  
  
1. No **Gerenciador de Soluções**, selecione o projeto SampleRules.  
  
2. No menu **Projeto**, selecione **Adicionar classe**. A caixa de diálogo **Adicionar Novo Item** aparecerá.  
  
3. Na caixa de texto **Nome**, digite SampleRuleConstants.cs e clique no botão **Adicionar**. O arquivo SampleRuleConstants.cs é adicionado ao projeto no **Gerenciador de Soluções**.  
  
4. Abra o arquivo SampleRuleConstants.cs e adicione as instruções using a seguir ao arquivo:  
  
    ```  
    namespace SampleRules  
    {   
        internal static class RuleConstants  
        {  
            /// <summary>  
            /// The name of the resources file to use when looking up rule resources  
            /// </summary>  
            public const string ResourceBaseName = "Public.Dac.Samples.Rules.RuleResources";  
  
            /// <summary>  
            /// Lookup name inside the resources file for the select asterisk rule name  
            /// </summary>  
            public const string AvoidWaitForDelay_RuleName = "AvoidWaitForDelay_RuleName";  
            /// <summary>  
            /// Lookup ID inside the resources file for the select asterisk description  
            /// </summary>  
            public const string AvoidWaitForDelay_ProblemDescription = "AvoidWaitForDelay_ProblemDescription";  
  
            /// <summary>  
            /// The design category (should not be localized)  
            /// </summary>  
            public const string CategoryDesign = "Design";  
  
            /// <summary>  
            /// The performance category (should not be localized)  
            /// </summary>  
            public const string CategoryPerformance = "Design";  
        }  
    }  
    ```  
  
5. Clique em **Arquivo** > **Salvar**.  
  
## <a name="creating-the-custom-code-analysis-rule-class"></a>Criação da classe de regra de análise de código personalizado

Agora que você adicionou as classes auxiliares que a regra de Análise de código personalizada usará, crie uma classe de regra personalizada e nomeie-a como AvoidWaitForDelayRule. A regra personalizada AvoidWaitForDelayRule será usada para ajudar os desenvolvedores de banco de dados a evitar instruções WAITFOR DELAY em procedimentos armazenados, gatilhos e funções.  
  
### <a name="creating-the-avoidwaitfordelayrule-class"></a>Criando a classe AvoidWaitForDelayRule  
  
1. No **Gerenciador de Soluções**, selecione o projeto SampleRules.  
  
2. No menu **Projeto**, selecione **Adicionar classe**. A caixa de diálogo **Adicionar Novo Item** aparecerá.  
  
3. Na caixa de texto **Nome**, digite AvoidWaitForDelayRule.cs e clique em **Adicionar**. O arquivo AvoidWaitForDelayRule.cs é adicionado ao projeto no **Gerenciador de Soluções**.  
  
4. Abra o arquivo AvoidWaitForDelayRule.cs e adicione as instruções using a seguir ao arquivo:  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;   
    namespace SampleRules {  
        class AvoidWaitForDelayRule {}  
    }  
    ```  
  
5. Na declaração de classe AvoidWaitForDelayRule, altere o modificador de acesso para público:  
  
    ```  
    /// <summary>  
    /// This is a rule that returns a warning message   
    /// whenever there is a WAITFOR DELAY statement appears inside a subroutine body.  
    /// This rule only applies to stored procedures, functions and triggers.  
    /// </summary>  
    public sealed class AvoidWaitForDelayRule  
    ```  
  
6. Derive a classe AvoidWaitForDelayRule da classe base Microsoft.SqlServer.Dac.CodeAnalysis.SqlCodeAnalysisRule:  
  
    ```  
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    ```  
  
7. Adicione o LocalizedExportCodeAnalysisRuleAttribute à sua classe.  
  
    O LocalizedExportCodeAnalysisRuleAttribute permite que o serviço de análise de código descubra as regras de análise de código personalizado. Somente as classes marcadas com um ExportCodeAnalysisRuleAttribute (ou um atributo que seja herdeiro disso) podem ser usadas na análise de código.  
  
    O LocalizedExportCodeAnalysisRuleAttribute fornece alguns metadados necessários usados pelo serviço. Isso inclui uma ID exclusiva para tal regra, um nome de exibição que será mostrado na interface do usuário do Visual Studio e uma Descrição que pode ser usada pela sua regra ao identificar problemas.  
  
    ```  
    [LocalizedExportCodeAnalysisRule(AvoidWaitForDelayRule.RuleId,  
        RuleConstants.ResourceBaseName,  
        RuleConstants.AvoidWaitForDelay_RuleName,   
        RuleConstants.AvoidWaitForDelay_ProblemDescription  
        Category = RuleConstants.CategoryPerformance,   
        RuleScope = SqlRuleScope.Element)]   
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    {  
       /// <summary>  
       /// The Rule ID should resemble a fully-qualified class name. In the Visual Studio UI  
       /// rules are grouped by "Namespace + Category", and each rule is shown using "Short ID: DisplayName".  
       /// For this rule, that means the grouping will be "Public.Dac.Samples.Performance", with the rule  
       /// shown as "SR1004: Avoid using WaitFor Delay statements in stored procedures, functions and triggers."  
       /// </summary>  
       public const string RuleId = "RuleSamples.SR1004";  
    }  
    ```  
  
    A propriedade RuleScope deve ser Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Element, pois essa regra analisará os elementos específicos. A regra será chamada uma vez para cada elemento correspondente no modelo. Caso deseje analisar um modelo inteiro, pode usar Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Model.  
  
8. Adicione um construtor que configure o Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.SupportedElementTypes. Isso é necessário para regras de escopo do elemento. Define os tipos de elementos aos quais essa regra será aplicada. Nesse caso, a regra será aplicada para procedimentos armazenados, gatilhos e funções. Observe que a classe Microsoft.SqlServer.Dac.Model.ModelSchema lista todos os tipos de elemento disponíveis que podem ser analisados.  
  
    ```  
    public AvoidWaitForDelayRule()  
    {  
       // This rule supports Procedures, Functions and Triggers. Only those objects will be passed to the Analyze method  
       SupportedElementTypes = new[]  
       {  
          // Note: can use the ModelSchema definitions, or access the TypeClass for any of these types  
          ModelSchema.ExtendedProcedure,  
          ModelSchema.Procedure,  
          ModelSchema.TableValuedFunction,  
          ModelSchema.ScalarFunction,  
  
          ModelSchema.DatabaseDdlTrigger,  
          ModelSchema.DmlTrigger,  
          ModelSchema.ServerDdlTrigger  
       };  
    }  
    ```  
  
9. Adicione uma substituição para o método Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.Analyze(Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext), que usa Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext como parâmetros de entrada. Esse método retorna uma lista de possíveis problemas.  
  
    O método obtém o Microsoft.SqlServer.Dac.Model.TSqlModel, o Microsoft.SqlServer.Dac.Model.TSqlObject e o [TSqlFragment](/dotnet/api/microsoft.sqlserver.transactsql.scriptdom.tsqlfragment) do parâmetro de contexto. A classe WaitForDelayVisitor é, então, usada para obter uma lista de todas as instruções WAITFOR DELAY presentes no modelo.  
  
    Para cada [WaitForStatement](/dotnet/api/microsoft.sqlserver.transactsql.scriptdom.waitforstatement) nessa lista, é criado um Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleProblem.  
  
    ```  
    /// <summary>  
    /// For element-scoped rules the Analyze method is executed once for every matching   
    /// object in the model.   
    /// </summary>  
    /// <param name="ruleExecutionContext">The context object contains the TSqlObject being   
    /// analyzed, a TSqlFragment  
    /// that's the AST representation of the object, the current rule's descriptor, and a   
    /// reference to the model being  
    /// analyzed.  
    /// </param>  
    /// <returns>A list of problems should be returned. These will be displayed in the Visual   
    /// Studio error list</returns>  
    public override IList<SqlRuleProblem> Analyze(  
        SqlRuleExecutionContext ruleExecutionContext)  
    {  
         IList<SqlRuleProblem> problems = new List<SqlRuleProblem>();  
  
         TSqlObject modelElement = ruleExecutionContext.ModelElement;  
  
         // this rule does not apply to inline table-valued function  
         // we simply do not return any problem in that case.  
         if (IsInlineTableValuedFunction(modelElement))  
         {  
             return problems;  
         }  
  
         string elementName = GetElementName(ruleExecutionContext, modelElement);  
  
         // The rule execution context has all the objects we'll need, including the   
         // fragment representing the object,  
         // and a descriptor that lets us access rule metadata  
         TSqlFragment fragment = ruleExecutionContext.ScriptFragment;  
         RuleDescriptor ruleDescriptor = ruleExecutionContext.RuleDescriptor;  
  
         // To process the fragment and identify WAITFOR DELAY statements we will use a   
         // visitor   
         WaitForDelayVisitor visitor = new WaitForDelayVisitor();  
         fragment.Accept(visitor);  
         IList<WaitForStatement> waitforDelayStatements = visitor.WaitForDelayStatements;  
  
         // Create problems for each WAITFOR DELAY statement found   
         // When creating a rule problem, always include the TSqlObject being analyzed. This   
         // is used to determine  
         // the name of the source this problem was found in and a best guess as to the   
         // line/column the problem was found at.  
         //  
         // In addition if you have a specific TSqlFragment that is related to the problem   
         //also include this  
         // since the most accurate source position information (start line and column) will   
         // be read from the fragment  
         foreach (WaitForStatement waitForStatement in waitforDelayStatements)  
         {  
            SqlRuleProblem problem = new SqlRuleProblem(  
                String.Format(CultureInfo.CurrentCulture,   
                    ruleDescriptor.DisplayDescription, elementName),  
                modelElement,  
                waitForStatement);  
            problems.Add(problem);  
        }  
        return problems;  
    }  
  
    private static string GetElementName(  
        SqlRuleExecutionContext ruleExecutionContext,   
        TSqlObject modelElement)  
    {  
        // Get the element name using the built in DisplayServices. This provides a number of   
        // useful formatting options to  
        // make a name user-readable  
        var displayServices = ruleExecutionContext.SchemaModel.DisplayServices;  
        string elementName = displayServices.GetElementName(  
            modelElement, ElementNameStyle.EscapedFullyQualifiedName);  
        return elementName;  
    }  
  
    private static bool IsInlineTableValuedFunction(TSqlObject modelElement)  
    {  
        return TableValuedFunction.TypeClass.Equals(modelElement.ObjectType)  
                       && FunctionType.InlineTableValuedFunction ==   
            modelElement.GetMetadata<FunctionType>(TableValuedFunction.FunctionType);  
    }  
    ```  
  
10. Clique em **Arquivo** > **Salvar**.  
  
### <a name="building-the-class-library"></a>Compilação da biblioteca de classes  
  
1. No menu **Projeto**, clique em **Propriedades de SampleRules**.  
  
2. Clique na guia **Assinatura** .  
  
3. Clique em **Assinar o assembly**.  
  
4. Em **Escolher um arquivo de chave de nome forte**, clique em **<New>** .  
  
5. Na caixa de diálogo **Criar chave de nome forte**, em **Nome do arquivo de chaves**, digite MyRefKey.  
  
6. (opcional) Você pode especificar uma senha para o arquivo de chave de nome forte.  
  
7. Clique em **OK**.  
  
8. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
9. No menu **Compilar**, clique em **Compilar Solução**.  
  
Em seguida, você deve instalar o assembly de modo que ele seja carregado quando você compilar e implantar projetos do SQL Server.  
  
## <a name="install-a-static-code-analysis-rule"></a>Instalar uma regra de análise de código estático

Para instalar uma regra, você deverá copiar o assembly e o arquivo .pdb associado à pasta Extensões.  
  
### <a name="to-install-the-samplerules-assembly"></a>Para instalar o Assembly SampleRules

Em seguida, você copiará as informações de assembly para o diretório Extensões. Ao iniciar, o Visual Studio identificará todas as extensões no diretório e subdiretórios <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions, além de disponibilizá-las para uso.  
  
Para o Visual Studio 2012, <Visual Studio Install Dir> geralmente será C:\Arquivos de Programas (x86)\\MicrosoftVisual Studio 11.0. Para o Visual Studio 2013, geralmente será C:\Arquivos de Programas (x86)\\MicrosoftVisual Studio 12.0.  
  
Copie o arquivo do assembly SampleRules.dll do diretório de saída para o diretório <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions. Por padrão, o caminho do seu arquivo compilado .dll é YourSolutionPath\YourProjectPath\bin\Debug ou YourSolutionPath\YourProjectPath\bin\Release.  
  
A regra já deve estar instalada e será exibida após o reinício do Visual Studio. Em seguida, você iniciará uma nova sessão do Visual Studio e criará um projeto de banco de dados.  
  
### <a name="starting-a-new-visual-studio-session-and-creating-a-database-project"></a>Iniciar uma nova sessão do Visual Studio e criar um projeto de banco de dados  
  
1. Inicie uma segunda sessão do Visual Studio.  
  
2. Clique em **Arquivo** > **Novo** > **Projeto**.  
  
3. Na caixa de diálogo **Novo projeto**, na lista de **Modelos instalados**, expanda o nó **SQL Server** e clique em **Projeto de Banco de Dados do SQL Server**.  
  
4. Na caixa de texto **Nome**, digite SampleRulesDB e clique em **OK**.  
  
Por fim, você verá a nova regra exibida no projeto SQL Server. Para exibir a nova regra de análise de código AvoidWaitForRule:  
  
1. No **Gerenciador de Soluções**, selecione o projeto SampleRulesDB.  
  
2. No menu **Projeto** , clique em **Propriedades**. A página de propriedades SampleRulesDB é exibida.  
  
3. Clique em **Análise de código**. Você deve ver uma nova categoria chamada RuleSamples.CategorySamples.  
  
4. Expanda RuleSamples .CategorySamples. Você deve ver SR1004: evite a declaração WAITFOR DELAY em procedimentos armazenados, gatilhos e funções.  
  
## <a name="see-also"></a>Consulte Também

[Visão geral de extensibilidade para regras de análise de código do banco de dados](../ssdt/overview-of-extensibility-for-database-code-analysis-rules.md)