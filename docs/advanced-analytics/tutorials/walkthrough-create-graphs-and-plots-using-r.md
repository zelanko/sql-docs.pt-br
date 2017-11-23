---
title: "Criar gráficos e gráficos usando SQL e R (passo a passo) | Microsoft Docs"
ms.date: 11/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: e720755146e8d29ddf06ccdecdd2d744c1885013
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2017
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Criar gráficos e gráficos usando SQL e R (passo a passo)

Nesta parte do passo a passo, você aprenderá técnicas para gerar gráficos e mapas usando R com dados do SQL Server. Criar um histograma simple, para praticar um pouco e, em seguida, desenvolver um gráfico de mapa mais complexo.

### <a name="create-a-histogram"></a>Criar um histograma

1. Gere a primeira plotagem, usando a função [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  A função rxHistogram fornece funcionalidade semelhante em pacotes de software livre R, mas pode ser executado em um contexto de execução remota.

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
    > O gráfico ser diferente?
    >  
    > Isso ocorre porque _inDataSource_ usa somente as primeiras 1000 linhas. A ordenação de linhas usando TOP é não determinística na ausência de uma cláusula ORDER BY, portanto é esperado que os dados e o gráfico resultante podem variar.
    > Essa imagem em particular foi gerada usando aproximadamente 10.000 linhas de dados. Recomendados que você teste com diferentes números de linhas para obter gráficos diferentes e observe quanto tempo leva para que os resultados sejam retornados em seu ambiente.

### <a name="create-a-map-plot"></a>Criar um gráfico de mapa

Normalmente, os servidores de banco de dados bloqueiam acesso à Internet. Isso pode ser inconveniente ao usar pacotes de R que precisam baixar mapas ou outras imagens para gerar gráficos. No entanto, há uma solução alternativa que podem ser úteis ao desenvolver seus próprios aplicativos. Basicamente, gere a representação de mapa no cliente e sobreposição no mapa de pontos que são armazenados como atributos na tabela do SQL Server.

1. Defina a função que cria o objeto de plotagem de R. A função personalizada *mapPlot* cria um gráfico de dispersão que usa os locais de recebimento táxi e plota o número de percursos iniciado a partir de cada local. Ela usa os pacotes **ggplot2** e  **ggmap** , que já devem estar instalados e carregados.

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

    + O *mapPlot* função leva dois argumentos: um objeto de dados existente, que você definiu anteriormente usando RxSqlServerData e a representação de mapa passado do cliente.
    + Em que a linha que começa com o *ds* variável rxImport é usada para carregar dados de memória da fonte de dados criado anteriormente, *inDataSource*. (Essa fonte de dados contém apenas 1000 linhas; se você quiser criar um mapa com mais pontos de dados, você pode substituir uma fonte de dados diferente).
    + Sempre que você usar **código-fonte aberto** funções de R, dados devem ser carregadas em quadros de dados na memória local. No entanto, ao chamar o [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) função, você pode executar na memória do contexto de computação remota.

2. Alterar o contexto de computação local e carregar as bibliotecas necessárias para criar os mapas.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + A variável `gc` armazena um conjunto de coordenadas para Times Square, NY.

    + A linha que começa com `googmap` gera um mapa com as coordenadas especificadas no centro.

3. Alterne para o contexto de computação do SQL Server e processar os resultados, encapsulando a função de plotagem em [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) conforme mostrado aqui. A função rxExec faz parte do **RevoScaleR** pacote e oferece suporte à execução de funções de R arbitrárias em um contexto de computação remota.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Os dados do mapa em `googMap` é passado como um argumento para a função executada remotamente *mapPlot*. Porque os mapas que foram gerados em seu ambiente local, deve ser passados para a função para criar o gráfico no contexto do SQL Server.

    + Quando a linha que começa com `plot` é executado, os dados renderizados é serializada de volta para o ambiente local do R para que você pode exibi-lo no seu cliente de R.

    > [!NOTE]
    > Se você estiver usando o SQL Server em uma máquina virtual do Azure, você poderá receber um erro neste momento. Isso ocorre porque uma regra de firewall padrão no Azure bloqueia o acesso à rede pelo código R. Para obter detalhes sobre como corrigir esse erro, consulte [instalando o R Services em uma VM do Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

4. A imagem a seguir mostra a plotagem de saída. Os locais em que os táxis apanham os clientes são adicionados ao mapa como pontos vermelhos. A imagem pode ser diferente, dependendo de quantos locais são na fonte de dados que você usou.

    ![plotagem de viagens de táxi usando uma função do R personalizada](media/rsql-e2e-mapplot.png "plotagem de viagens de táxi usando uma função do R personalizada")

## <a name="next-lesson"></a>Próxima lição

[Criar recursos de dados usando R e SQL](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>Lição anterior

[Resumir dados usando R](/walkthrough-view-and-summarize-data-using-r.md)
