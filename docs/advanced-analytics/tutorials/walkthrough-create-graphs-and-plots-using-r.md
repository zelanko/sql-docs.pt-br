---
title: Criar gráficos e plotagens usando o SQL e R - funções SQL Server Machine Learning
description: Tutorial que mostra como criar gráficos e plotagens usando funções da linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 542e36e01565ab454cce8beae9a4fa65279d8fa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961780"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Criar gráficos e plotagens usando o SQL e R (passo a passo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nesta parte do passo a passo, você aprenderá técnicas para gerar gráficos e mapas usando o R com dados do SQL Server. Criar um histograma simple e, em seguida, desenvolver uma plotagem de mapa mais complexa.

## <a name="prerequisites"></a>Pré-requisitos

Essa etapa pressupõe que uma sessão de R em andamento, com base nas etapas anteriores neste passo a passo. Ele usa as conexão cadeias de caracteres e dados de origem objetos criados nessas etapas. As ferramentas e os pacotes a seguir são usados para executar o script.

+ Rgui.exe para executar comandos de R
+ Management Studio para executar o T-SQL
+ googMap
+ pacote de ggmap
+ pacote de mapproj

## <a name="create-a-histogram"></a>Criar um histograma

1. Gere a primeira plotagem, usando a função [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  A função rxHistogram fornece funcionalidade semelhante àquela em pacotes de R de código-fonte aberto, mas pode ser executados em um contexto de execução remota.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. A imagem é retornada no dispositivo gráfico do R do ambiente de desenvolvimento.  Por exemplo, no RStudio, clique na janela **Plotar** .  No [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], uma janela gráfica separada é aberta.

    ![usando rxHistogram para plotar valores de tarifa](media/rsql-e2e-rxhistogramresult.png "usando rxHistogram para plotar valores de tarifa")

    > [!NOTE]
    > O gráfico parece diferente?
    >  
    > Isso ocorre porque _inDataSource_ usa apenas as primeiras 1000 linhas. A ordenação das linhas usando TOP é não determinística na ausência de uma cláusula ORDER BY, portanto, é esperado que os dados e o gráfico resultante podem variar.
    > Essa imagem em particular foi gerada usando aproximadamente 10.000 linhas de dados. Recomendados que você teste com diferentes números de linhas para obter gráficos diferentes e observe quanto tempo leva para que os resultados sejam retornados em seu ambiente.

## <a name="create-a-map-plot"></a>Criar um gráfico de mapa

Normalmente, os servidores de banco de dados bloqueiam acesso à Internet. Isso pode ser inconveniente ao usar pacotes de R que precisam baixar mapas ou outras imagens para gerar gráficos. No entanto, há uma solução alternativa que podem ser úteis ao desenvolver seus próprios aplicativos. Basicamente, você gera a representação de mapa no cliente e sobrepor no mapa os pontos que são armazenados como atributos na tabela do SQL Server.

1. Defina a função que cria o objeto de plotagem do R. A função personalizada *mapPlot* cria um gráfico de dispersão que usa os locais embarque de passageiros no táxi e plota o número de corridas que foram iniciadas em cada local. Ele usa o **ggplot2** e **ggmap** pacotes, que já devem estar [instalado e carregado](walkthrough-data-science-end-to-end-walkthrough.md#add-packages).

    ```R
    mapPlot <- function(inDataSource, googMap){
        library(ggmap)
        library(mapproj)
        ds <- rxImport(inDataSource)
        p <- ggmap(googMap)+
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,
    color="darkred", size = 1.5)
        return(list(myplot=p))
    }
    ```

    + O *mapPlot* função leva dois argumentos: um objeto de dados existente, o que você definiu anteriormente usando o RxSqlServerData e a representação de mapa passada do cliente.
    + Em que a linha que começa com o *ds* variável, rxImport é usado para carregar dados de memória da fonte de dados criada anteriormente, *inDataSource*. (Essa fonte de dados contém apenas 1000 linhas; se você quiser criar um mapa com mais pontos de dados, você pode substituir uma fonte de dados diferente).
    + Sempre que você usa funções de R de código-fonte aberto, os dados devem ser carregados em quadros de dados na memória local. No entanto, ao chamar o [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) função, você pode executar na memória do contexto de computação remota.

2. Alterar o contexto de computação para o local e carregar as bibliotecas necessárias para criar os mapas.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + A variável `gc` armazena um conjunto de coordenadas para Times Square, NY.

    + A linha que começa com `googmap` gera um mapa com as coordenadas especificadas no centro.

3. Alterne para o contexto de computação do SQL Server e renderizar os resultados, encapsulando a função de plotagem em [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) conforme mostrado aqui. A função rxExec faz parte de **RevoScaleR** pacote e dá suporte à execução de funções do R arbitrárias no contexto de computação remota.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Os dados do mapa `googMap` é passado como um argumento para a função executada remotamente *mapPlot*. Porque os mapas foram gerados no seu ambiente local, deve ser passados para a função para criar a plotagem no contexto do SQL Server.

    + Quando a linha que começa com `plot` é executado, os dados renderizados é serializada de volta para o ambiente local do R para que você pode exibi-lo no seu cliente de R.

    > [!NOTE]
    > Se você estiver usando o SQL Server em uma máquina virtual do Azure, você poderá receber um erro neste momento. Um erro ocorre quando a regra de firewall padrão no Azure bloqueia o acesso à rede pelo código R. Para obter detalhes sobre como corrigir esse erro, consulte [instalando o Machine Learning (R) serviços em uma VM do Azure](../install/sql-machine-learning-azure-virtual-machine.md).

4. A imagem a seguir mostra a plotagem de saída. Os locais em que os táxis apanham os clientes são adicionados ao mapa como pontos vermelhos. Sua imagem pode parecer diferente, dependendo de quantos locais estão na fonte de dados que você usou.

    ![plotagem de viagens de táxi usando uma função do R personalizada](media/rsql-e2e-mapplot.png "plotagem de viagens de táxi usando uma função do R personalizada")

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar recursos de dados usando R e SQL](walkthrough-create-data-features.md)
