---
title: "Criar gr&#225;ficos usando o R (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Criar gr&#225;ficos usando o R (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
Nesta lição, você aprenderá técnicas para gerar gráficos e mapas usando o R com os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Você verá como é fácil exibir gráficos criados no servidor e como você pode passar objetos gráficos para o servidor.  
  
## <a name="creating-graphics"></a>Criação de gráficos
No [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], os objetos gráficos, bem como os modelos e resultados, são serializados entre seu computador e o contexto de computação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Ao usar um contexto de computação do SQL Server, você não poderá baixar a representação do mapa, pois a maioria dos servidores de banco de dados de produção bloqueia completamente o acesso à Internet.  Portanto, para criar o segundo conjunto de plotagens, você vai gerar a representação de mapa no cliente e sobrepor no mapa os pontos armazenados como atributos na tabela *nyctaxi_sample*.   

Para fazer isso, primeiro crie a representação de mapa chamando o Google Maps e passe a representação do mapa para o contexto SQL.  
  
Esse é um padrão que pode ser útil ao desenvolver seus próprios aplicativos.   
  
### <a name="create-a-histogram"></a>Criar um histograma  
Para criar um histograma, você usará a fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é criado anteriormente, juntamente com a função `rxHistogram` fornecida no R Services.  
  
1.  Gere a primeira plotagem, usando a função *rxHistogram*.  A função *rxHistogram* fornece funcionalidade semelhante a dos pacotes de R de código-fonte aberto, mas pode ser executada em um contexto de execução remota. 
  
    ```R  
    #Plot fare amount on SQL Server and return the plot  
    start.time <- proc.time()  
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```         
  
2.  A imagem é retornada no dispositivo gráfico do R do ambiente de desenvolvimento.  Por exemplo, no RStudio, clique na janela **Plotar** .  No [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], uma janela gráfica separada é aberta.  
  
    ![using rxHistogram to plot fare amounts](../../advanced-analytics/r-services/media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")  
  
    > [!NOTE]  Como a ordenação das linhas com TOP não é determinística sem uma cláusula ORDER BY, você poderá ver resultados muito diferentes. Recomendados que você teste com diferentes números de linhas para obter gráficos diferentes e observe quanto tempo leva para que os resultados sejam retornados em seu ambiente.  Essa imagem em particular foi gerada usando aproximadamente 10.000 linhas de dados.
  
### <a name="create-a-map-plot"></a>Criar um plotagem de mapa  
Neste exemplo, você vai gerar um objeto de plotagem usando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o contexto de computação e retornar o objeto de plotagem ao contexto de computação local para renderização.  
   
1.  Primeiro, defina a função que cria o objeto de plotagem.  

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
    + A função de R personalizada *mapPlot* cria um gráfico de dispersão que usa os locais de embarque de passageiros no táxi para plotar o número de corridas que foram iniciadas em cada local. Ela usa os pacotes **ggplot2** e  **ggmap** , que já devem estar instalados e carregados.  
    + A função personalizada *mapPlot* usa dois argumentos: um objeto de dados existente, definido anteriormente usando *RxSqlServerData*, e a representação do mapa passada do cliente.    
    + Observe o uso da variável *ds* para carregar dados da fonte de dados criada anteriormente, *inDataSource*.  Sempre que você usar funções do R de software livre, os dados deverão ser carregados em quadros de dados na memória. Você pode fazer isso usando a função *rxImport* no pacote **RevoScaleR**.  No entanto, essa função é executada na memória, no contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido anteriormente. Ou seja, a função não usa a memória da estação de trabalho local.  
  
2.  Em seguida, carregue as bibliotecas necessárias para criar os mapas no ambiente local do R.  
  
    ```R  
    library(ggmap)  
    library(mapproj)  
    gc <- geocode("Times Square", source = "google")  
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color';    
    ```  
    + Esse código é executado no cliente do R. Observe a chamada repetida para as bibliotecas **ggmap** e **mapproj**. O motivo é que a definição da função anterior foi executada no contexto do servidor e as bibliotecas nunca foram carregadas localmente; agora você está levando a operação de plotagem de volta para sua estação de trabalho.  
  
    -   A variável *gc* armazena um conjunto de coordenadas para Times Square, NY.  
  
    -   A linha que começa com *googmap* gera um mapa com as coordenadas especificadas no centro.  
          
  
3.  Execute a função de plotagem e renderize os resultados no ambiente local do R. Para fazer isso, encapsule a função de plotagem em *rxExec*, como mostrado aqui.  A função *rxExec* está incluída no pacote **RevoScaleR** e dá suporte à execução de funções do R arbitrárias no contexto de computação remota. 
  
    ```R  
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)  
    plot(myplots[[1]][["myplot"]]);  
  
    ```  
    + Na primeira linha, você pode ver que os dados do mapa são passados como um argumento (*googMap*) para a função executada remotamente *mapPlot*. Isso ocorre porque os mapas foram gerados no ambiente local e devem ser passados para a função a fim de criar a plotagem no contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   
  
        Em seguida, os dados renderizados são serializados de volta para o ambiente local do R, para que você possa exibi-los usando a janela **Plotar** no RStudio ou em outro dispositivo gráfico do R.  
  
  
4.  Esta é a plotagem de saída, mostrando os locais embarque de passageiros no mapa como pontos vermelhos.  
  
    ![plotting taxi rides using a custom R function](../../advanced-analytics/r-services/media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 3: Criar recursos de dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
