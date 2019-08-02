---
title: Crie gráficos e plotagens usando funções do SQL e do R-SQL Server Machine Learning
description: Tutorial mostrando como criar grafos e plotagens usando funções de linguagem do R em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3e8293fecf351176ac2b1e88176395f6c2b34d20
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715313"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Criar gráficos e plotagens usando o SQL e o R (Walkthrough)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nesta parte do tutorial, você aprende técnicas para gerar plotagens e mapas usando o R com dados de SQL Server. Você cria um histograma simples e, em seguida, desenvolve um gráfico de mapa mais complexo.

## <a name="prerequisites"></a>Pré-requisitos

Esta etapa pressupõe uma sessão de R em andamento com base nas etapas anteriores neste passo a passos. Ele usa as cadeias de conexão e os objetos de fonte de dados criados nessas etapas. As seguintes ferramentas e pacotes são usados para executar o script.

+ Rgui. exe para executar comandos do R
+ Management Studio executar o T-SQL
+ googMap
+ pacote ggmap
+ pacote mapproj

## <a name="create-a-histogram"></a>Criar um histograma

1. Gere a primeira plotagem, usando a função [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  A função rxHistogram fornece funcionalidade semelhante àquela em pacotes de R de software livre, mas pode ser executada em um contexto de execução remota.

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
    > Seu grafo parece diferente?
    >  
    > Isso ocorre porque o indataname usa apenas as primeiras 1000 linhas. A ordenação de linhas que usam TOP é não determinística na ausência de uma cláusula ORDER BY, portanto, é esperado que os dados e o grafo resultante possam variar.
    > Essa imagem em particular foi gerada usando aproximadamente 10.000 linhas de dados. Recomendados que você teste com diferentes números de linhas para obter gráficos diferentes e observe quanto tempo leva para que os resultados sejam retornados em seu ambiente.

## <a name="create-a-map-plot"></a>Criar um gráfico de mapa

Normalmente, os servidores de banco de dados bloqueiam o acesso à Internet. Isso pode ser inconveniente ao usar pacotes de R que precisam baixar mapas ou outras imagens para gerar plotagens. No entanto, há uma solução alternativa que pode ser útil ao desenvolver seus próprios aplicativos. Basicamente, você gera a representação de mapa no cliente e, em seguida, sobrepõe no mapa os pontos que são armazenados como atributos na tabela SQL Server.

1. Defina a função que cria o objeto de gráfico de R. A função personalizada *mapPlot* cria um gráfico de dispersão que usa os locais de retirada de táxi e plota o número de corridas iniciados a partir de cada local. Ele usa os pacotes **ggplot2** e **ggmap** , que já devem estar [instalados e carregados](walkthrough-data-science-end-to-end-walkthrough.md#add-packages).

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

    + A função *mapPlot* usa dois argumentos: um objeto de dados existente, que você definiu anteriormente usando RxSqlServerData e a representação de mapa passada do cliente.
    + Na linha que começa com a variável *DS* , rxImport é usado para carregar os dados de memória da fonte de dados criada anteriormente, inmemoryname *.* (Essa fonte de dados contém apenas 1000 linhas; se você quiser criar um mapa com mais pontos de dados, poderá substituir uma fonte de dados diferente.)
    + Sempre que você usa funções de R de software livre, os dados devem ser carregados em quadros de dados na memória local. No entanto, chamando a função [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) , você pode executar na memória do contexto de computação remota.

2. Altere o contexto de computação para local e carregue as bibliotecas necessárias para criar os mapas.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + A variável `gc` armazena um conjunto de coordenadas para Times Square, NY.

    + A linha que começa com `googmap` gera um mapa com as coordenadas especificadas no centro.

3. Alterne para o contexto de computação SQL Server e processe os resultados, encapsulando a função de plotagem em [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) , conforme mostrado aqui. A função rxExec faz parte do pacote **RevoScaleR** e dá suporte à execução de funções do R arbitrárias em um contexto de computação remota.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Os dados do mapa `googMap` no são passados como um argumento para a função executada remotamente *mapPlot*. Como os mapas foram gerados em seu ambiente local, eles devem ser passados para a função a fim de criar a plotagem no contexto de SQL Server.

    + Quando a linha que começa `plot` com é executada, os dados renderizados são serializados de volta para o ambiente do r local para que você possa exibi-los em seu cliente r.

    > [!NOTE]
    > Se você estiver usando SQL Server em uma máquina virtual do Azure, poderá receber um erro neste ponto. Um erro ocorre quando a regra de firewall padrão no Azure bloqueia o acesso à rede pelo código R. Para obter detalhes sobre como corrigir esse erro, consulte [instalando os serviços do Machine Learning (R) em uma VM do Azure](../install/sql-machine-learning-azure-virtual-machine.md).

4. A imagem a seguir mostra a plotagem de saída. Os locais em que os táxis apanham os clientes são adicionados ao mapa como pontos vermelhos. Sua imagem pode parecer diferente, dependendo de quantos locais estão na fonte de dados usada.

    ![plotagem de viagens de táxi usando uma função do R personalizada](media/rsql-e2e-mapplot.png "plotagem de viagens de táxi usando uma função do R personalizada")

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar recursos de dados usando R e SQL](walkthrough-create-data-features.md)
