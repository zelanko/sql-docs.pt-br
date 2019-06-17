---
title: Criar fluxos de trabalho SSIS e o SSRS com R - serviços do SQL Server Machine Learning
description: Cenários de integração de combinar serviços do SQL Server Machine Learning e R Services, Reporting Services (SSRS) e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5d480b7cd24200b051fa2626fc41fa757703eaf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642661"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Criar fluxos de trabalho SSIS e o SSRS com R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como usar o script de R e Python incorporado usando os recursos de ciência de dados e de idioma de serviços do SQL Server Machine Learning com dois recursos importantes do SQL Server: SQL Server Integration Services (SSIS) e SQL Server Reporting Services SSRS. Bibliotecas de R e Python no SQL Server fornecem funções de estatística e previsão. SSIS e o SSRS fornecem coordenados transformação de ETL e visualizações, respectivamente. Este artigo explica como juntar todos esses recursos nesse padrão de fluxo de trabalho:

> [!div class="checklist"]
> * Criar um procedimento armazenado que contém o executável R ou Python
> * Execute o procedimento armazenado do SSIS ou SSRS

Os exemplos neste artigo são principalmente sobre R e o SSIS, mas os conceitos e as etapas se aplicam igualmente ao Python. A segunda seção fornece diretrizes e links para visualizações do SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Usar o SSIS para a automação

Fluxos de trabalho de ciência de dados são altamente iterativos e envolvem muita transformação de dados, incluindo dimensionamento, agregações, cálculo de probabilidades, renomeação e mesclagem de atributos. Os cientistas de dados estão acostumados a fazer muitas dessas tarefas em R, Python ou outra linguagem; contudo, a execução desses fluxos de trabalho em dados empresariais requer integração perfeita com processos e ferramentas de ETL.

Porque [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite que você execute operações complexas em R por meio do Transact-SQL e procedimentos armazenados, você pode integrar tarefas de ciência de dados com os processos ETL existentes. Em vez disso, executar uma cadeia de tarefas intensivo de memória, preparação de dados pode ser otimizada usando as ferramentas mais eficientes, incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Aqui estão algumas ideias de como você pode automatizar o processamento de dados e pipelines de modelagem usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Extrair dados localmente ou na nuvem fontes para criar dados de treinamento 
+ Compilar e executar R ou Python modelos como parte de um fluxo de trabalho de integração de dados
+ Readaptar os modelos regularmente (agendado)
+ Carregar os resultados do script R ou Python para outros destinos, como Excel, Power BI, Oracle e Teradata, para citar alguns exemplos
+ Usar tarefas do SSIS para criar recursos de dados no banco de dados SQL
+ Usar ramificação condicional para alternar o contexto de computação para trabalhos de R e Python

## <a name="ssis-example"></a>Exemplo do SSIS

O exemplo a seguir é proveniente de uma postagem de blog do MSDN já aposentado criada por Jimmy Wong nesta URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

Este exemplo mostra como automatizar tarefas usando o SSIS. Criar procedimentos armazenados com o R inserido usando o SQL Server Management Studio e, em seguida, executar esses procedimentos armazenados do [tarefas de T-SQL Execute](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) em um pacote SSIS.

Para percorrer este exemplo, você deve estar familiarizado com o Management Studio, SSIS, SSIS Designer, design de pacote e T-SQL. O pacote do SSIS usa três [tarefas de T-SQL Execute](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) que inserir dados de treinamento em uma tabela, os dados de modelo e pontuar os dados para obter uma saída de previsão.

### <a name="load-training-data"></a>Carregar dados de treinamento

Execute o seguinte script no SQL Server Management Studio para criar uma tabela para armazenar os dados. Você deve criar e usar um banco de dados de teste para este exercício. 

```T-SQL
Use test-db
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO
```

Crie um procedimento armazenado que carrega dados de treinamento no quadro de dados. Este exemplo usa o conjunto de dados íris internos. 

```T-SQL
Create procedure load_iris
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'iris_df <- iris;'
        , @input_data_1 = N''
        , @output_data_1_name = N'iris_df'
    with result sets (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100)));
end;
```

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que executa o procedimento armazenado que você acabou de definir. O script para **SQLStatement** remove dados existentes, especifica quais dados a serem inseridos e, em seguida, chama o procedimento armazenado para fornecer os dados.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Inserir dados](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "inserir dados")

### <a name="generate-a-model"></a>Gerar um modelo

Execute o seguinte script no SQL Server Management Studio para criar uma tabela que armazena um modelo. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

Criar um procedimento armazenado que gera um modelo linear usando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Bibliotecas de RevoScaleR e revoscalepy estão automaticamente disponíveis em sessões de R e Python no SQL Server, portanto, não há nenhuma necessidade de importar a biblioteca.

```T-SQL
Create procedure generate_iris_rx_model
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'
          irisLinMod <- rxLinMod(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = ssis_iris);
          trained_model <- data.frame(payload = as.raw(serialize(irisLinMod, connection=NULL)));'
        , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris'
        , @input_data_1_name = N'ssis_iris'
        , @output_data_1_name = N'trained_model'
    with result sets ((model varbinary(max)));
end;
GO
```

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) para executar o **generate_iris_rx_model** procedimento armazenado. O modelo é serializado e salvo na tabela ssis_iris_models. O script para **SQLStatement** é da seguinte maneira:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Gera um modelo linear](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "gera um modelo linear")

Como um ponto de verificação depois de concluir essa tarefa, você pode consultar o ssis_iris_models para ver que ele contém um modelo binário.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Prever resultados (pontuação) usando o modelo "treinado"

Agora que você tem código que carrega dados de treinamento e gera um modelo, a única etapa restante é usando o modelo para gerar previsões. 

Para fazer isso, coloque o script R na consulta SQL para disparar a [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) função R interna em ssis_iris_model. Um procedimento armazenado chamado **predict_species_length** realiza essa tarefa.

```T-SQL
Create procedure predict_species_length (@model varchar(100))
as
begin
    declare @rx_model varbinary(max) = (select model from ssis_iris_models where model_name = @model);
    -- Predict based on the specified model:
    exec sp_execute_external_script
        @language = N'R'
        , @script = N'
irismodel <-unserialize(rx_model);
irispred <- rxPredict(irismodel, ssis_iris[,2:6]);
OutputDataSet <- cbind(ssis_iris[1], irispred$Sepal.Length_Pred, ssis_iris[2]);
colnames(OutputDataSet) <- c("id", "Sepal.Length.Actual", "Sepal.Length.Expected");
#OutputDataSet <- subset(OutputDataSet, Species.Length.Actual != Species.Expected);
'
    , @input_data_1 = N'
    select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris
    '
    , @input_data_1_name = N'ssis_iris'
    , @params = N'@rx_model varbinary(max)'
    , @rx_model = @rx_model
    with result sets ( ("id" int, "Species.Length.Actual" float, "Species.Length.Expected" float)
        );
end;
```

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que executa o **predict_species_length** procedimento armazenado para gerar o comprimento da pétala previsto.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Gerar previsões](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "gerar previsões")

### <a name="run-the-solution"></a>Executar a solução

No SSIS Designer, pressione F5 para executar o pacote. Você deve ver um resultado semelhante à seguinte captura de tela.

![F5 para executar no modo de depuração](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 para executar no modo de depuração")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Use o SSRS para visualizações

Embora R possa criar gráficos e visualizações interessantes, não é bem integrado com fontes de dados externas, significando que cada de gráfico tem de ser produzido individualmente. O compartilhamento também pode ser difícil.

Usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], você pode executar operações complexas em R via [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados, que podem ser facilmente consumidos por uma variedade de ferramentas, incluindo de relatórios corporativos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o Power BI.

### <a name="ssrs-example"></a>Exemplo do SSRS

[R Graphics Device para Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/)

Este projeto CodePlex fornece o código para ajudá-lo a criar um item de relatório personalizado que renderiza a saída de gráficos do R como uma imagem que pode ser usada em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatórios.  Usando o item de relatório personalizado, é possível:

+ Publicar gráficos e plotagens criados usando o R Graphics Device para painéis do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Passar parâmetros [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para gráficos de R

> [!NOTE]
> Para este exemplo, o código que dá suporte ao R Graphics Device para Reporting Services deve ser instalado no servidor do Reporting Services, bem como no Visual Studio. Também são necessárias a compilação e a configuração manuais.

## <a name="next-steps"></a>Próximas etapas

Os exemplos SSIS e o SSRS neste artigo ilustram dois casos de execução de procedimentos armazenados que contêm o script de R ou Python incorporado. Uma consideração importante é que você possa fazer script do R ou Python disponíveis para qualquer aplicativo ou uma ferramenta que pode enviar uma solicitação de execução em um procedimento armazenado. Uma vantagem adicional para SSIS é que você pode criar pacotes que automatizam e agendar a ampla variedade de operações, como aquisição de dados, limpeza, manipulação e assim por diante, com o R ou Python funcionalidade de ciência de dados incluída na cadeia de operações. Para obter mais informações e ideias, consulte [código Operacionalizar o R usando procedimentos armazenados no SQL Server Machine Learning Services](operationalizing-your-r-code.md).