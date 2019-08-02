---
title: Baixe dados e scripts de demonstração do NYC táxi para R e Python inseridos
description: Instruções para baixar dados de exemplo de táxi de Nova York e criar um banco de dado. Os dados são usados nos tutoriais de linguagem SQL Server Python e R mostrando como inserir script em SQL Server procedimentos armazenados e funções T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5b60397bb3581ba2d210a6b4469184306145c8a
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714863"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Dados de demonstração do NYC táxi para SQL Server tutoriais de Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo explica como configurar um banco de dados de exemplo que consiste em um dado público do [táxi da cidade de Nova York e da Comissão limusines](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Esses dados são usados em vários tutoriais de R e Python para análise no banco de dados no SQL Server. Para fazer com que o código de exemplo seja executado mais rapidamente, criamos uma amostragem representativa de 1% dos dados. No seu sistema, o arquivo de backup do banco de dados é um pouco mais de 90 MB, fornecendo 1,7 milhões linhas na tabela Data primária.

Para concluir este exercício, você deve ter [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) ou outra ferramenta que possa restaurar um arquivo de backup de banco de dados e executar consultas T-SQL.

Os tutoriais e os guias de início rápido usando esse conjunto de dados incluem o seguinte:

+ [Aprenda sobre análise no banco de dados usando o R no SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Aprenda sobre análise no banco de dados usando Python no SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Baixar arquivos

O banco de dados de exemplo é um SQL Server arquivo 2016 BAK hospedado pela Microsoft. Você pode restaurá-lo no SQL Server 2016 e posterior. O download do arquivo é iniciado imediatamente quando você clica no link. 

O tamanho do arquivo é de aproximadamente 90 MB.

1. Clique em [NYCTaxi_Sample. bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) para baixar o arquivo de backup do banco de dados.

2. Copie o arquivo em C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup Folder.

3. No Management Studio, clique com o botão direito do mouse em **bancos de dados** e selecione **restaurar arquivos e grupos de arquivos**.

4. Insira *NYCTaxi_Sample* como o nome do banco de dados.

5. Clique em **do dispositivo** e abra a página seleção de arquivo para selecionar o arquivo de backup. Clique em **Adicionar** para selecionar NYCTaxi_Sample. bak.

6. Marque a caixa de seleção **restaurar** e clique em **OK** para restaurar o banco de dados.

## <a name="review-database-objects"></a>Examinar objetos de banco de dados
   
Confirme se os objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados existem [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]na instância do usando. Você deve ver o banco de dados, as tabelas, as funções e os procedimentos armazenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Objetos no banco de dados NYCTaxi_Sample

A tabela a seguir resume os objetos criados no banco de dados de demonstração de táxi NYC.

|**Nome do objeto**|**Tipo de objeto**|**Descrição**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | Cria um banco de dados e duas tabelas:<br /><br />tabela dbo. nyctaxi_sample: Contém o conjunto de NYC principal de táxi. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta. A amostra de 1% do conjunto de NYC de táxi é inserida nessa tabela.<br /><br />tabela _taxi_models dbo. NYC: Usado para persistir o modelo de análise avançada treinado.|
|**fnCalculateDistance** |função de valor escalar | Calcula a distância direta entre os locais de retirada e chegada. Essa função é usada em [criar recursos de dados](sqldev-create-data-features-using-t-sql.md), [treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md) e colocar [o modelo R em operação](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |função com valor de tabela | Cria novos recursos de dados para treinamento de modelo. Essa função é usada em [criar recursos de dados](sqldev-create-data-features-using-t-sql.md) e [operacionalize o modelo de R](sqldev-operationalize-the-model.md).|


Os procedimentos armazenados são criados usando o script R e Python encontrados em vários tutoriais. A tabela a seguir resume os procedimentos armazenados que você pode opcionalmente adicionar ao banco de dados de demonstração de táxi NYC ao executar o script de várias lições.

|**Procedimento armazenado**|**Idioma**|**Descrição**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Chama a função RevoScaleR rxHistogram para plotar o histograma de uma variável e, em seguida, retorna a plotagem como um objeto binário. Esse procedimento armazenado é usado em [explorar e Visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Cria um gráfico usando a função sua e salva a saída como um arquivo PDF local. Esse procedimento armazenado é usado em [explorar e Visualizar dados](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Treina um modelo de regressão logística chamando um pacote de R. O modelo prevê o valor da coluna tipped e é treinado usando uma seleção aleatória de 70% dos dados. A saída do procedimento armazenado é o modelo treinado, que é salvo na tabela nyc_taxi_models. Esse procedimento armazenado é usado em [treinar e salvar um modelo](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Chama o modelo treinado para criar previsões usando o modelo. O procedimento armazenado aceita uma consulta como seu parâmetro de entrada e retorna uma coluna de valores numéricos que contêm as pontuações para as linhas de entrada. Esse procedimento armazenado é usado em [prever resultados potenciais](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Chama o modelo treinado para criar previsões usando o modelo. Esse procedimento armazenado aceita uma nova observação como entrada, com valores de recursos individuais passados como parâmetros na linha, e retorna um valor que prevê o resultado da nova observação. Esse procedimento armazenado é usado em [prever resultados potenciais](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Consultar os dados

Como uma etapa de validação, execute uma consulta para confirmar se os dados foram carregados.

1. No Pesquisador de objetos, em bancos de dados, clique com o botão direito do mouse em **NYCTaxi_Sample** e inicie uma nova consulta.

2. Execute algumas consultas simples:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
O banco de dados contém 1,7 milhões linhas.

3. No banco de dados, há uma tabela **nyctaxi_sample** que contém o conjunto. A tabela foi otimizada para cálculos baseados em conjuntos com a adição de um [índice columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md). Execute esta instrução para gerar um resumo rápido da tabela.

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

Os dados de exemplo de táxi de NYC agora estão disponíveis para aprendizado prático.

+ [Aprenda sobre análise no banco de dados usando o R no SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Aprenda sobre análise no banco de dados usando Python no SQL Server](sqldev-in-database-python-for-sql-developers.md)