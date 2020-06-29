---
title: Determinar se os dados de alterações estão prontos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],determining readiness
ms.assetid: 04935f35-96cc-4d70-a250-0fd326f8daff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a6035aa3af7dbb55ee4f3b948806d9dc63626e13
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438753"
---
# <a name="determine-whether-the-change-data-is-ready"></a>Determinar se os dados de alteração estão prontos
  No fluxo de controle de um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza uma carga incremental de dados de alteração, a segunda tarefa serve para garantir que os dados de alteração para o intervalo selecionado estejam prontos. Esta etapa é necessária, pois o processo de captura assíncrono pode ainda não ter processado todas as alterações até o ponto de extremidade selecionado.  
  
> [!NOTE]  
>  A primeira tarefa para o fluxo de controle é calcular os pontos de extremidade do intervalo de alteração. Para obter mais informações sobre essa tarefa, consulte [Especificar um intervalo de dados de alteração](specify-an-interval-of-change-data.md). Para obter uma descrição do processo geral de criação do fluxo de controle, consulte [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="understanding-the-components-of-the-solution"></a>Compreendendo os componentes da solução  
 A solução descrita neste tópico usa quatro componentes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
-   Um contêiner do Loop For que avalia repetidamente a saída de uma Tarefa Executar SQL.  
  
-   Uma tarefa Executar SQL que consulta tabelas especiais mantidas pelo processo de captura dos dados de alteração e usa essas informações para determinar se os dados estão prontos ou não.  
  
-   Um componente que implementa um atraso no processamento quando os dados não estão prontos. Pode ser uma tarefa Script ou uma tarefa Executar SQL.  
  
-   Como opção, um componente que reporta um erro ou um tempo limite excedido quando a tarefa Executar SQL retorna um valor indicando um erro ou uma condição de tempo limite excedido.  
  
 Esses componentes definem ou leem os valores de diversas variáveis de pacote para controlar o fluxo de execução dentro do loop e posteriormente no pacote.  
  
#### <a name="to-set-up-package-variables"></a>Para definir as variáveis do pacote  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na janela **Variáveis** , crie as seguintes variáveis:  
  
    1.  Crie uma variável com um tipo de dados inteiros para manter o valor de status retornado pela tarefa Executar SQL.  
  
         Este exemplo usa o nome da variável, DataReady, com um valor inicial de 0.  
  
    2.  Crie uma variável para segurar o período de tempo para atrasar quando os dados não estiverem prontos. Se você planeja usar uma tarefa Script para implementar o atraso, a variável deverá ter um tipo de dados inteiros. Se você planeja usar uma tarefa Executar SQL com uma instrução WAITFOR, a variável deverá ter um tipo de dados de cadeia de caracteres para aceitar valores como "00:00:10".  
  
         Este exemplo usa o nome da variável, DelaySeconds, com um valor inicial de 10.  
  
    3.  Crie uma variável com um tipo de dados inteiros para segurar a iteração atual do loop.  
  
         Este exemplo usa o nome da variável, TimeoutCount, com um valor inicial de 0.  
  
    4.  Crie uma variável com um tipo de dados inteiros, para especificar o número de vezes que o loop deve testar os dados antes de reportar uma condição de tempo limite excedido.  
  
         Este exemplo usa o nome da variável, TimeoutCeiling, com um valor inicial de 20.  
  
    5.  (Opcional) Crie uma variável com um tipo de dados inteiros que possa ser usada para indicar a primeira carga de dados de alteração.  
  
         Este exemplo usa o nome da variável, IntervalID, e verifica apenas a existência de um valor 0 para indicar a carga inicial.  
  
## <a name="configuring-a-for-loop-container"></a>Configurando um contêiner Loop For  
 Com as variáveis definidas, o contêiner Loop For é o primeiro componente em ser adicionado.  
  
#### <a name="to-configure-a-for-loop-container-to-wait-until-change-data-is-ready"></a>Para configurar um contêiner Loop For espere até que dados de alteração estejam prontos  
  
1.  Na guia **Fluxo de Controle** do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , adicione um contêiner Loop For ao fluxo de controle.  
  
2.  Conecte a tarefa Executar SQL que calcula os pontos de extremidade do intervalo para o contêiner Loop For.  
  
3.  No **Editor do Loop For**, selecione as seguintes opções:  
  
    1.  Para **InitExpression**, digite `@DataReady = 0`.  
  
         Esta expressão define o valor inicial da variável de loop.  
  
    2.  Para **EvalExpression**m, digite `@DataReady == 0`.  
  
         Quando esta expressão avaliar como **False**, a execução passará pelo loop e a carga incremental será iniciada.  
  
## <a name="configuring-the-execute-sql-task-that-queries-for-change-data"></a>Configurando a tarefa Executar SQL que consulta a existência de dados de alteração  
 Dentro do contêiner Loop For, você adiciona uma tarefa Executar SQL. Esta tarefa consulta as tabelas que o processo de captura de dados de alteração mantém no banco de dados. O resultado desta consulta é um valor de status que indica se os dados de alteração estão prontos ou não.  
  
 Na seguinte tabela, a primeira coluna mostra os valores retornados da tarefa Executar SQL pela consulta Transact-SQL. A segunda coluna mostra como os outros componentes respondem a estes valores.  
  
|Valor retornado|Significado|Resposta|  
|------------------|-------------|--------------|  
|0|Indica que os dados de alteração não estão prontos.<br /><br /> Não há nenhum registro de captura de dados de alteração posterior ao ponto final do intervalo selecionado.|A execução continua com o componente que implementa um atraso. Em seguida, o controle retorna para o contêiner Loop For, que continua a verificar a tarefa Executar SQL contanto que o valor retornado seja 0.|  
|1|Pode indicar que os dados de alteração não foram capturados para o intervalo completo ou que foram excluídos. Isso é tratado como uma condição de erro.<br /><br /> Não há nenhum registro de captura de dados de alteração anterior ao ponto inicial do intervalo selecionado|A execução continua com o componente opcional que armazena o erro.|  
|2|Indica que os dados estão prontos.<br /><br /> Não há nenhum registro de captura de dados de alteração anterior ao ponto inicial ou posterior ao ponto final do intervalo selecionado.|A execução passa pelo contêiner Loop For e a carga incremental é iniciada.|  
|3|Indica a carga inicial de todos os dados de alteração disponíveis.<br /><br /> A lógica condicional obtém este valor de uma variável de pacote especial usada apenas para este propósito.|A execução passa pelo contêiner Loop For e a carga incremental é iniciada.|  
|5|Indica que o TimeoutCeiling foi alcançado.<br /><br /> O loop realizou um teste para obter os dados do número de vezes especificado e os dados ainda não estão disponíveis. Sem este teste ou um teste semelhante, o pacote pode ser executado indefinidamente.|A execução continua com o componente opcional que armazena o tempo limite excedido.|  
  
#### <a name="to-configure-an-execute-sql-task-to-query-whether-change-data-is-ready"></a>Para configurar uma tarefa Executar SQL para consultar se os dados de alteração estão prontos  
  
1.  Dentro do contêiner Loop For, adicione uma tarefa Executar SQL.  
  
2.  No **Editor da Tarefa Executar SQL**, na página **Geral** , selecione as seguintes opções:  
  
    1.  Para **Conjunto de Resultados**, selecione **Linha simples**.  
  
    2.  Configure uma conexão válida com o banco de dados fonte.  
  
    3.  Para **SQLSourceType**, selecione **Entrada direta**.  
  
    4.  Para **SQLStatement**, digite a seguinte instrução SQL:  
  
        ```  
        declare @DataReady int, @TimeoutCount int  
  
        if not exists (select tran_end_time from cdc.lsn_time_mapping  
                where tran_end_time > ?  )  
            select @DataReady = 0  
        else  
            if ? = 0  
                select @DataReady = 3   
        else  
            if not exists (select tran_end_time from cdc.lsn_time_mapping  
                    where tran_end_time <= ? )  
                select @DataReady = 1   
        else  
            select @DataReady = 2  
  
        select @TimeoutCount = ?  
        if (@DataReady = 0)  
            select @TimeoutCount = @TimeoutCount + 1  
        else  
            select @TimeoutCount = 0  
  
        if (@TimeoutCount > ?)  
            select @DataReady = 5  
  
        select @DataReady as DataReady, @TimeoutCount as TimeoutCount  
  
        ```  
  
3.  Na página **Mapeamentos de Parâmetros** do **Editor da Tarefa Executar SQL**, faça os seguintes mapeamentos:  
  
    1.  Mapeie a variável ExtractEndTime para o parâmetro 0.  
  
    2.  Mapeie a variável IntervalID para o parâmetro 1.  
  
    3.  Mapeie a variável ExtractStartTime para o parâmetro 2.  
  
    4.  Mapeie a variável TimeoutCount para o parâmetro 3.  
  
    5.  Mapeie a variável TimeoutCeiling para o parâmetro 4.  
  
4.  Na página **Conjunto de Resultados** do **Editor da tarefa Executar SQL**, mapeie o resultado de DataReady para a variável DataReady e o resultado de TimeoutCount para a variável TimeoutCount.  
  
## <a name="waiting-until-the-change-data-is-ready"></a>Esperando até que os dados de alteração estejam prontos  
 É possível usar um dos diversos métodos para implementar um atraso quando os dados de alteração não estiverem prontos. Os dois procedimentos a seguir ilustram como usar uma tarefa Script ou uma tarefa Executar SQL para implementar o atraso.  
  
> [!NOTE]  
>  Um script pré-compilado causa menos sobrecarga do que uma tarefa Executar SQL.  
  
#### <a name="to-implement-a-delay-by-using-a-script-task"></a>Para implementar um atraso usando uma tarefa Script  
  
1.  Dentro do contêiner Loop For, adicione uma tarefa Script.  
  
2.  Conecte a tarefa Executar SQL que realiza a consulta para determinar se os dados de alteração estão prontos para a nova tarefa Script.  
  
3.  Para a restrição de precedência que conecta a tarefa Executar SQL à tarefa Script, abra o **Editor de Restrição de Precedência** e selecione as seguintes opções:  
  
    1.  Para **Operação de avaliação**, selecione **Expressão e Restrição**.  
  
    2.  Para **Valor**, selecione **Êxito**.  
  
         O valor de restrição de **Êxito** se refere ao sucesso da tarefa anterior. Neste caso, o sucesso da tarefa Executar SQL.  
  
    3.  Para **Expressão**, digite `@DataReady == 0 && @TimeoutCount <= @TimeoutCeiling`.  
  
    4.  Selecione **E Lógico. Todas as restrições deverão avaliar como True**, se ainda não estiver selecionado.  
  
4.  Em **Editor da Tarefa Script**, na página **Script** , para **ReadOnlyVariables**, selecione a variável de número inteiro **User::DelaySeconds** da lista.  
  
5.  No **Editor da Tarefa Script**, na página **Script** , clique em **Editar Script** para abrir o ambiente de desenvolvimento de script.  
  
6.  No procedimento Principal, digite uma das seguintes linhas de código:  
  
    -   Se você estiver programando em C#, digite a seguinte linha de código:  
  
        ```  
        System.Threading.Thread.Sleep((int)Dts.Variables["DelaySeconds"].Value * 1000);  
        ```  
  
         \- ou –  
  
    -   Se você estiver programando em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], digite a seguinte linha de código:  
  
        ```  
        System.Threading.Thread.Sleep(Ctype(Dts.Variables("DelaySeconds").Value, Integer) * 1000)  
  
        ```  
  
        > [!NOTE]  
        >  O método `Thread.Sleep` espera um argumento especificado em milissegundos.  
  
7.  Tire a linha padrão de código que retorna `DtsExecResult.Success` da execução do script.  
  
8.  Feche o ambiente de desenvolvimento de script e o **Editor da Tarefa Script**.  
  
#### <a name="to-implement-a-delay-by-using-an-execute-sql-task"></a>Para implementar um atraso usando uma tarefa Executar SQL  
  
1.  Dentro do contêiner Loop For, adicione uma tarefa Executar SQL.  
  
2.  Conecte a tarefa Executar SQL que realiza a consulta para determinar se os dados de alteração estão prontos para a nova tarefa Executar SQL.  
  
3.  Para a restrição de precedência que conecta as duas tarefas Executar SQL, abra o **Editor de Restrição de Precedência** e selecione as seguintes opções:  
  
    1.  Para **Operação de avaliação**, selecione **Expressão e Restrição**.  
  
    2.  Para **Valor**, selecione **Êxito**.  
  
         O valor de restrição de **Êxito** se refere ao êxito da tarefa Executar SQL anterior.  
  
    3.  Para **Expressão**, digite `@DataReady == 0`.  
  
    4.  Selecione **E Lógico. Todas as restrições deverão avaliar como True**, se ainda não estiver selecionado.  
  
         Esta seleção requer que ambas as condições, a restrição e a expressão, sejam verdadeiras.  
  
4.  No **Editor da Tarefa Executar SQL**, na página **Geral** , selecione as seguintes opções:  
  
    1.  Para **Conjunto de Resultados**, selecione **Linha simples**.  
  
    2.  Configure uma conexão válida com o banco de dados fonte.  
  
    3.  Para **SQLSourceType**, selecione **Entrada direta**.  
  
    4.  Para **SQLStatement**, digite a seguinte instrução SQL:  
  
        ```  
        WAITFOR DELAY ?  
  
        ```  
  
5.  Na página **Mapeamento de Parâmetro** do editor, mapeie a variável de cadeia de caracteres DelaySeconds para o parâmetro 0.  
  
## <a name="handling-an-error-condition"></a>Controlando uma condição de erro  
 Como opção, é possível configurar um componente adicional dentro do loop para armazenar um erro ou uma condição de tempo limite excedido:  
  
-   Este componente pode armazenar uma condição de erro quando o valor da variável DataReady for = 1. Este valor indica que não há dados de alteração disponíveis antes do início do intervalo selecionado.  
  
-   Este componente também pode armazenar uma condição de tempo limite excedido quando o valor da variável TimeoutCeiling é alcançado. Este valor indica que o loop realizou um teste para obter os dados do número de vezes especificado e os dados ainda não estão disponíveis. Sem este teste ou um teste semelhante, o pacote pode ser executado indefinidamente.  
  
#### <a name="to-configure-an-optional-script-task-to-log-an-error-condition"></a>Para configurar uma tarefa Script opcional para armazenar uma condição de erro  
  
1.  Se quiser reportar o erro ou o tempo limite excedido gravando uma mensagem no log, configure o armazenamento em log para o pacote. Para obter mais informações, consulte [Habilitar o log de pacote no SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md).  
  
2.  Dentro do contêiner Loop For, adicione uma tarefa Script.  
  
3.  Conecte a tarefa Executar SQL que realiza a consulta para determinar se os dados de alteração estão prontos para a nova tarefa Script.  
  
4.  Para a restrição de precedência que conecta a tarefa Executar SQL à tarefa Script, abra o **Editor de Restrição de Precedência** e selecione as seguintes opções:  
  
    1.  Para **Operação de avaliação**, selecione **Expressão e Restrição**.  
  
    2.  Para **Valor**, selecione **Êxito**.  
  
         O valor de restrição de **Êxito** se refere ao sucesso da tarefa anterior. Neste caso, o sucesso da tarefa Executar SQL.  
  
    3.  Para **Expressão**, digite `@DataReady == 1 || @DataReady == 5`.  
  
    4.  Selecione **E Lógico. Todas as restrições deverão avaliar como True**, se ainda não estiver selecionado.  
  
         Esta seleção requer que ambas as condições, a restrição e a expressão, sejam verdadeiras.  
  
5.  No **Editor da Tarefa Script**, na página **Script** do editor, para **ReadOnlyVariables**, selecione **User::DataReady** e **User::ExtractStartTime** da lista para disponibilizar seus valores para o script.  
  
     Se você quiser incluir informações de determinadas variáveis do sistema (por exemplo, System::PackageName) nas informações gravadas no log, selecione também as variáveis.  
  
6.  No **Editor da Tarefa Script**, na página **Script** , clique em **Editar Script** para abrir o ambiente de desenvolvimento de script.  
  
7.  No procedimento Principal, digite o código para armazenar um erro chamando o método `Dts.Log` ou acione um evento chamando um dos métodos da interface `Dts.Events`. Informe o pacote do erro retornando `Dts.TaskResult = Dts.Results.Failure`.  
  
     A seguinte amostra mostra como gravar uma mensagem no log. Para obter mais informações, consulte [Registrando a tarefa Script](../extending-packages-scripting/task/logging-in-the-script-task.md), [Gerando eventos na tarefa Script](../extending-packages-scripting/task/raising-events-in-the-script-task.md)e [Retornando resultados da tarefa Script](../extending-packages-scripting/task/returning-results-from-the-script-task.md).  
  
    ```  
    ' User variables.  
    Dim dataReady As Integer = _  
      CType(Dts.Variables("DataReady").Value, Integer)  
    Dim extractStartTime As Date = _  
      CType(Dts.Variables("ExtractStartTime").Value, DateTime)  
  
    ' System variables.  
    Dim packageName As String = _  
      Dts.Variables("PackageName").Value.ToString()  
    Dim executionStartTime As Date = _  
      CType(Dts.Variables("StartTime").Value, DateTime)  
  
    Dim eventMessage As New System.Text.StringBuilder()  
  
    If dataReady = 1 OrElse dataReady = 5 Then  
  
      If dataReady = 1 Then  
        eventMessage.AppendLine("Start Time Error")  
      Else  
        eventMessage.AppendLine("Timeout Error")  
      End If  
  
      With eventMessage  
        .Append("The package ")  
        .Append(packageName)  
        .Append(" started at ")  
        .Append(executionStartTime.ToString())  
        .Append(" and ended at ")  
        .AppendLine(DateTime.Now().ToString())  
        If dataReady = 1 Then  
          .Append("The specified ExtractStartTime was ")  
          .AppendLine(extractStartTime.ToString())  
        End If  
      End With  
  
      System.Windows.Forms.MessageBox.Show(eventMessage.ToString())  
  
      Dts.Log(eventMessage.ToString(), 0, Nothing)  
  
      Dts.TaskResult = Dts.Results.Failure  
  
    Else  
  
      Dts.TaskResult = Dts.Results.Success  
  
    End If  
  
    ```  
  
8.  Feche o ambiente de desenvolvimento de script e o **Editor da Tarefa Script**.  
  
## <a name="next-step"></a>Próxima etapa  
 Após determinar que os dados de alteração estão prontos, a próxima etapa será preparar para consultar os dados de alteração.  
  
 **Próximo tópico:** [Preparar para consultar os dados de alterações](prepare-to-query-for-the-change-data.md)  
  
  
