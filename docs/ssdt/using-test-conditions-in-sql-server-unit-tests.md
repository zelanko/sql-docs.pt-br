---
title: Usar condições de teste nos testes de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconditions
ms.assetid: e3d1c86c-1e58-4d2c-b625-d1b591b221aa
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 923c6fc93418cf2e46bf3970632ae0454f5a611d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101889"
---
# <a name="using-test-conditions-in-sql-server-unit-tests"></a>Usando condições de teste nos testes de unidade do SQL Server
Em um teste de unidade do SQL Server, um ou mais scripts de teste Transact\-SQL são executados. Os resultados podem ser avaliados dentro do script Transact\-SQL e THROW ou RAISERROR podem ser usados para retornar um erro e falha do teste, ou as condições de teste podem ser definidas no teste para avaliar os resultados. O teste retorna uma instância da classe [SqlExecutionResult](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.sqlexecutionresult.aspx). A instância dessa classe contém um ou mais Conjunto de Dados, o tempo de execução e as linhas afetadas pelo script. Todas essas informações são coletadas durante a execução do script. Esses resultados podem ser avaliados usando condições de teste. O SQL Server Data Tools fornece um conjunto de condições de teste predefinidos. Você também pode criar e usar condições personalizadas; confira [Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md).  
  
## <a name="predefined-test-conditions"></a>Condições de teste predefinidas  
A tabela a seguir lista as condições de teste predefinidas que você pode adicionar usando o painel Condições de Teste no Designer de Teste de Unidade do SQL Server.  
  
|**Condição de teste**|**Descrição da condição de teste**|  
|----------------------|----------------------------------|  
|Soma de verificação dos dados|Apresentará falha se a soma de verificação do conjunto de resultados retornado pelo script Transact\-SQL não corresponder à soma de verificação esperada. Para obter mais informações, consulte [Especificando uma soma de verificação de dados](#SpecifyDataChecksum).<br /><br />**OBSERVAÇÃO:** Essa condição de teste não será recomendada se você estiver retornando dados que variarão entre as execuções de teste. Por exemplo, se o conjunto de resultados contiver as datas ou horas da geração, ou contiver colunas de identidade, os testes apresentarão falha porque a soma de verificação será diferente em cada execução.|  
|ResultSet Vazio|Apresentará falha se o conjunto de resultados retornado pelo script Transact\-SQL não estiver vazio.|  
|Tempo de execução|Apresentará falha se o script de teste Transact\-SQL levar muito mais tempo do que o esperado para ser executado. O tempo de execução padrão é 30 segundos.<br /><br />O tempo de execução se aplica somente ao teste do script de teste, e não ao script de pré-teste ou pós-teste.|  
|Esquema esperado|Apresentará falha se as colunas e os tipos de dados do conjunto de resultados não corresponderem aos especificados para a condição de teste. Você deve especificar um esquema através das propriedades da condição de teste. Para obter mais informações, consulte [Especificando um esquema esperado](#SpecifyExpectedSchema).|  
|Inconclusivo|Sempre gera um teste com o resultado Inconclusivo. Essa é a condição padrão adicionada a cada teste. Ela é incluída para indicar que a verificação de teste não foi implementada. Exclua essa condição do teste depois que você tiver adicionado outras condições.|  
|ResultSet Não Vazio|Apresentará falha se o conjunto de resultados estiver vazio. Você pode usar essa condição de teste ou EmptyResultSet com a função Transact\-SQL @@RAISERROR no script de teste para verificar se uma atualização funcionou corretamente. Por exemplo, você pode salvar valores de pré-atualização, executar a atualização, comparar valores de pós-atualização e emitir um erro se você não obtiver os resultados esperados.|  
|Contagem de Linhas|Apresentará falha se o conjunto de resultados não contiver o número de linhas esperado.|  
|Valor escalar|Apresentará falha se um valor no conjunto de resultados não for igual ao valor especificado. O **Valor esperado** padrão é nulo.|  
  
> [!NOTE]  
> A condição de teste Tempo de Execução especifica um limite de tempo no qual o script de teste Transact\-SQL deve ser executado. Se esse tempo limite for excedido, o teste falhará. Os resultados do teste também incluem uma estatística de duração, que é diferente da condição de teste Tempo de Execução. A estatística de duração inclui não somente o tempo de execução, mas também o tempo de conexão ao banco de dados multiplicado por dois; o tempo de execução de quaisquer outro scripts de teste, como o script de pré-teste e o script de pós-teste; e o tempo de execução das condições de teste. Portanto, um teste pode passar até mesmo se sua duração for maior do que o tempo de execução.  
>   
> A duração informada não inclui o tempo usado para a geração de dados e a implantação do esquema porque eles ocorrem antes que os testes sejam executados. Para exibir a duração do teste, selecione um execução do teste na janela **Resultados de Teste**, clique com o botão direito do mouse e escolha **Exibir Detalhes dos Resultados de Teste**.  
  
Você pode adicionar condições aos testes de unidade do SQL Server usando o painel Condições do Teste do Designer de Teste de Unidade do SQL Server. Para obter mais informações, confira [Como Adicionar condições de teste a testes de unidade do SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
Você também pode editar o código do método de teste diretamente para adicionar mais funcionalidade. Para obter mais informações, confira [Como abrir um teste de unidade do SQL Server a ser editado](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md) e [Como: Gravar um teste de unidade do SQL Server executado no escopo de uma única transação](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md). Por exemplo, você pode adicionar funcionalidade a um método de teste adicionando instruções de asserção. Para saber mais, confira [Usar asserções Transact-SQL em testes de unidade do SQL Server](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md).  
  
## <a name="expected-failures"></a>Falhas esperadas  
Você pode criar testes de unidade do SQL Server para testar o comportamento que não deve ter êxito. Essas falhas esperadas às vezes são chamadas de testes negativos. Alguns exemplos incluem:  
  
-   Verifique se um procedimento armazenado que exclui os dados de um cliente apresentará falha se você especificar uma ID de cliente inválida.  
  
-   Verifique se um procedimento armazenado que preenche um pedido apresentará falha caso o pedido nunca tenha sido inserido ou já tenha sido preenchido.  
  
-   Verifique se um procedimento armazenado que cancela um pedido não pode cancelar os pedidos concluídos ou os pedidos já cancelados.  
  
Você pode definir testes de unidade do SQL Server para procedimentos armazenados que lançam exceções esperadas. Você pode adicionar um atributo ao método de teste de unidade para indicar quais exceções são esperadas. Fazendo isso, você impedirá que o teste falhe quando a exceção ocorrer.  
  
Para marcar um método de teste de unidade do SQL Server com as exceções esperadas, adicione o seguinte atributo:  
  
```  
[ExpectedSqlException(MessageNumber = nnnnn, Severity = x, MatchFirstError = false, State = y)]  
```  
  
Onde:  
  
-   *nnnnn* é o número da mensagem esperada; por exemplo, 14025  
  
-   *x* é o nível de severidade da exceção esperada  
  
-   *y* é o estado da exceção esperada  
  
Todos os parâmetros não especificados são ignorados. Você passa esses parâmetros para a instrução **THROW** no código do banco de dados. Se você especificar MatchFirstError = false, o atributo corresponderá a qualquer SqlError na exceção. O comportamento padrão (MatchFirstError = true) é retornar somente o primeiro erro.  
  
Para obter um exemplo de como usar as exceções esperadas e um teste de unidade negativo do SQL Server, veja [Passo a passo: Criar e Executar um Teste de Unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md).  
  
## <a name="SpecifyDataChecksum"></a>Especificar uma soma de verificação de dados  
Para exibir o Designer do Teste de Unidade do SQL Server, clique duas vezes no arquivo do código de origem do teste de unidade no **Gerenciador de Soluções**.  
  
Depois que você adicionar a condição de teste Soma de Verificação de Dados no teste de unidade de banco de dados, configure a soma de verificação esperada usando o procedimento a seguir:  
  
#### <a name="to-specify-an-expected-checksum"></a>Para especificar uma soma de verificação esperada  
  
1.  Na lista de condições de teste, clique na condição de teste Soma de Verificação de Dados para a qual você deseja especificar uma soma de verificação.  
  
2.  Abra a janela **Propriedades** pressionando F4. Você também pode abrir o menu **Exibir** e clicar na janela **Propriedades** .  
  
3.  (Opcional) Talvez seja necessário alterar a propriedade **(Nome)** da condição de teste de modo que ela seja mais descritiva.  
  
4.  Na propriedade **Configuração**, clique no botão Procurar ( **…** ).  
  
    A caixa de diálogo **Configuração de TestConditionName** é exibida.  
  
5.  Especifique uma conexão com o banco de dados que você deseja testar. Para obter mais informações, confira [Como criar uma Conexão de Banco de Dados](https://msdn.microsoft.com/library/aa833420(VS.100).aspx).  
  
6.  Por padrão, o corpo de Transact\-SQL do teste é exibido no painel de edição. Você pode modificar o código, se necessário, para gerar os resultados esperados. Por exemplo, se o teste tiver código no pré-teste, talvez seja necessário adicionar esse código.  
  
    > [!IMPORTANT]  
    > Se você modificar uma condição de soma de verificação para a qual tinha especificado uma soma de verificação, as alterações feitas no painel de edição não serão salvas. Você deve fazer essas alterações novamente antes de clicar em **Recuperar**.  
  
7.  Clique em **Recuperar**.  
  
    O Transact\-SQL é executado na conexão de banco de dados especificada, e os resultados aparecem na caixa de diálogo.  
  
8.  Se os resultados corresponderem aos resultados esperados do teste, clique em **OK**. Caso contrário, não modifique o corpo de Transact\-SQL, e repita as etapas 6, 7 e 8 até que os resultados retornados sejam os esperados.  
  
    A coluna **Valor** da condição de teste exibe o valor da soma de verificação esperada.  
  
## <a name="SpecifyExpectedSchema"></a>Especificar um esquema esperado  
Depois que você adicionar a condição de teste Esquema Esperado ao teste de unidade do SQL Server, configure o esquema esperado usando o procedimento a seguir:  
  
#### <a name="to-specify-an-expected-schema"></a>Para especificar um esquema esperado  
  
1.  Na lista de condições de teste, clique na condição de teste Esquema Esperado para a qual você deseja especificar um esquema.  
  
2.  Abra a janela **Propriedades** pressionando F4. Você também pode abrir o menu **Exibir** e clicar na janela **Propriedades** .  
  
3.  (Opcional) Talvez seja necessário alterar a propriedade **(Nome)** da condição de teste de modo que ela seja mais descritiva.  
  
4.  Na propriedade **Configuração**, clique no botão Procurar ( **…** ).  
  
    A caixa de diálogo **Configuração de TestConditionName** é exibida.  
  
5.  Especifique uma conexão com o banco de dados que você deseja testar. Para obter mais informações, confira [Como criar uma Conexão de Banco de Dados](https://msdn.microsoft.com/library/aa833420(VS.100).aspx).  
  
6.  Por padrão, o corpo de Transact\-SQL do teste é exibido no painel de edição. Você pode modificar o código, se necessário, para gerar os resultados esperados. Por exemplo, se o teste tiver código no pré-teste, talvez seja necessário adicionar esse código.  
  
    > [!IMPORTANT]  
    > Se você modificar uma condição de esquema esperado para a qual tinha especificado um esquema, as alterações feitas no painel de edição não serão salvas. Você deve fazer essas alterações novamente antes de clicar em **Recuperar**.  
  
7.  Clique em **Recuperar**.  
  
    O Transact\-SQL é executado na conexão de banco de dados especificada, e os resultados aparecem na caixa de diálogo. Como você está verificando o esquema, ou a forma, do conjunto de resultados, e não os valores dos resultados, não é necessário consultar nenhum dado nos resultados retornados, contanto que as colunas apareçam da maneira esperada.  
  
8.  Se os resultados corresponderem aos resultados esperados do teste, clique em **OK**. Caso contrário, não modifique o corpo de Transact\-SQL, e repita as etapas 6, 7 e 8 até que os resultados retornados sejam os esperados.  
  
    A coluna **Valor** da condição de teste exibe informações sobre o esquema esperado. Por exemplo, ela poderia informar "Esperado: 2 tabelas."  
  
## <a name="extensible-test-conditions"></a>Condições de teste extensíveis  
Além das seis condições de teste predefinidas, você pode escrever novas condições de teste por sua própria conta. Essas condições serão exibidas no painel Condições de Teste do Designer de Teste de Unidade do SQL Server. Para saber mais, confira [Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Usar asserções Transact-SQL nos testes de unidade do SQL Server](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)  
[Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
