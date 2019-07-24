---
title: Executar trabalhos do Spark com as ferramentas do Spark & Hive para VS Code no cluster SQL Server Big Data
titleSuffix: SQL Server big data clusters
description: Envie um trabalho do Spark com as ferramentas do Spark & Hive para Visual Studio Code no cluster SQL Server Big Data.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425976"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>Enviar trabalhos do Spark no cluster SQL Server Big Data no Visual Studio Code

Saiba como usar as ferramentas do Spark & Hive para Visual Studio Code para criar e enviar scripts do PySpark para o Apache Spark, primeiro descreveremos como instalar as ferramentas do Spark & Hive no Visual Studio Code e, em seguida, veremos como enviar trabalhos para o Spark.  

As ferramentas do hive do Spark & podem ser instaladas em plataformas com suporte no Visual Studio Code, que incluem Windows, Linux e macOS. Abaixo você encontrará os pré-requisitos para diferentes plataformas.


## <a name="prerequisites"></a>Pré-requisitos

Os itens a seguir são necessários para concluir as etapas neste artigo:

- Um cluster SQL Server Big Data. Consulte [SQL Server Big data clusters](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
- [Visual Studio Code](https://code.visualstudio.com/).
- [Mono](https://www.mono-project.com/docs/getting-started/install/). O mono é necessário apenas para Linux e macOS.
- [Configurar o ambiente interativo do PySpark para Visual Studio Code](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment).
- Um diretório local chamado **HDexample**.  Este artigo usa **C:\HD\HDexample**.

## <a name="install-spark--hive-tools"></a>Instalar as ferramentas do Spark & Hive

Depois de concluir os pré-requisitos, você poderá instalar as ferramentas do Spark & Hive para Visual Studio Code.  Conclua as etapas a seguir para instalar as ferramentas do Spark & Hive:

1. Abra Visual Studio Code.

2. Na barra de menus, navegue até **Exibir** > **extensões**.

3. Na caixa de pesquisa, insira **Spark & Hive**.

4. Selecione **Ferramentas do hive do Spark &** nos resultados da pesquisa e selecione **instalar**.  

   ![Instalar extensão](./media/spark-hive-tools-vscode/extension.png)

5. Recarregue quando necessário.

## <a name="open-work-folder"></a>Abrir pasta de trabalho

Conclua as etapas a seguir para abrir uma pasta de trabalho e criar um arquivo no Visual Studio Code:

1. Na barra de menus, navegue até **arquivo** > **abrir pasta..** . C:\HD\HDexample, em seguida, selecione o botão **Selecionar pasta** .   >  A pasta aparece no modo de exibição do **Explorer** à esquerda.

2. No modo de exibição do **Explorer** , selecione a pasta, **HDexample**, e o ícone **novo arquivo** ao lado da pasta de trabalho.

   ![Novo arquivo](./media/spark-hive-tools-vscode/new-file.png)

3. Nomeie o novo arquivo com a `.py` extensão de arquivo (script Spark).  Este exemplo usa **HelloWorld.py**.
4. Copie e cole o seguinte código no arquivo de script:
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>Vincular um cluster de Big Data SQL Server

Antes de enviar scripts para seus clusters do Visual Studio Code, você precisa vincular um SQL Server Big Data cluster.

1. Na barra de menus, navegue até **Exibir** > **paleta de comandos...** e **insira Spark/Hive: Vincular um cluster**.

   ![comando vincular cluster](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. Selecione o tipo de cluster vinculado **SQL Server Big data**.

3. Insira SQL Server ponto de extremidade de Big Data.

4. Insira SQL Server nome de usuário do cluster de Big Data.

5. Insira a senha para o administrador do usuário.

6. Defina o nome de exibição do cluster (opcional).

7. Listar clusters, examinar exibição de **saída** para verificação.

## <a name="list-clusters"></a>Listar clusters

1. Na barra de menus, navegue até **Exibir** > **paleta de comandos...** e **insira Spark/Hive: Listar**cluster.

2. Examine a exibição de **saída** .  A exibição mostrará seus clusters vinculados.

    ![Definir uma configuração de cluster padrão](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>Definir cluster padrão

1. Abra novamente a pasta **HDexample** criada [anteriormente](#open-work-folder) se fechada.  

2. Selecione o arquivo **HelloWorld.py** criado [anteriormente](#open-work-folder) e ele será aberto no editor de scripts.

3. Vincule um cluster se ainda não tiver feito isso.

4. Clique com o botão direito do mouse no editor **de scripts e selecione Spark/Hive: Defina o cluster**padrão.   

5. Selecione um cluster como o cluster padrão para o arquivo de script atual. As ferramentas atualizam automaticamente o arquivo de configuração **. VSCode\settings.json**. 

   ![Definir configuração de cluster padrão](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>Enviar consultas interativas do PySpark

Você pode enviar consultas PySpark interativas seguindo as etapas abaixo:

1. Reabra a pasta **HDexample** criada [anteriormente](#open-work-folder) se fechada.  

2. Selecione o arquivo **HelloWorld.py** criado [anteriormente](#open-work-folder) e ele será aberto no editor de scripts.

3. Vincule um cluster se ainda não tiver feito isso.

4. Escolha todo o código e clique com o botão direito do mouse no **editor de scripts, selecione Spark: PySpark Interactive** para enviar a consulta ou use o atalho **Ctrl + Alt + I**.

   ![menu de contexto interativo do pyspark](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. Selecione o cluster se você não tiver especificado um cluster padrão. Após alguns instantes, os resultados interativos do **Python** aparecem em uma nova guia. As ferramentas também permitem que você envie um bloco de código em vez do arquivo de script inteiro usando o menu de contexto. 

   ![janela interativa do Python pyspark Interactive](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. Insira **"%% info"** e pressione **Shift + Enter** para exibir informações do trabalho. (opcional)

   ![exibir informações do trabalho](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > Quando a **extensão do Python habilitada** está desmarcada nas configurações (a configuração padrão está marcada), os resultados da interação pyspark enviada usarão a janela antiga.
   >
   > ![extensão do Python interativa do pyspark desabilitada](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>Enviar trabalho do lote PySpark

1. Reabra a pasta **HDexample** criada [anteriormente](#open-work-folder) se fechada.  

2. Selecione o arquivo **HelloWorld.py** criado [anteriormente](#open-work-folder) e ele será aberto no editor de scripts.

3. Vincule um cluster se ainda não tiver feito isso.

4. Clique com o botão direito do mouse no editor de **scripts e selecione Spark: PySpark lote**ou use o atalho **Ctrl + Alt + H**. 

5. Selecione o cluster se você não tiver especificado um cluster padrão. Depois de enviar um trabalho do Python, os logs de envio aparecem na janela de **saída** no Visual Studio Code. A **URL da interface do usuário do Spark** e a **URL da interface do usuário yarn** também são mostradas. Você pode abrir a URL em um navegador da Web para acompanhar o status do trabalho.

   ![Enviar resultado do trabalho do Python](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Configuração do Apache Livy

A configuração do [Apache Livy](https://livy.incubator.apache.org/) tem suporte, ela pode ser definida no **. VSCode\settings.json** na pasta de espaço de trabalho. Atualmente, a configuração do Livy dá suporte apenas ao script Python. Para obter mais detalhes, consulte [LIVY README](https://github.com/cloudera/livy/blob/master/README.rst ).

### <a id="triggerlivyconf"></a>**Como disparar a configuração do Livy**

#### <a name="method-1"></a>Método 1

1. Na barra de menus, navegue até **arquivo** > **preferências** > **configurações**.  
2. Na caixa de texto **configurações** de pesquisa **, insira Sumission de trabalho do HDInsight: Livy conf**.  
3. Selecione **Editar em Settings. JSON** para o resultado da pesquisa relevante.

#### <a name="method-2"></a>Método 2

Envie um arquivo, observe que `.vscode` a pasta é adicionada automaticamente à pasta de trabalho. Você pode encontrar a configuração do Livy clicando `.vscode\settings.json`em.

+ As configurações do projeto:

    ![Configuração do Livy](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>Para as configurações **driverMomory** e **executorMomry**, defina o valor com unidade, por exemplo 1G ou 1024M. 

### <a name="supported-livy-configurations"></a>Configurações de Livy com suporte

#### <a name="post-batches"></a>POSTAR/batches

**Corpo da solicitação**

| name | description | type |
| :- | :- | :- |
| Arquivo | Arquivo que contém o aplicativo a ser executado | caminho (obrigatório) |
| proxyUser | Usuário a representar ao executar o trabalho | cadeia de caracteres |
| className | Classe principal do aplicativo Java/Spark | cadeia de caracteres |
| argumento | Argumentos de linha de comando para o aplicativo | lista de cadeias de caracteres |
| Jars | Jars a serem usados nesta sessão | Lista de cadeia de caracteres |
| pyFiles | Arquivos Python a serem usados nesta sessão | Lista de cadeia de caracteres |
| files | arquivos a serem usados nesta sessão | Lista de cadeia de caracteres |
| driverMemory | Quantidade de memória a ser usada para o processo de driver | cadeia de caracteres |
| driverCores | Número de núcleos a serem usados para o processo de driver | int |
| executorMemory | Quantidade de memória a ser usada por processo de executor | cadeia de caracteres |
| executorCores | Número de núcleos a serem usados para cada executor | int |
| numExecutors | Número de executores a serem iniciados para esta sessão | int |
| zip | Arquivos mortos a serem usados nesta sessão | Lista de cadeia de caracteres |
| queue | O nome da fila YARN para a qual foi enviado | cadeia de caracteres |
| name | O nome desta sessão | cadeia de caracteres |
| conf | Propriedades de configuração do Spark | Mapa de chave = Val |

#### <a name="response-body"></a>Corpo da resposta

O objeto de lote criado.

| name | description | type |
| :- | :- | :- |
| id | A ID da sessão | int |
| appId | A ID do aplicativo desta sessão | Cadeia de caracteres |
| appInfo | As informações detalhadas do aplicativo | Mapa de chave = Val |
| Façam | As linhas de log | lista de cadeias de caracteres |
| state | O estado do lote | cadeia de caracteres |

>[!NOTE]
>A configuração Livy atribuída será exibida no painel de saída quando o script for enviado.

## <a name="additional-features"></a>Recursos adicionais

O Spark & Hive para Visual Studio Code dá suporte aos seguintes recursos:

- **Preenchimento automático do IntelliSense**. Sugestões pop-up para palavra-chave, métodos, variáveis e assim por diante. Ícones diferentes representam tipos diferentes de objetos.

    ![Ferramentas do hive & Spark para tipos de objeto Visual Studio Code IntelliSense](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **Marcador de erro do IntelliSense**. O serviço de linguagem sublinha os erros de edição para o script do hive.     
- **Destaques da sintaxe**. O serviço de idioma usa cores diferentes para diferenciar variáveis, palavras-chave, tipo de dados, funções e assim por diante. 

    ![Ferramentas do Spark & Hive para Visual Studio Code destaques da sintaxe](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>Desvincular cluster

1. Na barra de menus, navegue até **Exibir** > **paleta de comandos...** e, **em seguida, insira Spark/Hive: Desvincular um cluster**.  

2. Selecione cluster para desvincular.  

3. Examine a exibição de **saída** para verificação.  

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre SQL Server Big Data cluster e cenários relacionados, consulte [SQL Server clusters Big data](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
