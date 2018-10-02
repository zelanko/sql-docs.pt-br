---
title: 'Passo a passo: usar uma condição de teste personalizada para verificar os resultados de um procedimento armazenado | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4c33b494-a85e-4dd2-97b6-c88ee858a99c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f109fd19d6c74fc60746fdccd5560b8aa482eb02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832994"
---
# <a name="walkthrough-using-a-custom-test-condition-to-verify-the-results-of-a-stored-procedure"></a>Passo a passo: usando uma condição de teste personalizada para verificar os resultados de um procedimento armazenado
Neste passo a passo da extensão de recursos, você criará uma condição de teste e verificará sua funcionalidade criando um teste de unidade do SQL Server. O processo inclui criar um projeto de biblioteca de classes para a condição de teste, além de assiná-lo e instalá-lo. Se você já tiver uma condição de teste para atualização, confira [Como atualizar uma condição de teste personalizado do Visual Studio 2010 de uma versão anterior do SQL Server Data Tools](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md).  
  
Este passo a passo ilustra as seguintes tarefas:  
  
-   Como criar uma condição de teste.  
  
-   Como assinar o assembly com um nome forte.  
  
-   Como adicionar as referências necessárias para o projeto.  
  
-   Como criar uma condição de teste.  
  
-   Como instalar a nova condição de teste.  
  
-   Como testar a nova condição de teste.  
  
Você deve ter o Visual Studio 2010 ou Visual Studio 2012 com a versão mais recente do SQL Server Data Tools para concluir este passo a passo. Para saber mais, confira [Instalar o SQL Server Data Tools](../ssdt/install-sql-server-data-tools.md).  
  
## <a name="creating-a-custom-test-condition"></a>Criando uma condição de teste personalizada  
Primeiro, você criará uma biblioteca de classes.  
  
1.  No menu **Arquivo**, clique em **Novo** e, depois, em **Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto**, em **Tipos de Projeto**, clique em Visual C\#.  
  
3.  Em **Modelos**, selecione **Biblioteca de Classes**.  
  
4.  Na caixa de texto **Nome**, digite **ColumnCountCondition** e clique em **OK**.  
  
Em seguida, assine o projeto.  
  
1.  No menu **Projeto**, clique em **Propriedades ColumnCountCondition**.  
  
2.  Na guia **Assinatura**, marque a caixa de seleção **Assinar o assembly**.  
  
3.  Na caixa de diálogo **Escolher um arquivo de chave de nome forte**, clique em **\<Novo...>**.  
  
    A caixa de diálogo **Criar Chave de Nome Forte** é aberta.  
  
4.  Na caixa **Nome de arquivo de chave**, digite **SampleKey**.  
  
5.  Digite e confirme uma senha e clique em **OK**. Quando você cria sua solução, o arquivo de chave é usado para assinar o assembly.  
  
6.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
7.  No menu **Criar** , clique em **Criar Solução**.  
  
Em seguida, você adicionará as referências necessárias para o projeto.  
  
1.  No **Gerenciador de Soluções**, selecione o projeto **ColumnCountCondition**.  
  
2.  No menu **Projeto**, clique em **Adicionar Referência** para exibir a caixa de diálogo **Adicionar Referência**.  
  
3.  Selecione a guia **.NET**.  
  
4.  Na coluna **Nome do Componente**, localize e selecione o componente **System.ComponentModel.Composition**. Clique em **OK** depois de selecionar o componente.  
  
5.  Adicione as referências de assembly necessárias. Clique com o botão direito do mouse no nó do projeto e clique em **Adicionar Referência**. Clique em **Procurar** e navegue até a pasta C:\Arquivos de Programas (x86)\\Microsoft SQL Server\110\DAC\Bin. Escolha Microsoft.Data.Tools.Schema.Sql.dll, clique em Adicionar e depois em OK.  
  
6.  No menu **Projeto**, clique em **Descarregar Projeto**.  
  
7.  Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolha **Editar <project name>.csproj**.  
  
8.  Adicione a seguinte instrução Import depois da importação de **Microsoft.CSharp.targets**:  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. Salve o arquivo e feche-o. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolha **Recarregar Projeto**.  
  
    As referências necessárias serão mostradas no nó **Referências** do projeto no **Gerenciador de Soluções**.  
  
## <a name="creating-the-resultsetcolumncountcondition-class"></a>Criando a classe ResultSetColumnCountCondition  
Agora, você renomeará **Class1** para **ResultSetColumnCountCondition** e o derivará de [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx). A classe **ResultSetColumnCountCondition** é uma condição de teste simples que verifica o número de colunas retornadas no ResultSet. Você pode usar esta condição para verificar se o contrato para um procedimento armazenado está correto:  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em Class1.cs, clique em **Renomear** e digite **ResultSetColumnCountCondition.cs**.  
  
2.  Clique em **Sim** para confirmar a renomeação de todas as referências para Class1.  
  
3.  Abra o arquivo **ResultSetColumnCountCondition.cs** e adicione as instruções using a seguir:  
  
    ```  
    using System;  
    using System.ComponentModel;  
    using System.Data;  
    using System.Data.Common;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
    namespace ColumnCountCondition {  
        public class ResultSetColumnCountCondition  
    ```  
  
4.  Derive a classe de [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx):  
  
    ```  
    public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
5.  Adicione [ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx). Confira [Como criar condições de teste para o Designer de teste de unidade do SQL Server](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md) para saber mais sobre UnitTesting.Conditions.ExportTestConditionAttribute.  
  
    ```  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
        public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
6.  Crie as variáveis de membro e o construtor:  
  
    ```  
            private int _resultSet;  
            private int _count;  
            private int _batch;  
  
            public ResultSetColumnCountCondition() {  
                _resultSet = 1;  
                _count = 0;  
                _batch = 1;  
            }  
    ```  
  
7.  Substitua o método **Assert**. O método inclui argumentos para **IDbConnection**, que representam a conexão com o banco de dados, e **SqlExecutionResult**. O método usa **DataSchemaException** para tratamento de erros:  
  
    ```  
           //method you need to override  
            //to perform the condition verification  
            public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
            {  
                //call base for parameter validation  
                base.Assert(validationConnection, results);  
  
                //verify batch exists  
                if (results.Length < _batch)  
                    throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
                SqlExecutionResult result = results[_batch - 1];  
  
                //verify resultset exists  
                if (result.DataSet.Tables.Count < ResultSet)  
                    throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
                DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
                //actual condition verification  
                //verify resultset column count matches expected  
                if (table.Columns.Count != Count)  
                    throw new DataException(String.Format(  
                        "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                        ResultSet, table.Columns.Count, Count));  
            }  
  
    Add the following method, which overrides the ToString method:  
    C#  
            //this method is called to provide the string shown in the  
            //test conditions panel grid describing what the condition tests  
            public override string ToString()  
            {  
                return String.Format(  
                    "Condition fails if ResultSet {0} does not contain {1} columns",  
                    ResultSet, Count);  
            }  
    ```  
  
8.  Adicione as seguintes propriedades de condição de teste usando os atributos **CategoryAttribute**, **DisplayNameAttribute** e **DescriptionAttribute**:  
  
    ```  
            //below are the test condition properties  
            //that are exposed to the user in the property browser  
            #region Properties  
  
            //property specifying the resultset for which  
            //you want to check the column count  
            [Category("Test Condition")]  
            [DisplayName("ResultSet")]  
            [Description("ResultSet Number")]  
            public int ResultSet  
            {  
                get { return _resultSet; }  
  
                set  
                {  
                    //basic validation  
                    if (value < 1)  
                        throw new ArgumentException("ResultSet cannot be less than 1");  
  
                    _resultSet = value;  
                }  
            }  
  
            //property specifying  
            //expected column count  
            [Category("Test Condition")]  
            [DisplayName("Count")]  
            [Description("Column Count")]  
            public int Count  
            {  
                get { return _count; }  
  
                set  
                {  
                    //basic validation  
                    if (value < 0)  
                        throw new ArgumentException("Count cannot be less than 0");  
  
                    _count = value;  
                }  
            }  
             #endregion  
    ```  
  
A listagem de código final é:  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace ColumnCountCondition  
{  
  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
    public class ResultSetColumnCountCondition : TestCondition  
    {  
        private int _resultSet;  
        private int _count;  
        private int _batch;  
  
        public ResultSetColumnCountCondition()  
        {  
            _resultSet = 1;  
            _count = 0;  
            _batch = 1;  
        }  
  
        //method you need to override  
        //to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            //call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            //verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            //verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            //actual condition verification  
            //verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        //this method is called to provide the string shown in the  
        //test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        //below are the test condition properties  
        //that are exposed to the user in the property browser  
        #region Properties  
  
        //property specifying the resultset for which  
        //you want to check the column count  
        [Category("Test Condition")]  
        [DisplayName("ResultSet")]  
        [Description("ResultSet Number")]  
        public int ResultSet  
        {  
            get { return _resultSet; }  
  
            set  
            {  
                //basic validation  
                if (value < 1)  
                    throw new ArgumentException("ResultSet cannot be less than 1");  
  
                _resultSet = value;  
            }  
        }  
  
        //property specifying  
        //expected column count  
        [Category("Test Condition")]  
        [DisplayName("Count")]  
        [Description("Column Count")]  
        public int Count  
        {  
            get { return _count; }  
  
            set  
            {  
                //basic validation  
                if (value < 0)  
                    throw new ArgumentException("Count cannot be less than 0");  
  
                _count = value;  
            }  
        }  
  
        #endregion  
    }  
}  
  
```  
  
Em seguida, precisaremos criar o projeto.  
  
## <a name="xxx"></a>Compilando o projeto e instalando sua condição de teste  
No menu **Criar** , clique em **Criar Solução**.  
  
Em seguida, você copiará as informações de assembly para o diretório Extensões. Ao iniciar, o Visual Studio identificará as extensões no diretório e subdiretórios de %Arquivos de Programas%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions e as tornará disponíveis para uso:  
  
Copie o arquivo de assembly **ColumnCountCondition.dll** do diretório de saída para o diretório %Arquivos de Programas%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions.  
  
Por padrão, o caminho do seu arquivo .dll compilado é *YourSolutionPath*\\*YourProjectPath*\bin\Debug ou *YourSolutionPath*\\*YourProjectPath*\bin\Release.  
  
Em seguida, você iniciará uma nova sessão do Visual Studio e criará um projeto de banco de dados. Para iniciar uma nova sessão do Visual Studio e criar um projeto de banco de dados:  
  
1.  Inicie uma segunda sessão do Visual Studio.  
  
2.  No menu **Arquivo**, clique em **Novo** e, depois, em **Projeto**.  
  
3.  Na caixa de diálogo **Novo Projeto**, na lista de modelos instalados, selecione o nó do **SQL Server**.  
  
4.  No painel de detalhes, clique em **Projeto de Banco de Dados do SQL Server**.  
  
5.  Na caixa de texto **Nome**, digite **SampleConditionDB** e clique em **OK**.  
  
Em seguida, precisamos criar um teste de unidade. Para criar um teste de unidade do SQL Server em uma nova classe de teste:  
  
1.  No menu **Teste**, clique em **Novo Teste** para exibir a caixa de diálogo **Adicionar Novo Teste**.  
  
    Você também pode abrir o **Gerenciador de Soluções**, clicar com o botão direito do mouse em um projeto de teste, apontar para **Adicionar** e clicar em **Novo Teste**.  
  
2.  Na lista de modelos, clique em **Teste de Unidade do SQL Server**.  
  
3.  Em **Nome do Teste**, digite **SampleUnitTest**.  
  
4.  Em **Adicionar ao Projeto de Teste**, clique em **Criar um novo projeto de teste do Visual C\#**. Em seguida, clique em **OK** para exibir a caixa de diálogo **Novo Projeto de Teste**.  
  
5.  Digite **SampleUnitTest** para o nome do projeto.  
  
6.  Clique em **Cancelar** para criar o teste de unidade sem configurar o projeto de teste para usar uma conexão de banco de dados. O teste em branco aparece no Designer de Teste de Unidade do SQL Server. Um arquivo do código-fonte do Visual C\# é adicionado ao projeto de teste.  
  
    Para saber mais sobre como criar e configurar testes de unidade de banco de dados com conexões de banco de dados, consulte [Como criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md).  
  
7.  Clique em **Clique aqui para criar** para concluir a criação do teste de unidade. Você verá a nova condição de teste exibia no projeto do SQL Server.  
  
> [!NOTE]  
> Para usar sua nova condição de teste personalizada com projetos de teste de unidade existentes, pelo menos uma nova classe de teste de unidade do SQL Server deve ser criada. A referência necessária para seu assembly de condição de teste é adicionada ao seu projeto de teste durante a criação da classe de teste.  
  
Para exibir a nova condição de teste:  
  
1.  No **Designer de Teste de Unidade do SQL Server**, em **Condições de Teste**, na coluna **Nome**, clique no teste inconclusiveCondition1.  
  
2.  Clique no botão da barra de ferramentas **Excluir Condição de Teste** para remover o teste inconclusiveCondition1.  
  
3.  Clique no menu suspenso **Condições de Teste** e selecione **Contagem da Coluna ResultSet**.  
  
4.  Clique no botão da barra de ferramentas **Adicionar Condição de Teste** para adicionar sua condição de teste personalizada.  
  
5.  Na janela **Propriedades**, configure as propriedades Count, Enabled e ResultSet.  
  
    Para saber mais, confira [Como adicionar condições de teste a testes de unidade do SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Consulte Também  
[Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
