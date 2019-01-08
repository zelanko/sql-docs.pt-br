---
title: Baixe dados de demonstração de táxi de NYC e scripts para embedded R e Python – Machine Learning do SQL Server
description: Instruções para baixar dados de exemplo de táxi de Nova York e criação de um banco de dados. Dados são usados nos tutoriais de linguagem Python do SQL Server e R que mostra como incorporar o script em procedimentos armazenados do SQL Server e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 25ac1b4884b0d12de9de59f44ba02ac9fec7e952
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645017"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Dados de demonstração de táxi de NYC para tutoriais do SQL Server Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como configurar um banco de dados de exemplo consiste em dados públicos a partir de [táxi de Nova York e Limusines comissão](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Esses dados são usados nos tutoriais de várias R e Python para análise no banco de dados no SQL Server. Para fazer o código de exemplo executado mais rápido, criamos uma amostragem representativa de 1% dos dados. Em seu sistema, o arquivo de backup do banco de dados é um pouco mais de 90 MB, fornecendo 1.7 milhões de linhas na tabela de dados primário.

Para concluir este exercício, você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que pode restaurar um arquivo de backup do banco de dados e executar consultas T-SQL.

Tutoriais e guias de início rápido usando esse conjunto de dados incluem o seguinte:

+ [Aprenda a análise no banco de dados usando o R no SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Aprenda a análise no banco de dados usando o Python no SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Baixar arquivos

O banco de dados de exemplo é um arquivo de SQL Server 2016 BAK hospedado pela Microsoft. Você pode restaurá-lo no SQL Server 2016 e posterior. Download do arquivo começa imediatamente quando você clica no link. 

Tamanho do arquivo é de aproximadamente 90 MB.

1. Clique em [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) para baixar o arquivo de backup do banco de dados.

2. Copie o arquivo C:\Program files\Microsoft SQL Server\MSSQL instância name\MSSQL\Backup pasta.

3. No Management Studio, clique com botão direito **bancos de dados** e selecione **restaurar arquivos e grupos de arquivos**.

4. Insira *NYCTaxi_Sample* como o nome do banco de dados.

5. Clique em **do dispositivo** e, em seguida, abra a página de seleção de arquivo para selecionar o arquivo de backup. Clique em **adicionar** para selecionar NYCTaxi_Sample.bak.

6. Selecione o **restaurar** caixa de seleção e clique em **Okey** para restaurar o banco de dados.

## <a name="review-database-objects"></a>Examine os objetos de banco de dados
   
Confirme se os objetos de banco de dados existem na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você deve ver o banco de dados, tabelas, funções e procedimentos armazenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Objetos no banco de dados NYCTaxi_Sample

A tabela a seguir resume os objetos criados no banco de dados de demonstração de táxi de Nova York.

|**Nome do objeto**|**Tipo de objeto**|**Descrição**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | Banco de Dados | Cria um banco de dados e duas tabelas:<br /><br />tabela nyctaxi_sample: Contém o conjunto de dados principal táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de dados de táxi de Nova York será inserida nesta tabela.<br /><br />tabela dbo.nyc_taxi_models: Usado para persistir o modelo treinado de análise avançada.|
|**fnCalculateDistance** |função de valor escalar | Calcula a distância direta entre os locais de embarque e desembarque de passageiros. Essa função é usada na [criar recursos de dados](sqldev-create-data-features-using-t-sql.md), [treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md) e [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |função com valor de tabela | Cria novos recursos de dados para treinamento do modelo. Essa função é usada na [criar recursos de dados](sqldev-create-data-features-using-t-sql.md) e [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|


Procedimentos armazenados são criados usando o script de R e Python encontrada nos vários tutoriais. A tabela a seguir resume os procedimentos armazenados que você pode opcionalmente adicionar ao banco de dados de demonstração de táxi de NYC quando você executar o script de várias lições.

|**procedimento armazenado**|**Idioma**|**Descrição**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Chama a função RevoScaleR rxHistogram para plotar o histograma de uma variável e, em seguida, retorna a plotagem como um objeto binário. Esse procedimento armazenado é usado em [explorar e visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Cria um gráfico usando a função Hist e salva a saída como um arquivo PDF local. Esse procedimento armazenado é usado em [explorar e visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Treina um modelo de regressão logística chamando um pacote R. O modelo prevê o valor da coluna tipped e é treinado usando uma seleção aleatória de 70% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models. Esse procedimento armazenado é usado em [treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Chama o modelo treinado para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada. Esse procedimento armazenado é usado em [prever resultados potenciais](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Chama o modelo treinado para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação. Esse procedimento armazenado é usado em [prever resultados potenciais](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se que os dados foram carregados.

1. No Pesquisador de objetos em bancos de dados, clique com botão direito do **NYCTaxi_Sample** de banco de dados e iniciar uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
O banco de dados contém 1.7 milhões de linhas.

3. No banco de dados é um **nyctaxi_sample** tabela que contém o conjunto de dados. A tabela foi otimizada para cálculos com base em conjunto com a adição de um [índice de columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md). Execute esta instrução para gerar um resumo rápido na tabela.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
Resultados devem ser semelhantes aos que mostra a captura de tela a seguir.

  ![Informações de resumo da tabela](media/nyctaxidatatablesummary.png "resultados da consulta")

## <a name="next-steps"></a>Próximas etapas

Dados de exemplo de táxi de NYC agora estão disponíveis para o aprendizado prático.

+ [Aprenda a análise no banco de dados usando o R no SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Aprenda a análise no banco de dados usando o Python no SQL Server](sqldev-in-database-python-for-sql-developers.md)