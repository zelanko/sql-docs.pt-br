---
title: Criar condições de teste para o designer de teste de unidade do SQL Server
description: Veja como estender a classe TestCondition para criar uma condição de teste personalizada para o designer de teste de unidade do SQL Server. Veja um exemplo de uma condição de teste personalizada.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 48076062-1ef5-419a-8a55-3c7b4234cc35
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: e34ca98e6a6a9423bd0237c980e15b91fcdd9aa6
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85518886"
---
# <a name="how-to-create-test-conditions-for-the-sql-server-unit-test-designer"></a>Como fazer: Criar condições de teste para o designer de teste de unidade do SQL Server

Você pode usar a classe extensível [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) para criar novas condições de teste. Por exemplo, você pode criar uma nova condição de teste que verifica o número de colunas ou os valores em um conjunto de resultados.  
  
## <a name="to-create-a-test-condition"></a>Para criar uma condição de teste  
Este procedimento explica como criar uma condição de teste para aparecer no Designer de Teste de Unidade do SQL Server.  
  
1.  No Visual Studio, crie um projeto de biblioteca de classes.  
  
2.  No menu **Projeto**, clique em **Adicionar Referência**.  
  
3.  Clique na guia **.NET**.  
  
4.  Na lista **Nome do Componente**, selecione **System.ComponentModel.Composition** e clique em **OK**.  
  
5.  Adicione as referências de assembly necessárias. Clique com o botão direito do mouse no nó do projeto e clique em **Adicionar Referência**. Clique em **Procurar** e navegue até a pasta C:\Arquivos de Programas (x86)\\Microsoft SQL Server\110\DAC\Bin. Escolha Microsoft.Data.Tools.Schema.Sql.dll, clique em Adicionar e depois em OK.  
  
6.  No menu **Projeto**, clique em **Descarregar Projeto**.  
  
7.  Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolha **Editar <project name>.csproj**.  
  
8.  Adicione as seguintes Instruções Import depois da importação de Microsoft.CSharp.targets:  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. Salve o arquivo e feche-o. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e escolha **Recarregar Projeto**.  
  
10. Derive sua classe da classe [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx).  
  
11. Assine o assembly com um nome forte. Para obter mais informações, confira [Como assinar um assembly com um nome forte](https://msdn.microsoft.com/library/xc31ft41.aspx).  
  
12. Crie a biblioteca de classes.  
  
13. Antes de usar a nova condição de teste, você deverá copiar seu assembly assinado para o diretório de saída para a pasta %Arquivos de Programas%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions. Se esta pasta não existir, crie-a. Você precisa de privilégios administrativos em seu computador para copiar para este diretório.  
  
14. Instalar a condição de teste. Para saber mais, confira [Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md).  
  
15. Adicione um novo teste de unidade do SQL Server para o projeto para criar uma referência para que a condição de teste seja adicionada ao projeto. Você pode adicionar manualmente uma referência ao assembly de condição de teste no projeto. Recarregue o designer após essa etapa.  
  
    > [!NOTE]  
    > Uma classe de teste deve ser adicionada para criar a referência. Você pode excluir a classe de teste depois que a referência for adicionada.  
  
No exemplo a seguir, você cria uma condição de teste simples que verifica o número de colunas retornadas no ResultSet. Você pode usar esta condição de teste simples para verificar se o contrato para um procedimento armazenado está correto:  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace Ssdt.Samples.SqlUnitTesting  
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
  
        // method you need to override  
        // to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            // call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            // verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            // verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            // actual condition verification  
            // verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        // this method is called to provide the string shown in the  
        // test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        // below are the test condition properties  
        // that are exposed to the user in the property browser  
        #region Properties  
  
        // property specifying the resultset for which  
        // you want to check the column count  
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
  
        // property specifying  
        // expected column count  
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
  
A classe para a condição de teste personalizada herda da classe base [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx). Devido às propriedades adicionais na condição de teste personalizada, os usuários podem configurar a condição na janela Propriedades depois de terem instalado a condição.  
  
[ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx) deve ser adicionada às classes que estendem [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx). Este atributo permite que a classe seja descoberta pelo SQL Server Data Tools e usada durante o design e a execução de teste de unidade. O atributo utiliza dois parâmetros:  
  
|Parâmetro de Atributos|Posição|Descrição|  
|-----------------------|------------|---------------|  
|DisplayName|1|Identifica a cadeia de conexão na caixa de combinação "Condições de Teste". Esse nome deve ser exclusivo. Se duas condições tiverem o mesmo nome para exibição, a primeira condição encontrada será mostrada para o usuário e um aviso será mostrado no Gerenciador de Erros do Visual Studio.|  
|ImplementingType|2|É usado para identificar exclusivamente a extensão. Você precisa alterar isso para corresponder ao tipo no qual você está colocando o atributo. Este exemplo usa o tipo **ResultSetColumnCountCondition**, portanto use **typeof(ResultSetColumnCountCondition)** . Se seu tipo for **NewTestCondition**, use **typeof(NewTestCondition)** .|  
  
Neste exemplo, você adiciona duas propriedades. Os usuários da condição de teste personalizada podem usar a propriedade ResultSet para especificar para qual conjunto de resultados a contagem de coluna deve ser verificada. Em seguida, é possível usar a propriedade Count para especificar a contagem de coluna esperada.  
  
Três atributos são adicionados para cada propriedade:  
  
-   O nome da categoria, que ajuda a organizar as propriedades.  
  
-   O nome para exibição da propriedade.  
  
-   A descrição da propriedade.  
  
A validação é realizada nas propriedades, para verificar se o valor da propriedade ResultSet não é menor que um e se o valor da propriedade Count é maior que zero.  
  
O método Assert realiza a tarefa primária da condição de teste. Você substitui o método Assert para validar se a condição esperada foi atendida. Este método fornece dois parâmetros:  
  
-   O primeiro parâmetro é a conexão de banco de dados que é usada para validar a condição de teste.  
  
-   O segundo e mais importante parâmetro é a matriz de resultados, que retorna um único elemento de matriz para cada lote que foi executado.  
  
Somente um único lote tem suporte para cada script de teste. Portanto, as condições de teste sempre examinarão o primeiro elemento da matriz. O elemento da matriz contém um Conjunto de Dados que, por sua vez, contém os conjuntos de resultados retornados para o script de teste. Neste exemplo, o código verifica se a tabela de dados no Conjunto de Dados contém o número de colunas apropriado. Para obter mais informações, consulte Conjunto de Dados.  
  
Você deve definir a biblioteca de classes que contém sua condição de teste a ser assinada, que você pode fazer nas propriedades do projeto na guia Assinatura.  
  
## <a name="see-also"></a>Consulte Também  
[Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
