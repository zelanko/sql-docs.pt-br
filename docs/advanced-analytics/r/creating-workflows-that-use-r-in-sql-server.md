---
title: Criar fluxos de trabalho SSIS e o SSRS com R - serviços do SQL Server Machine Learning
description: Cenários de integração de combinar serviços do SQL Server Machine Learning e R Services, Reporting Services (SSRS) e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76ddf3e3fdb43fea6bb8fd224f8199cda4134b64
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976296"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Criar fluxos de trabalho SSIS e o SSRS com R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como usar procedimentos armazenados em dois recursos importantes do SQL Server, SQL Server Integration Services (SSIS) e SQL Server Reporting Services SSRS, de forma que combina dados relacionais, funções de ciência de dados de bibliotecas Microsoft R, e os recursos de BI para transformações de coordenada de dados e visualização. Saiba quais recursos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] prestam-se para uma solução de ciência de dados. Este artigo também lembra você de código e os dados no SQL Server, como o código R inserido em procedimentos armazenados, seja consumida facilmente em visualizações fornecidas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

## <a name="bring-compute-power-to-the-data"></a>Traga o poder de computação para os dados

Uma meta de design de chave de integração do R e Python com o SQL Server foi colocar a análise próxima aos dados. Isso oferece várias vantagens:

+ Segurança de dados. Trazendo o mais próximo do R para a fonte de dados evita a movimentação de dados desperdiçadora ou insegura.
+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. As recentes inovações em bancos de dados como tabelas na memória tornam resumos e agregações muito mais e são um complemento perfeito para ciência de dados.
+ Facilidade de integração e implantação. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas de gerenciamento de dados e aplicativos. Usando dados que residem no banco de dados ou no warehouse de relatórios, verifique se que os dados usados por soluções de aprendizado de máquina são consistente e atualizado. 
+ Eficiência na nuvem e locais. Em vez de processar dados no R, é possível contar com pipelines de dados corporativos incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o Azure Data Factory. Comunicar resultados ou análises é fácil com o Power BI ou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Usando a combinação certa de SQL e R para processamento de dados e tarefas analíticas diferentes, desenvolvedores e cientistas de dados podem ser mais produtivos.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-data-transformation-and-automation"></a>Usar o SSIS para automação e a transformação de dados

Fluxos de trabalho de ciência de dados são altamente iterativos e envolvem muita transformação de dados, incluindo dimensionamento, agregações, cálculo de probabilidades, renomeação e mesclagem de atributos. Os cientistas de dados estão acostumados a fazer muitas dessas tarefas em R, Python ou outra linguagem; contudo, a execução desses fluxos de trabalho em dados empresariais requer integração perfeita com processos e ferramentas de ETL.

Como o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite que você execute operações complexas em R por meio do Transact-SQL e de procedimentos armazenados, é possível integrar tarefas específicas de R a processos de ETL existentes sem o mínimo trabalho de novo desenvolvimento. Em vez disso, executar uma cadeia de tarefas intensivo de memória em R, preparação de dados pode ser otimizada usando as ferramentas mais eficientes, incluindo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Aqui estão algumas ideias de como você pode automatizar o processamento de dados e pipelines de modelagem usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tarefas para criar recursos de dados necessários no banco de dados SQL
+ Usar ramificação condicional para alternar o contexto de computação para trabalhos em R
+ Executar trabalhos do R que geram seus próprios dados no banco de dados e compartilhar dados com aplicativos
+ Ao usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], carregar o script R salvo em uma variável de texto e executá-lo no SQL Server

## <a name="ssis-example"></a>Exemplo do SSIS

O exemplo a seguir é proveniente de uma postagem de blog do MSDN já aposentado criada por Jimmy Wong nesta URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`.

Este exemplo mostra como automatizar tarefas usando o SSIS. Criar procedimentos armazenados com o R inserido usando o SQL Server Management Studio e, em seguida, executar esses procedimentos armazenados do [tarefas de T-SQL Execute](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) em um pacote SSIS.

Para percorrer este exemplo, você deve estar familiarizado com o Management Studio, SSIS, SSIS Designer, design de pacote e T-SQL. O pacote do SSIS usa três [tarefas de T-SQL Execute](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) que inserir dados de treinamento em uma tabela, os dados de modelo e pontuar os dados para obter uma saída de previsão.

### <a name="create-tables"></a>Criar tabelas

Execute o seguinte script no SQL Server Management Studio para criar algumas tabelas: uma para armazenar os dados e outro para armazenar um modelo. A função da tabela ssis_iris é atuar como dados de treinamento em um cenário de operacionalização. 

```T-SQL
Use irissql
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

### <a name="create-a-stored-procedure-that-loads-training-data"></a>Criar um procedimento armazenado que carrega os dados de treinamento

Esse script cria um procedimento armazenado que carrega íris em um quadro de dados usando o conjunto de dados interno do R.

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

### <a name="define-an-execute-sql-task-that-refreshes-the-model"></a>Definir uma tarefa Executar SQL que atualiza o modelo

No Designer SSIS, crie uma [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task).

![Inserir dados](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "inserir dados")

O script para SQLStatement é da seguinte maneira. O script remove dados existentes e, em seguida, recarrega novos dados usando o **load_iris** procedimento armazenado criado na etapa anterior.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

### <a name="create-a-stored-procedure-that-generates-a-model"></a>Criar um procedimento armazenado que gera um modelo

Esse procedimento armazenado é o código que cria um modelo linear usando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Bibliotecas de RevoScaleR e revoscalepy são carregadas automaticamente nas sessões de R e Python no SQL Server.

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

### <a name="define-an-execute-sql-task-that-runs-the-model-generation-stored-procedure"></a>Definir uma tarefa Executar SQL que executa o procedimento armazenado de geração de modelo

Nesta etapa, [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) executa o **generate_iris_rx_model** procedimento armazenado, criando o modelo e inseri-los na tabela ssis_iris_models.

![Gera um modelo linear](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "gera um modelo linear")

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

Depois de concluir essa tarefa, você pode consultar o ssis_iris_models para ver que ele contém um modelo binário.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Prever resultados (pontuação) usando o modelo "treinado"

Neste exemplo simples, a suposição é que ssis_iris_model é um modelo treinado. Como é a finalidade de um modelo treinado gerar previsões, agora estamos prontos para executar uma previsão usando ele. 

Para fazer isso, coloque o script R na consulta SQL para disparar a [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) função R interna em ssis_iris_model. Um procedimento armazenado no SQL Server chamado **predict_species_length** realiza essa tarefa.

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

### <a name="define-an-execute-sql-task-that-predicts-outcomes"></a>Definir uma tarefa Executar SQL que prevê os resultados

Usando o [tarefa Executar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task), execute o **predict_species_length** procedimento armazenado para gerar o comprimento da pétala previsto.

![Gerar previsões](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "gerar previsões")

```T-SQL
exec predict_species_length 'rxLinMod';
```

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