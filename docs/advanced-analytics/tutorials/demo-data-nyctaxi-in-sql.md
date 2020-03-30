---
title: Dados de demonstração de Táxi de Nova York para tutoriais
description: Crie um banco de dados que contenha os dados de exemplo de taxi de Nova York. Esse conjunto de dados é usado em tutoriais de R e Python para os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e55076a539cb2a932c2f1e0c432daf774899518f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74908916"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Dados de demonstração de táxi de Nova York para tutoriais de Python e R do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo explica como configurar um banco de dados de exemplo que consiste em dados públicos da [Comissão táxi e limusines da Cidade de Nova York](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Esses dados são usados em vários tutoriais de R e Python para análise no banco de dados no SQL Server. Para fazer com que o código de exemplo seja executado mais rapidamente, criamos uma amostragem representativa de 1% dos dados. No seu sistema, o arquivo de backup do banco de dados terá um pouco mais de 90 MB, fornecendo 1,7 milhões de linhas na tabela de dados primária.

Para concluir este exercício, você deve ter o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que possa restaurar um arquivo de backup de banco de dados e executar consultas T-SQL.

Os tutoriais e guias de início rápido que usam esse conjunto de dados incluem o seguinte:

+ [Aprender sobre análise no banco de dados usando R no SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Aprender sobre análise no banco de dados usando Python no SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Baixar arquivos

O banco de dados de exemplo é um arquivo BAK do SQL Server 2016 hospedado pela Microsoft. Você pode restaurá-lo no SQL Server 2016 e posterior. O download do arquivo é iniciado imediatamente quando você clica no link. 

O tamanho do arquivo é aproximadamente 90 MB.

1. Clique em [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) para baixar o arquivo de backup do banco de dados.

2. Copie o arquivo na pasta C:\Arquivos de Programas\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup.

3. No Management Studio, clique com o botão direito do mouse em **Bancos de Dados** e selecione **Restaurar Arquivos e Grupos de Arquivos**.

4. Insira *NYCTaxi_Sample* como o nome do banco de dados.

5. Clique em **Do dispositivo** e, em seguida, abra a página seleção de arquivo para selecionar o arquivo de backup. Clique em **Adicionar** para selecionar NYCTaxi_Sample.bak.

6. Marque a caixa de seleção **Restaurar** e clique em **OK** para restaurar o banco de dados.

## <a name="review-database-objects"></a>Examinar objetos de banco de dados
   
Confirme se os objetos de banco de dados existem na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você deverá ver banco de dados, tabelas, funções e procedimentos armazenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxi_sample-database"></a>Objetos no banco de dados NYCTaxi_Sample

A tabela a seguir resume os objetos criados no banco de dados de demonstração de táxi de Nova York.

|**Nome do objeto**|**Tipo de objeto**|**Descrição**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | Banco de Dados | Cria um banco de dados e duas tabelas:<br /><br />tabela dbo.nyctaxi_sample: Contém o conjunto de dados principal de táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de dados de Táxi de Nova York está inserida nesta tabela.<br /><br />tabela dbo.nyc_taxi_models: Usada para persistir o modelo treinado de análise avançada.|
|**fnCalculateDistance** |função de valor escalar | Calcula a distância direta entre os locais de embarque e desembarque de passageiros. Essa função é usada em [Criar recursos de dados](sqldev-create-data-features-using-t-sql.md), [Treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md) e [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |função com valor de tabela | Cria novos recursos de dados para treinamento de modelo. Essa função é usada em [Criar recursos de dados](sqldev-create-data-features-using-t-sql.md) e [Operacionalizar o modelo de R](sqldev-operationalize-the-model.md).|


Os procedimentos armazenados são criados usando scripts de R e Python encontrados em vários tutoriais. A tabela a seguir resume os procedimentos armazenados que você pode adicionar opcionalmente ao banco de dados de demonstração de táxi de Nova York ao executar o script de várias lições.

|**Procedimento armazenado**|**Idioma**|**Descrição**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Chama a função RevoScaleR rxHistogram para plotar o histograma de uma variável e retorna a plotagem como um objeto binário. Esse procedimento armazenado é usado em [Explorar e visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Cria um gráfico usando uma função Hist e salva a saída como um arquivo PDF local. Esse procedimento armazenado é usado em [Explorar e visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Treina um modelo de regressão logística chamando um pacote do R. O modelo prevê o valor da coluna tipped e é treinado usando uma seleção aleatória de 70% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models. Esse procedimento armazenado é usado em [Treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Chama o modelo treinado para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada. Esse procedimento armazenado é usado em [Prever resultados potenciais](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Chama o modelo treinado para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação. Esse procedimento armazenado é usado em [Prever resultados potenciais](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se os dados foram carregados.

1. No Pesquisador de Objetos, em Bancos de Dados, clique com o botão direito do mouse no banco de dados **NYCTaxi_Sample** e inicie uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
O banco de dados contém 1,7 milhões linhas.

3. No banco de dados, há uma tabela **nyctaxi_sample** que contém o conjunto de dados. Esta tabela foi otimizada para cálculos baseados em conjunto com a adição de um [índice columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md). Execute esta instrução para gerar um resumo rápido na tabela.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
Os resultados devem ser semelhantes aos mostrados na captura de tela a seguir.

  ![Informações de resumo da tabela](media/nyctaxidatatablesummary.png "Resultados da consulta")

## <a name="next-steps"></a>Próximas etapas

Os dados de exemplo de táxi de Nova York já estão disponíveis para o aprendizado prático.

+ [Aprender sobre análise no banco de dados usando R no SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Aprender sobre análise no banco de dados usando Python no SQL Server](sqldev-in-database-python-for-sql-developers.md)