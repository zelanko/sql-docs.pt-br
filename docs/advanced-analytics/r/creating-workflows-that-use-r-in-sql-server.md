---
title: Criar fluxos de trabalho SSIS e SSRS com R
description: Cenários de integração que combinam SQL Server Serviços de Machine Learning e R Services, Reporting Services (SSRS) e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b8d55e95991437e4d76911fd26afb5b1bc9c550
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2019
ms.locfileid: "68715169"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Criar fluxos de trabalho do SSIS e do SSRS com R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo explica como usar o script incorporado R e Python usando os recursos de ciência de dados e de linguagem do SQL Server Serviços de Machine Learning com dois recursos importantes de SQL Server: SQL Server Integration Services (SSIS) e SQL Server Reporting Services SSRS. As bibliotecas R e Python no SQL Server fornecem funções estatísticas e preditivas. O SSIS e o SSRS fornecem transformação e visualizações de ETL coordenadas, respectivamente. Este artigo explica como colocar todos esses recursos juntos neste padrão de fluxo de trabalho:

> [!div class="checklist"]
> * Criar um procedimento armazenado que contenha R ou Python executável
> * Executar o procedimento armazenado do SSIS ou SSRS

Os exemplos neste artigo são basicamente sobre R e SSIS, mas os conceitos e as etapas se aplicam igualmente ao Python. A segunda seção fornece orientações e links para visualizações do SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Usar o SSIS para automação

Fluxos de trabalho de ciência de dados são altamente iterativos e envolvem muita transformação de dados, incluindo dimensionamento, agregações, cálculo de probabilidades, renomeação e mesclagem de atributos. Os cientistas de dados estão acostumados a fazer muitas dessas tarefas em R, Python ou outra linguagem; contudo, a execução desses fluxos de trabalho em dados empresariais requer integração perfeita com processos e ferramentas de ETL.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] o permite executar operações complexas em R por meio de Transact-SQL e procedimentos armazenados, você pode integrar tarefas de ciência de dados com processos de ETL existentes. Em vez de executar uma cadeia de tarefas com uso intensivo de memória, a preparação de dados pode ser otimizada usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] as [!INCLUDE[tsql](../../includes/tsql-md.md)]ferramentas mais eficientes, incluindo e. 

Aqui estão algumas ideias sobre como você pode automatizar seus pipelines de processamento e modelagem de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]dados usando:

+ Extrair dados de fontes de nuvem ou locais para criar dados de treinamento 
+ Compilar e executar modelos de R ou Python como parte de um fluxo de trabalho de integração de dados
+ Readaptação de modelos em uma base regular (agendada)
+ Carregar resultados de script R ou Python para outros destinos, como Excel, Power BI, Oracle e Teradata, para citar alguns
+ Usar as tarefas do SSIS para criar recursos de dados no SQL Database
+ Use a ramificação condicional para alternar o contexto de computação para trabalhos de R e Python

## <a name="ssis-example"></a>Exemplo de SSIS

O exemplo a seguir provém de uma postagem de blog do MSDN agora desativada, criada por Jimmy Wong nesta URL:`https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

Este exemplo mostra como automatizar tarefas usando o SSIS. Você cria procedimentos armazenados com R incorporado usando SQL Server Management Studio e, em seguida, executa esses procedimentos armazenados de [executar tarefas do T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) em um pacote do SSIS.

Para percorrer este exemplo, você deve estar familiarizado com Management Studio, SSIS, Designer SSIS, design de pacote e T-SQL. O pacote SSIS usa três [tarefas executar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) que inserem dados de treinamento em uma tabela, modelam os dados e pontuam os dados para obter a saída de previsão.

### <a name="load-training-data"></a>Carregar dados de treinamento

Execute o script a seguir em SQL Server Management Studio para criar uma tabela para armazenar os dados. Você deve criar e usar um banco de dados de teste para este exercício. 

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

Crie um procedimento armazenado que carregue dados de treinamento no quadro de dados. Este exemplo está usando o conjunto de dados íris interno. 

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

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que execute o procedimento armazenado que você acabou de definir. O script para SQLStatement remove os dados existentes, especifica quais dados inserir e, em seguida, chama o procedimento armazenado para fornecer os dados.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Inserir dados](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "Inserir dados")

### <a name="generate-a-model"></a>Gerar um modelo

Execute o script a seguir em SQL Server Management Studio para criar uma tabela que armazena um modelo. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

Crie um procedimento armazenado que gera um modelo linear usando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). As bibliotecas RevoScaleR e revoscalepy estão automaticamente disponíveis em sessões de R e Python no SQL Server para que não haja necessidade de importar a biblioteca.

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

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) para executar o procedimento armazenado **generate_iris_rx_model** . O modelo é serializado e salvo na tabela ssis_iris_models. O script para SQLStatement é o seguinte:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Gera um modelo linear](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "Gera um modelo linear")

Como um ponto de verificação, após a conclusão dessa tarefa, você pode consultar o ssis_iris_models para ver que ele contém um modelo binário.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Previsão (Pontuação) resultados usando o modelo "treinado"

Agora que você tem código que carrega dados de treinamento e gera um modelo, a única etapa restante é usar o modelo para gerar previsões. 

Para fazer isso, coloque o script R na consulta SQL para disparar a função de R interna [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) em ssis_iris_model. Um procedimento armazenado chamado **predict_species_length** realiza essa tarefa.

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

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que execute o procedimento armazenado **predict_species_length** para gerar o comprimento de pétala previsto.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Gerar previsões](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "Gerar previsões")

### <a name="run-the-solution"></a>Executar a solução

No Designer SSIS, pressione F5 para executar o pacote. Você deverá ver um resultado semelhante à captura de tela a seguir.

![F5 para ser executado no modo de depuração](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 para ser executado no modo de depuração")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Usar o SSRS para visualizações

Embora o R possa criar gráficos e visualizações interessantes, ele não é bem integrado a fontes de dados externas, o que significa que cada gráfico ou gráfico precisa ser produzido individualmente. O compartilhamento também pode ser difícil.

Usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]o, você pode executar operações complexas em R por [!INCLUDE[tsql](../../includes/tsql-md.md)] meio de procedimentos armazenados, que podem ser facilmente consumidos por uma variedade de ferramentas [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de relatórios empresariais, incluindo e Power bi.

### <a name="ssrs-example"></a>Exemplo de SSRS

[R Graphics Device para Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/)

Este projeto CodePlex fornece o código para ajudá-lo a criar um item de relatório personalizado que renderiza a saída de gráficos de R como uma imagem que pode [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ser usada em relatórios.  Usando o item de relatório personalizado, é possível:

+ Publicar gráficos e plotagens criados usando o R Graphics Device para painéis do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Passar parâmetros [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para gráficos de R

> [!NOTE]
> Para este exemplo, o código que dá suporte ao dispositivo de gráficos R para Reporting Services deve ser instalado no servidor Reporting Services, bem como no Visual Studio. Também são necessárias a compilação e a configuração manuais.

## <a name="next-steps"></a>Próximas etapas

Os exemplos do SSIS e do SSRS neste artigo ilustram dois casos de execução de procedimentos armazenados que contêm script R ou Python incorporado. Um importante argumento é que você pode tornar o script R ou Python disponível para qualquer aplicativo ou ferramenta que possa enviar uma solicitação de execução em um procedimento armazenado. Uma vantagem adicional para o SSIS é que você pode criar pacotes que automatizam e agendam uma ampla gama de operações, como aquisição de dados, limpeza, manipulação e assim por diante, com a funcionalidade de ciência de dados R ou Python incluída na cadeia de operações. Para obter mais informações e ideias, consulte operacionalize o [código R usando procedimentos armazenados no SQL Server serviços de Machine Learning](operationalizing-your-r-code.md).