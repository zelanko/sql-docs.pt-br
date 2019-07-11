---
title: Depuração/diagnosticar aplicativos Spark
titleSuffix: SQL Server big data clusters
description: Use o servidor de histórico do Spark para depurar e diagnosticar aplicativos Spark em execução em clusters de grandes dados do SQL Server 2019.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cba788fcb61dddce54d8b0c4ad4f2ca87ea0906d
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728392"
---
# <a name="debug-and-diagnose-spark-applications-on-sql-server-big-data-clusters-in-spark-history-server"></a>Depurar e diagnosticar aplicativos do Spark em clusters de grandes dados do SQL Server no servidor de histórico do Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece orientação sobre como usar o servidor de histórico Spark estendido para depurar e diagnosticar aplicativos Spark em um cluster de big data do SQL Server 2019 (visualização). Esses recursos de depuração e diagnóstico são criados no servidor de histórico do Spark e fornecidos pela Microsoft. A extensão inclui guias de dados e guia gráfico e diagnóstico. Na guia dados, os usuários podem verificar os dados de entrada e saída do trabalho do Spark. Na guia gráfico, os usuários podem verificar o fluxo de dados e repetir o grafo de trabalho. Na guia de diagnóstico, o usuário pode se referir a distorção de dados, distorção de tempo e análise de uso do Executor.

## <a name="get-access-to-spark-history-server"></a>Obter acesso ao servidor de histórico do Spark

A experiência do usuário de servidor do histórico de Spark do código-fonte aberto é aprimorada com informações, que incluem dados específicos do trabalho e visualização interativa de fluxos de trabalho gráfico e os dados para o cluster de big data. 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>Abra a Web da interface do usuário pela URL do servidor de histórico Spark
Substituir do servidor de histórico do Spark, navegando até a URL a seguir, abra `<Ipaddress>` e `<Port>` com informações específicas do cluster de big data. Obter mais informações podem ser referenciadas: [Implantar um cluster de big data do SQL Server](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

A web do servidor de histórico Spark a interface do usuário é semelhante a:

![Servidor de histórico do Spark](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Guia de dados no servidor de histórico do Spark
Selecione a ID do trabalho e clique em **dados** no menu de ferramenta para obter a exibição de dados.

+ Verifique as **entradas**, **saídas**, e **operações de tabela** selecionando as guias separadamente.

    ![Guias de dados do servidor de histórico do Spark](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ Copiar todas as linhas clicando no botão **cópia**.

    ![Copiar todas as linhas](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ Salvar todos os dados como arquivo CSV clicando no botão **csv**.

    ![Salvar dados como arquivos CSV](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ Pesquisa digitando palavras-chave no campo **pesquisa**, o resultado da pesquisa será exibida imediatamente.

    ![Pesquisar por palavras-chave](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ Clique no cabeçalho de coluna para classificar a tabela, clique no sinal de adição para expandir uma linha para mostrar mais detalhes ou clique no sinal de menos para recolher uma linha.

    ![Funcionalidade de tabela de dados](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ Baixar um único arquivo clicando no botão **Download parcial** que coloque à direita, em seguida, o arquivo selecionado é baixado para um lugar local. Se o arquivo não existir mais, ele abrirá uma nova guia para mostrar as mensagens de erro.

    ![Baixe uma linha de dados](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ Copiar caminho completo ou relativo, selecionando o **Copiar caminho completo**, **Copiar caminho relativo** que se expande de menu download. Para arquivos do armazenamento do azure data lake **aberto no Gerenciador de armazenamento do Azure** iniciará o Gerenciador de armazenamento do Azure. E localize a pasta exata ao entrar.

    ![Copiar um caminho completo ou relativo](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ Clique em navegar o número abaixo da tabela de páginas quando muito muitas linhas para exibir em uma única página. 

    ![Página de dados](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ Passe o mouse sobre o ponto de interrogação ao lado de dados para mostrar a dica de ferramenta, ou clique no ponto de interrogação para obter mais informações.

    ![Dados de mais informações](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ Enviar comentários com problemas clicando **fornecer comentários**.

    ![comentários de gráfico](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Guia do gráfico no servidor de histórico do Spark

Selecione a ID do trabalho e clique em **Graph** no menu de ferramenta para obter o modo de exibição de gráfico do trabalho.

+ Verifique a visão geral do seu trabalho, o grafo de trabalho gerado. 

+ Por padrão, ele mostrará todos os trabalhos, e ele pode ser filtrado por **ID do trabalho**.

    ![ID do trabalho de grafo](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ Deixamos **andamento** como valor padrão. Usuário pode verificar o fluxo de dados, selecionando **leitura** ou * * Written * * * na lista suspensa de **exibição**.

    ![exibição de gráfico](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    A exibição do nó de gráfico na cor que mostra o mapa de calor.

    ![gráfico de mapa de calor](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ Reproduzir o trabalho clicando o **reprodução** botão e parar a qualquer momento clicando no botão Parar. A exibição de tarefas na cor para mostrar o status diferentes durante a reprodução:

    + Verde para bem-sucedido: O trabalho foi concluído com êxito.
    + Laranja para repetida: Instâncias das tarefas que falharam, mas não afetam o resultado final do trabalho. Essas tarefas tinham duplicar ou repita instâncias que podem ter êxito posteriormente.
    + Azul para execução: A tarefa está em execução.
    + Branco para espera ou ignorados: A tarefa está esperando para ser executado ou o estágio foi ignorada.
    + Falha em vermelho para: Falha da tarefa.

    ![amostra de cor do gráfico, em execução](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    A exibição de estágio ignorada em branco.
    ![amostra de cor do Graph, ignorar](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![amostra de cor do gráfico, com falha](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > Reprodução para cada trabalho é permitida. Para o trabalho incompleto. não há suporte para reprodução.


+ Rola o mouse para aplicar zoom de entrada/saída grafo do trabalho, ou clique em **Aplicar Zoom para ajustar** para torná-lo a ajustar à tela.
 
    ![Aplicar zoom de gráfico para ajustar](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ Passe o mouse no nó de gráfico para ver a dica de ferramenta quando há falha de tarefas e clique no Palco para abrir a página de estágio.

    ![Dica de ferramenta do gráfico](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ Na guia gráfico de trabalho, estágios terá dica de ferramenta e o ícone pequeno exibidas se tiverem tarefas atender o abaixo de condições:
    + Distorção de dados: tamanho de leitura de dados > tamanho de todas as tarefas dentro do estágio de leitura de média de dados * > 10 MB de tamanho de 2 e leitura de dados
    + Distorção de tempo: tempo de execução > tempo médio de execução de todas as tarefas dentro do estágio * 2 e o tempo de execução > 2 min

    ![ícone de distorção de grafo](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ O nó de gráfico do trabalho exibirá as informações a seguir de cada estágio:
    + ID.
    + Nome ou descrição.
    + Número total de tarefas.
    + Dados lidos: tamanho de leitura as somas de tamanho de entrada e de ordem aleatória.
    + Gravação de dados: as somas de tamanho de saída e em ordem aleatória de tamanho de gravação.
    + Tempo de execução: o tempo entre a hora de início da primeira tentativa e tempo de conclusão da última tentativa.
    + Contagem de linhas: a soma dos registros de entrada, registros de saída, em ordem aleatória de registros de leitura e gravação registros em ordem aleatória.
    + Progresso.

    > [!NOTE]
    > Por padrão, o nó de gráfico do trabalho exibirá informações da última tentativa de cada estágio (com exceção de tempo de execução do estágio), mas durante o gráfico de reprodução de nó mostrará informações de cada tentativa.

    > [!NOTE]
    > Para o tamanho dos dados de leitura e gravação que podemos usar 1 MB = 1000 KB = 1000 * 1000 Bytes.

+ Enviar comentários com problemas clicando **fornecer comentários**.

    ![comentários de gráfico](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Guia de diagnóstico no servidor de histórico do Spark
Selecione a ID do trabalho e clique em **diagnóstico** no menu de ferramenta para obter a modo de exibição de diagnóstico do trabalho. A guia Diagnóstico inclui **distorção de dados**, **distorção de horário**, e **análise de uso do Executor**.
    
+ Verifique as **distorção de dados**, **distorção de horário**, e **análise de uso do Executor** selecionando as guias, respectivamente.

    ![Guias de diagnóstico](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>Distorção de dados
Clique em **distorção de dados** guia correspondente distorcidas as tarefas são exibidas com base nos parâmetros especificados. 

+ **Especificar parâmetros** -a primeira seção exibe os parâmetros, que são usados para detectar a distorção de dados. A regra interna é: Dados da tarefa lidos é maior que três vezes os tarefa médio da leitura dos dados e a leitura de dados de tarefa são maior que 10 MB. Se você quiser definir sua própria regra para tarefas distorcidas, você pode escolher seus parâmetros, o **estágio distorcido**, e **distorcer Char** seção será atualizada adequadamente. 

+ **Distorcida estágio** -a segunda seção exibe os estágios, que tem Inclinado tarefas que atendem aos critérios especificados acima. Se houver mais de uma tarefa distorcida em um estágio, a tabela de estágio distorcido exibe apenas a tarefa mais distorcida (por exemplo, os maiores data para distorção de dados). 

    ![Section2 de distorção de dados](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **Inclinar o gráfico** - quando uma linha na tabela de preparo distorção é selecionada, a exibição do gráfico de distorção de obter mais detalhes de distribuições de tarefa com base em dados de leitura e o tempo de execução. As tarefas distorcidas são marcadas em vermelho e as tarefas normais são marcadas em azul. Para considerações sobre desempenho, o gráfico exibe apenas tarefas de exemplo até 100. Os detalhes da tarefa são exibidos no painel inferior direito.

    ![Remoções3 de distorção de dados](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>Distorção de tempo
O **distorção de horário** guia exibe tarefas distorcidas com base em tempo de execução de tarefa. 

+ **Especificar parâmetros** -a primeira seção exibe os parâmetros, que são usados para detectar a distorção de horário. Os critérios para detectar a distorção de tempo padrão é: tempo de execução de tarefa é maior que três vezes média de tempo de execução e tempo de execução de tarefa é maior que 30 segundos. Você pode alterar os parâmetros de acordo com suas necessidades. O **estágio distorcido** e **inclinar o gráfico** exibir as informações de tarefas e estágios correspondentes exatamente como o **distorção de dados** guia acima.

+ Clique em **distorção de horário**, e em seguida, o resultado filtrado é exibido na **estágio distorcido** seção de acordo com os parâmetros definidos na seção **especificar parâmetros**. Clique em um item na **estágio distorcido** seção e, em seguida, o gráfico correspondente é escrito em Remoções3 e os detalhes da tarefa são exibidos no painel inferior direito.

    ![Section2 distorção de tempo](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>Análise de uso do executor
O gráfico de uso do Executor visualiza o status de alocação e a execução de executor real do trabalho Spark.  

+ Clique em **análise de uso do Executor**, em seguida, podemos curvas de quatro tipos sobre o uso do executor de rascunho. Eles incluem **executores alocado**, **executando executores**, **ocioso executores**, e **máximo de instâncias de Executor**. Em relação à executores alocados, cada "Executor adicionado" ou "Executor removido" evento aumentará ou diminuirá os executores alocados. Você pode verificar a "Linha do tempo do evento" na guia "Trabalhos" para mais de comparação.

    ![Guia de executores](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ Clique no ícone de cor para selecionar ou desmarcar o conteúdo correspondente em todos os rascunhos.

    ![Selecione o gráfico](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>Problemas conhecidos
O servidor de histórico do Spark tem os seguintes problemas conhecidos:

+ Atualmente, ele só funciona para o cluster Spark 2.3.

+ Dados de entrada/saída usando RDD não serão mostrados na guia dados.

## <a name="next-steps"></a>Próximas etapas

* [Gerenciar recursos para um cluster Spark no HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-resource-manager)
* [Definir configurações do Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-settings)
