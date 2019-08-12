---
title: Executar trabalhos do Spark com as Ferramentas do Spark & Hive para o VS Code no cluster de Big Data do SQL Server
titleSuffix: SQL Server big data clusters
description: Envie trabalhos do Spark com as Ferramentas do Spark & Hive para o Visual Studio Code no cluster de Big Data do SQL Server.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68425976"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>Enviar trabalhos do Spark em clusters de Big Data do SQL Server no Visual Studio Code

Saiba como usar as Ferramentas do Spark & Hive para Visual Studio Code para criar e enviar scripts de PySpark para o Apache Spark. Primeiro, descreveremos como instalar as ferramentas do Spark & Hive no Visual Studio Code e, em seguida, veremos como enviar trabalhos para o Spark.  

As Ferramentas do Spark & Hive podem ser instaladas em plataformas com suporte do Visual Studio Code, que incluem Windows, Linux e macOS. A seguir, você verá os pré-requisitos das diferentes plataformas.


## <a name="prerequisites"></a>Prerequisites

Os itens a seguir são necessários para concluir as etapas neste artigo:

- Um cluster de Big Data do SQL Server. Confira [Clusters de Big Data do SQL Server](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
- [Visual Studio Code](https://code.visualstudio.com/).
- [Mono](https://www.mono-project.com/docs/getting-started/install/). O Mono é necessário apenas para Linux e macOS.
- [Configurar o ambiente interativo do PySpark para Visual Studio Code](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment).
- Um diretório local chamado **HDexample**.  Este artigo usa **C:\HD\HDexample**.

## <a name="install-spark--hive-tools"></a>Instalar Ferramentas do Spark & Hive

Após concluir os pré-requisitos, você poderá instalar as Ferramentas do Spark & Hive para Visual Studio Code.  Conclua as etapas a seguir para instalar as Ferramentas do Spark & Hive:

1. Abra o Visual Studio Code.

2. Na barra de menus, navegue até **Exibir** > **Extensões**.

3. Na caixa de pesquisa, insira **Spark & Hive**.

4. Selecione **Ferramentas do Spark & Hive** nos resultados da pesquisa e selecione **Instalar**.  

   ![Instalar extensão](./media/spark-hive-tools-vscode/extension.png)

5. Recarregue quando necessário.

## <a name="open-work-folder"></a>Abrir a pasta de trabalho

Conclua as etapas a seguir para abrir uma pasta de trabalho e criar um arquivo no Visual Studio Code:

1. Na barra de menus, navegue até **Arquivo** > **Abrir Pasta...**  > **C:\HD\HDexample**e, em seguida, selecione o botão **Selecionar Pasta**. A pasta aparece no modo de exibição do **Explorer** à esquerda.

2. No modo de exibição do **Explorer**, selecione a pasta **HDexample** e, em seguida, o ícone **Novo Arquivo** ao lado da pasta de trabalho.

   ![Novo arquivo](./media/spark-hive-tools-vscode/new-file.png)

3. Nomeie o novo arquivo com a extensão de arquivo `.py` (script de Spark).  Este exemplo usa **HelloWorld.py**.
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

## <a name="link-a-sql-server-big-data-cluster"></a>Vincular um cluster de Big Data do SQL Server

Antes de enviar scripts para a seus clusters do Visual Studio Code, você precisa vincular um cluster de Big Data do SQL Server.

1. Na barra de menus, navegue até **Exibir** > **Paleta de Comandos...** e insira **Spark / Hive: Vincular um cluster**.

   ![comando vincular cluster](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. Selecione o tipo de cluster vinculado **Big Data do SQL Server**.

3. Insira o ponto de extremidade de Big Data do SQL Server.

4. Insira o nome de usuário do Cluster de Big Data do SQL Server.

5. Insira a senha do administrador do usuário.

6. Defina o nome de exibição do cluster (opcional).

7. Liste os clusters e examine a exibição **SAÍDA** para verificação.

## <a name="list-clusters"></a>Listar clusters

1. Na barra de menus, navegue até **Exibir** > **Paleta de Comandos...** e insira **Spark / Hive: Listar Cluster**.

2. Examine a exibição **SAÍDA**.  A exibição mostrará seus clusters vinculados.

    ![Definir uma configuração de cluster padrão](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>Definir cluster padrão

1. Abra novamente a pasta **HDexample** criada [anteriormente](#open-work-folder) se estiver fechada.  

2. Selecione o arquivo **HelloWorld.py** criado [anteriormente](#open-work-folder) e ele será aberto no editor de scripts.

3. Vincule um cluster se ainda não tiver feito isso.

4. Clique com o botão direito do mouse no editor de scripts e selecione **Spark/Hive: Definir Cluster Padrão**.   

5. Selecione um cluster como o cluster padrão para o arquivo de script atual. As ferramentas atualizam automaticamente o arquivo de configuração **.VSCode\settings.json**. 

   ![Definir configuração de cluster padrão](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>Enviar consultas interativas de PySpark

Você pode enviar consultas de PySpark interativas seguindo as etapas abaixo:

1. Reabra a pasta **HDexample** criada [anteriormente](#open-work-folder) se estiver fechada.  

2. Selecione o arquivo **HelloWorld.py** criado [anteriormente](#open-work-folder) e ele será aberto no editor de scripts.

3. Vincule um cluster se ainda não tiver feito isso.

4. Escolha todo o código e clique com o botão direito do mouse no editor de scripts, selecione **Spark: PySpark Interativo** para enviar a consulta ou use o atalho **CTRL + ALT + I**.

   ![menu de contexto do pyspark interativo](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. Selecione o cluster se não tiver especificado um cluster padrão. Após alguns instantes, os resultados de **Python Interativo** aparecem em uma nova guia. As ferramentas também permitem que você envie um bloco de código em vez do arquivo de script inteiro usando o menu de contexto. 

   ![janela de python interativo pyspark interativo](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. Insira **"%%info"** e, em seguida, pressione **Shift + Enter** para exibir informações do trabalho. (opcional)

   ![exibir informações do trabalho](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > Quando **Extensão do Python Habilitada** é desmarcado nas configurações (a configuração padrão é estar marcado), os resultados da interação de pyspark enviados usarão a janela antiga.
   >
   > ![extensão de python interativa do pyspark desabilitada](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>Enviar trabalho em lotes PySpark

1. Reabra a pasta **HDexample** criada [anteriormente](#open-work-folder) se estiver fechada.  

2. Selecione o arquivo **HelloWorld.py** criado [anteriormente](#open-work-folder) e ele será aberto no editor de scripts.

3. Vincule um cluster se ainda não tiver feito isso.

4. Clique com o botão direito do mouse no editor de scripts e, em seguida selecione **Spark: Lote de PySpark** ou use o atalho **CTRL + ALT + H**. 

5. Selecione o cluster se não tiver especificado um cluster padrão. Após você enviar um trabalho do Python, os logs de envio aparecem na janela de **SAÍDA** no Visual Studio Code. A **URL da interface do usuário do Spark** e a **URL da interface do usuário do YARN** também são mostradas. Você pode abrir a URL em um navegador da Web para acompanhar o status do trabalho.

   ![Enviar resultado do trabalho do Python](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Configuração do Apache Livy

A configuração do [Apache Livy](https://livy.incubator.apache.org/) tem suporte, ela pode ser definida no **.VSCode\settings.json** na pasta de espaço de trabalho. Atualmente, a configuração do Livy dá suporte apenas ao script de Python. Para obter mais detalhes, confira o [LEIAME do Livy](https://github.com/cloudera/livy/blob/master/README.rst ).

### <a id="triggerlivyconf"></a>**Como disparar a configuração do Livy**

#### <a name="method-1"></a>Método 1

1. Na barra de menus, navegue até **Arquivo** > **Preferências** > **Configurações**.  
2. Na caixa de texto, **Configurações de pesquisa**, insira **Envio de Trabalho do HDInsight: Livy Conf**.  
3. Selecione **Editar em settings.json** para o resultado da pesquisa relevante.

#### <a name="method-2"></a>Método 2

Envie um arquivo, observe que a pasta `.vscode` é adicionada automaticamente à pasta de trabalho. Você pode encontrar a configuração do Livy clicando em `.vscode\settings.json`.

+ As configurações do projeto:

    ![Configuração do Livy](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>Para as configurações **driverMomory** e **executorMomry**, defina o valor com a unidade, por exemplo, 1g ou 1024m. 

### <a name="supported-livy-configurations"></a>Configurações do Livy com suporte

#### <a name="post-batches"></a>POST /lotes

**Corpo da solicitação**

| NAME | descrição | Tipo |
| :- | :- | :- |
| file | Arquivo que contém o aplicativo a ser executado | caminho (obrigatório) |
| proxyUser | Usuário a representar ao executar o trabalho | cadeia de caracteres |
| className | Classe principal de Java/Spark do aplicativo | cadeia de caracteres |
| args | Argumentos de linha de comando para o aplicativo | lista de cadeias de caracteres |
| jars | jars a serem usados nesta sessão | Lista de cadeias de caracteres |
| pyFiles | Arquivos Python a serem usados nesta sessão | Lista de cadeias de caracteres |
| files | arquivos a serem usados nesta sessão | Lista de cadeias de caracteres |
| driverMemory | Quantidade de memória a ser usada para o processo do driver | cadeia de caracteres |
| driverCores | Número de núcleos a serem usados para o processo do driver | INT |
| executorMemory | Quantidade de memória a ser usada pelo processo de executor | cadeia de caracteres |
| executorCores | Número de núcleos a serem usados para cada executor | INT |
| numExecutors | Número de executores a serem iniciados para esta sessão | INT |
| archives | Arquivos a serem usados nesta sessão | Lista de cadeias de caracteres |
| fila | O nome da fila YARN para a qual foi enviado | cadeia de caracteres |
| NAME | O nome desta sessão | cadeia de caracteres |
| conf | Propriedades de configuração do Spark | Mapa de chave = valor |

#### <a name="response-body"></a>Corpo da resposta

O objeto de lote criado.

| NAME | descrição | Tipo |
| :- | :- | :- |
| id | A ID da sessão | INT |
| appId | A ID do aplicativo desta sessão | Cadeia de caracteres |
| appInfo | As informações detalhadas do aplicativo | Mapa de chave = valor |
| log | As linhas de log | lista de cadeias de caracteres |
| state | O estado do lote | cadeia de caracteres |

>[!NOTE]
>A configuração do Livy atribuída será exibida no painel de saída quando o script for enviado.

## <a name="additional-features"></a>Recursos adicionais

O Spark & Hive para Visual Studio Code tem suporte para os seguintes recursos:

- **Preenchimento automático do IntelliSense**. Aparecem sugestões de palavra-chave, métodos, variáveis e assim por diante. Ícones diferentes representam tipos diferentes de objetos.

    ![Tipos de objeto de IntelliSense das Ferramentas do Spark & Hive para Visual Studio Code](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **Marcador de erro do IntelliSense**. O serviço de linguagem sublinha os erros de edição para o script do Hive.     
- **Destaques da sintaxe**. O serviço de linguagem usa cores diferentes para distinguir variáveis, palavras-chave, tipo de dados, funções e assim por diante. 

    ![Destaques de sintaxe das Ferramentas do Spark & Hive para Visual Studio Code](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>Desvincular cluster

1. Na barra de menus, navegue até **Exibir** > **Paleta de Comandos...** e, em seguida, insira **Spark / Hive: Desvincular um Cluster**.  

2. Selecione o cluster a ser desvinculado.  

3. Examine a exibição **SAÍDA** para verificação.  

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o cluster de Big Data do SQL Server e cenários relacionados, confira [Clusters de Big Data do SQL Server](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
