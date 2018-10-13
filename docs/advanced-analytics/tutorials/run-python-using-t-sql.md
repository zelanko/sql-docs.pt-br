---
title: Execute o Python usando o T-SQL | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7b4a6035996ce457cb2e58aef5d1c7498ad9f826
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878019"
---
# <a name="run-python-using-t-sql"></a>Executar Python usando T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tutorial explica como você pode executar o código do Python no SQL Server 2017. Ele orienta você durante o processo de mover dados entre o SQL Server e o Python e explica como empacotar o código do Python bem formado em um procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para criar, treinar e usar modelos de aprendizado de máquina no SQL Servidor.

## <a name="prerequisites"></a>Prerequisites

Para concluir este tutorial, você deve primeiro instalar o SQL Server 2017 e habilitar serviços de Machine Learning na instância, conforme descrito em [instalar o SQL Server 2017 serviços Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md). 

Você também deve instalar [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Como alternativa, você pode usar a ferramenta de outro de banco de dados gerenciamento ou consulta, desde que ele pode se conectar a um servidor e banco de dados e executar uma consulta T-SQL ou procedimento armazenado.

Depois de concluir a instalação, retorne a este tutorial, para aprender a executar código Python no contexto de um procedimento armazenado. 

## <a name="overview"></a>Visão geral

Este tutorial inclui quatro lições:

+ Os conceitos básicos de mover dados entre o SQL Server e o Python: saber os requisitos básicos, estruturas de dados, entradas e saídas.
+ Praticar usando procedimentos armazenados para tarefas simples de Python, como carregar dados de exemplo.
+ Use os procedimentos armazenados para criar uma modelo de aprendizado de máquina do Python e gerar pontuações do modelo.
+ Uma lição opcional para os usuários que pretende executar o Python em um cliente remoto, usando o SQL Server como o _contexto de computação_. Inclui o código para a criação de um modelo; No entanto, exige que você já está familiarizado com os ambientes do Python e ferramentas do Python.

Exemplos de Python adicionais específicos ao SQL Server 2017 são fornecidos aqui: [tutoriais do Python do SQL Server](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>Verifique se o Python está habilitado e a barra inicial está em execução

1. No Management Studio, execute esta instrução para verificar se que o serviço foi habilitado.

    ```sql
    sp_configure 'external scripts enabled'
    ```

    Se **run_value** é 1, o recurso de aprendizado de máquina é instalado e pronto para uso.

    Uma causa comum de erros é que a barra inicial, que gerencia a comunicação entre o SQL Server e o Python, foi interrompido. Você pode exibir o status da barra inicial, usando o Windows **Services** painel ou abrindo o SQL Server Configuration Manager. Se o serviço foi interrompido, reinicie-o.

2. Em seguida, verifique se que o tempo de execução do Python está funcionando e se comunicando com o SQL Server. Para fazer isso, abra uma nova **consulta** janela no SQL Server Management Studio e conecte-se à instância onde o Python foi instalado.

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    Se tudo estiver bem, você deverá ver uma mensagem de resultado como este

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. Se você obtiver erros, há uma variedade de coisas que você pode fazer para garantir que o servidor e o Python pode se comunicar. 

    Você deve adicionar o grupo de usuários do Windows `SQLRUserGroup` como um logon na instância, para garantir que o Launchpad poderá fornecer comunicação entre o Python e o SQL Server. (O mesmo grupo é usado para ambos os R e execução de código do Python.) Para obter mais informações, consulte [habilitado a autenticação implícita](../security/add-sqlrusergroup-to-database.md).
    
    Além disso, talvez você precise habilitar protocolos de rede que foram desabilitados ou abrir o firewall para que o SQL Server pode se comunicar com clientes externos. Para obter mais informações, consulte [Solucionando problemas de instalação](../common-issues-external-script-execution.md).

## <a name="basic-python-interaction"></a>Interação de Python básica

Há duas maneiras de executar código Python no SQL Server:

+ Adicionar um script Python como um argumento de procedimento armazenado do sistema, **sp_execute_external_script**
+ De um cliente remoto do Python, conecte-se ao SQL Server e executar o código usando o SQL Server como o contexto de computação. Isso exige [revoscalepy](../python/what-is-revoscalepy.md).

O objetivo principal deste tutorial é garantir que você pode usar o Python em um procedimento armazenado.

1. Execute alguns códigos simples para ver como os dados são passados bidirecionalmente entre o SQL Server e o Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Supondo que você tem tudo configurado corretamente, e o Python e o SQL Server estiverem falando uns aos outros, o resultado correto é calculado e o Python `print` função retorna o resultado para o **mensagens** windows.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    Ao obter **stdout** mensagens é útil ao testar seu código, mais geralmente, você precisa retornar os resultados em formato tabular, para que você possa usá-lo em um aplicativo ou escrevê-lo a uma tabela. 

Por enquanto, lembre-se estas regras:

+ Tudo dentro de `@script` argumento deve ser um código Python válido. 
+ O código deve seguir todas as regras Pythonic relativos a recuo, nomes de variáveis e assim por diante. Quando você receber um erro, verifique o espaço em branco e o uso de maiusculas.
+ Se você estiver usando todas as bibliotecas que não são carregadas por padrão, você deve usar uma instrução de importação no início do seu script para carregá-los. 
+ Se a biblioteca já não estiver instalada, parar e instalar o pacote do Python fora do SQL Server, conforme descrito aqui: [instalar novos pacotes de Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>Entradas e Saídas

Por padrão, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) aceita um único conjunto de dados entrado, que normalmente você fornece na forma de uma consulta SQL válida. Outros tipos de entrada podem ser passados como variáveis SQL: por exemplo, você pode passar um modelo treinado como uma variável, usando uma função de serialização, como [pickle](https://docs.python.org/3.0/library/pickle.html) ou [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para gravar o modelo um formato binário.

O procedimento armazenado retorna um único Python [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html) quadro de dados como saída. No entanto, é possível transmitir escalares e modelos como variáveis. Por exemplo, você pode gerar um modelo treinado como uma variável binária e passá-lo para uma instrução T-SQL INSERT, para gravar esse modelo em uma tabela. Você também pode gerar plotagens (em formato binário) ou escalares (valores individuais, como a data e hora, o tempo decorrido para treinar o modelo e assim por diante).

Por enquanto, vamos examinar apenas o padrão variáveis de entrada e saídas `InputDataSet` e `OutputDataSet`. 

1. Execute o seguinte código para fazer alguns cálculos e os resultados de saída.

        ```sql
        execute sp_execute_external_script 
        @language = N'Python', 
        @script = N'
        a = 1
        b = 2
        c = a/b
        print(c)
        OutputDataSet = c
        '
        WITH RESULT SETS ((ResultValue float))
        ```

2. Você deve receber um erro, porque o código Python gera um escalar, não um quadro de dados.

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. Agora, veja o que acontece quando você passa um conjunto de dados tabular para Python, usando a variável de entrada padrão `InputDataSet`. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    O procedimento armazenado retorna um Frame automaticamente, sem ter que fazer nada extra em seu código Python.

    **Resultados**

    | Não há columnname|
    |------|
    | 1|

    Por padrão, o conjunto de entradas de tabela único tem o nome, `InputDataSet`. No entanto, você pode alterar esse nome, adicionando uma linha como esta: `@input_data_1_name = N'myResultName'`.

    Nomes de coluna usados pelo Python nunca são preservados na saída. Embora a consulta de entrada especificado o nome da coluna `Col1`, esse nome não é retornado, nem seria quaisquer cabeçalhos de coluna usados pelo seu script de Python. Para especificar um tipo de dados e o nome de coluna quando você retornar os dados para o SQL Server, use o T-SQL `WITH RESULT SETS` cláusula.

4. Este exemplo fornece novos nomes para as variáveis de entrada e saídas.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    MyOutput = MyInput
    ',
    @input_data_1_name = N'MyInput',
    @input_data_1 = N'SELECT 1 as Col1',
    @output_data_1_name = N'MyOutput'
    WITH RESULT SETS ((ResultValue int))
    ```

    A cláusula com o conjunto de resultados define o esquema para a saída, já que os nomes de coluna de Python nunca são retornados com o Frame.

    **Resultados**

    | ResultValue|
    |------|
    | 1|

5. Agora vamos examinar um erro típico do Python. Altere a linha no exemplo anterior do `@input_data_1_name = N'MyInput'` para `@input_data_1_name = N'myinput'`.

    Erros de Python são passados para você como mensagens de, pelo serviço de satélite usado pelo SQL Server. As mensagens podem ser longos e erros do SQL Server ou erros de barra inicial, além de erros do Python, portanto, seja paciente em aprofundar-se pelo texto. A principal mensagem é nessa linha:

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    Lembre-se de que o Python, como R, diferencia maiusculas de minúsculas. Portanto, quando você receber qualquer tipo de erro, certifique-se verificar os nomes das variáveis e procurar problemas com espaçamento, recuo e tipos de dados.

## <a name="python-data-structures"></a>Estruturas de dados do Python

SQL Server depende do Python **pandas** pacote, que é ideal para trabalhar com dados tabulares. No entanto, você já viu que você não pode passar um escalar do Python para o SQL Server e esperar que ele "simplesmente funcionem". Nesta seção, vamos examinar algumas definições de tipo de dados básico, para se preparar para problemas adicionais que podem ocorrer ao passar dados tabulares entre Python e o SQL Server.

+ Um quadro de dados é uma tabela com _vários_ colunas.
+ Uma única coluna de um DataFrame, é um objeto de lista como chamado de uma série.
+ Um único valor é uma célula de um quadro de dados e deve ser chamado por índice.

Então, como você poderia expor o resultado de um cálculo como um quadro de dados, se um frame requer uma estrutura tabular? Uma resposta é representar o único valor escalar como uma série, o que é facilmente convertida em um quadro de dados. 

1. Este exemplo faz alguns cálculos matemáticos simples e converte um escalar em uma série. Uma série requer um índice, que você pode atribuir manualmente, conforme mostrado aqui, ou programaticamente.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. Como a série ainda não foi convertida em um Frame, os valores são retornados na janela de mensagens, mas você pode ver que os resultados estão em um formato tabular mais.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar o tamanho da série, você pode adicionar novos valores, usando uma matriz. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    Se você não especificar um índice, um índice é gerado que tenha valores começando com 0 e terminando com o comprimento da matriz.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Se você aumentar o número de **índice** valores, mas não adicionar novas **dados** valores, os valores de dados são repetidos para preencher a série.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    '
    ```

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    simple math example 2    0.5
    dtype: float64
    ```

### <a name="convert-series-to-data-frame"></a>Converter série ao quadro de dados

Ter convertido nossos resultados escalares matemática em uma estrutura tabular, ainda precisamos convertê-los em um formato que pode lidar com os do SQL Server. 

1. Para converter uma série em um Frame, chame os pandas [DataFrame](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) método.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s)
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

2. Observe que os valores de índice não são a saída, mesmo se você usar o índice para obter valores específicos do Frame.

    **Resultados**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>Valores de saída em Frame usando um índice

Vamos ver como a conversão para um Frame funciona com nossas duas séries que contém os resultados de operações matemáticas simples. O primeiro tem um índice de valores sequenciais gerados pelo Python. O segundo usa um índice arbitrário de valores de cadeia de caracteres.

1. Este exemplo obtém um valor da série que usa um índice de inteiro.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    Lembre-se de que o índice gerado automaticamente começa em 0. Tente usar uma valor fora do intervalo índice e ver o que acontece.

2. Agora vamos obter um único valor de outra estrutura de dados que tem um índice de cadeia de caracteres. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **Resultados**

    |ResultValue|
    |------|
    |0.5|

    Se você tentar usar um índice numérico para obter um valor desta série, você obterá um erro.

Este exercício foi destinado para dar uma ideia de como trabalhar com estruturas de dados diferentes do Python e verifique se que você obter o resultado correto como um quadro de dados. Você pode ter concluído que produzir um único valor como um quadro de dados é mais problemas para que seu valor! Felizmente, você pode passar facilmente todos os tipos de valores de entrada e saída do procedimento armazenado como variáveis. Que é abordado na próxima lição.

## <a name="tips"></a>Dicas

+ Entre linguagens de programação Python é uma das mais flexível em relação a aspas simples e aspas duplas; eles são bastante intercambiáveis. 

    No entanto, o T-SQL usa aspas simples para somente determinadas coisas e o `@script` argumento usa aspas simples para colocar o código do Python como uma cadeia de caracteres Unicode. Portanto, você precisará examinar o código do Python e alterar alguns aspas para aspas duplas.

+ Não é possível encontrar o procedimento armazenado, `sp_execute_external_script`? Isso significa que você provavelmente ainda não tiver terminado de configurar a instância para dar suporte à execução de script externo. Depois de executar a instalação do SQL Server 2017 e selecionando Python como a linguagem de aprendizado de máquina, você deve habilitar explicitamente o recurso usando `sp_configure`e, em seguida, reinicie a instância. 

    Para obter detalhes, consulte [instalar o SQL Server 2017 serviços Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md).

## <a name="next-steps"></a>Próximas etapas

[Encapsular o código do Python em um procedimento armazenado SQL](wrap-python-in-tsql-stored-procedure.md)