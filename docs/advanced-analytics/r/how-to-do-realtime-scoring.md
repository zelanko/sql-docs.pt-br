---
title: "Como realizar em tempo real de pontuação ou pontuação nativo no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 175a9bc664a2032d828ca790312920339f971b9b
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="how-to-perform-realtime-scoring-or-native-scoring-in-sql-server"></a>Como realizar em tempo real de pontuação ou pontuação nativo no SQL Server

Este tópico fornece instruções e código de exemplo de como executar a pontuação em tempo real e recursos nativos de pontuação em 2017 do SQL Server e SQL Server 2016. O objetivo de pontuação em tempo real e pontuação nativo é melhorar o desempenho das operações de pontuação em lotes pequenos.

Tanto em tempo real de pontuação e nativo de pontuação são projetados para permitir o uso de uma máquina de modelo de aprendizado sem a necessidade de instalar o R. Tudo o que você precisa fazer é obter um modelo pré-treinado em um formato compatível e salvá-la em um banco de dados do SQL Server.

## <a name="choosing-a-scoring-method"></a>Escolhendo um método de pontuação

As opções a seguir têm suporte para previsão de lote rápida:

+ **Pontuação nativo**: função PREVER T-SQL no SQL Server 2017
+ **Em tempo real de pontuação**: usando o sp\_rxPredict o procedimento armazenado no SQL Server 2016 ou 2017 do SQL Server.

> [!NOTE]
> Uso da função de previsão é recomendado em 2017 do SQL Server.
> Para usar sp\_rxPredict requer que você habilitar a integração do SQLCLR. Considere as implicações de segurança antes de habilitar essa opção.

O processo geral de preparar o modelo e, em seguida, gerar pontuações é muito semelhante:

1. Crie um modelo usando um algoritmo com suporte.
2. Serialize o modelo usando um formato binário especial.
3. Tornar o modelo disponível para o SQL Server. Normalmente, isso significa armazenar o modelo serializado em uma tabela do SQL Server.
4. Chame a função ou procedimento armazenado e passar o modelo e dados de entrada.

### <a name="requirements"></a>Requisitos

+ A função de previsão está disponível em todas as edições do SQL Server 2017 e é habilitada por padrão. Você não precisa instalar o R ou habilitar recursos adicionais.

+ Se usar sp\_rxPredict, algumas etapas adicionais são necessárias. Consulte [habilitar em tempo real de pontuação](#bkmk_enableRtScoring).

+ Neste momento, apenas RevoScaleR e MicrosoftML podem criar modelos compatíveis. Tipos de modelo adicionais podem ser disponibilizados no futuro. Para obter a lista dos algoritmos com suporte no momento, consulte [em tempo real de pontuação](../real-time-scoring.md).

### <a name="serialization-and-storage"></a>Serialização e armazenamento

Para usar um modelo com uma das opções de classificação rápidas, o modelo deve ser salvo em um formato serializado especial, que foi otimizado para o tamanho e a eficiência de pontuação.

+ Chamar `rxSerializeModel` para gravar um modelo com suporte para o **bruto** formato.
+ Chamar `rxUnserializeModel` para reconstituir o modelo para uso em outro código de R, ou para exibir o modelo.

Para obter mais informações, consulte [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel).

**Usando o SQL**

Código de SQL, você pode treinar o modelo usando `sp_execute_external_script`e insira os modelos treinados diretamente em uma tabela, em uma coluna do tipo **varbinary (max)**.

Para obter um exemplo simple, consulte [este tutorial](../tutorials/rtsql-create-a-predictive-model-r.md)

**Usando o R**

Código de R, há duas maneiras de salvar o modelo em uma tabela:

+ Chamar o `rxWriteObject` função, do pacote RevoScaleR, para gravar o modelo diretamente para o banco de dados.

  O `rxWriteObject()` função pode recuperar objetos de R de uma fonte de dados ODBC como o SQL Server ou gravar objetos do SQL Server. A API é modelada de um repositório de chave-valor simple.
  
  Se você usar essa função, certifique-se de serialize o modelo usando a nova função de serialização primeiro. Em seguida, defina o *serializar* sinalizador em `rxWriteObject` como FALSE, para evitar repetir a etapa de serialização.

+ Você pode também salvar o modelo em formato bruto em um arquivo e, em seguida, ler o arquivo no SQL Server. Essa opção pode ser útil se você estiver movendo ou copiando modelos entre ambientes.

## <a name="native-scoring-with-predict"></a>Nativo com previsão de pontuação

Neste exemplo, você cria um modelo e, em seguida, chame a função de previsão em tempo real do T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Etapa 1. Preparar e salvar o modelo

Execute o seguinte código para criar o banco de dados de exemplo e as tabelas necessárias.

```SQL
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

Use a seguinte instrução para popular a tabela de dados com dados do **íris** conjunto de dados.

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Agora, crie uma tabela para armazenar modelos.

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

O código a seguir cria um modelo baseado no **íris** conjunto de dados e salva-o para a tabela de modelos.

```SQL
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> Você deve usar o [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) RevoScaleR para salvar o modelo de função. O padrão R `serialize` função não é possível gerar o formato necessário.

Você pode executar uma instrução como a seguir para exibir o modelo armazenado em formato binário:

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Etapa 2. Executar previsão no modelo

A seguinte instrução de previsão simples obtém uma classificação do modelo de árvore de decisão usando o **pontuação nativo** função. Ele prevê a espécie de íris com base em atributos que você fornecer, comprimento pétala e largura.

```SQL
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

Se você receber o erro, "Erro durante a execução da função de previsão. Modelo está corrompido ou inválido", isso normalmente significa que a consulta não retornou um modelo. Verifique se você digitou o nome do modelo corretamente ou se a modelos de tabela está vazio.

> [!NOTE]
> Como as colunas e os valores retornados por **PREVER** pode variar por tipo de modelo, você deve definir o esquema dos dados retornados usando uma **WITH** cláusula.

## <a name="realtime-scoring-with-sprxpredict"></a>Em tempo real com sp_rxPredict de pontuação

Esta seção descreve as etapas necessárias para configurar o **em tempo real** previsão e fornece um exemplo de como chamar a função do T-SQL.

### <a name ="bkmk_enableRtScoring"></a>Etapa 1. Habilitar o procedimento de pontuação em tempo real

Você deve habilitar esse recurso para cada banco de dados que você deseja usar para pontuação. O administrador do servidor deve executar o utilitário de linha de comando, RegisterRExt.exe, que é incluído com o pacote RevoScaleR.

> [!NOTE]
> Em ordem de pontuação para trabalhar e em tempo real, a funcionalidade de SQL CLR precisa ser habilitado na instância e o banco de dados precisa ser marcado como confiável. Quando você executa o script, essas ações são executadas para você. No entanto, você deve considerar as implicações de segurança adicional.

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta onde RegisterRExt.exe está localizado. O caminho a seguir pode ser usado em uma instalação padrão:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Execute o seguinte comando, substituindo o nome da sua instância e o banco de dados de destino em que você deseja habilitar os procedimentos armazenados estendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por exemplo, para adicionar o procedimento armazenado estendido para o banco de dados CLRPredict na instância padrão, digite:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    O nome da instância é opcional se o banco de dados na instância padrão. Se você estiver usando uma instância nomeada, especifique o nome da instância.

3. RegisterRExt.exe cria os seguintes objetos:

    + Assemblies confiáveis
    + O procedimento armazenado`sp_rxPredict`
    + Uma nova função de banco de dados, `rxpredict_users`. O administrador de banco de dados pode usar essa função para conceder permissão aos usuários que usam a funcionalidade de pontuação em tempo real.

4. Adicionar todos os usuários que precisam executar `sp_rxPredict` à nova função.

> [!NOTE]
> 
> No SQL Server de 2017, medidas adicionais de segurança estão em vigor para evitar problemas com a integração CLR. Essas medidas impõem restrições adicionais sobre o uso desse procedimento armazenado também.

### <a name="step-2-prepare-and-save-the-model"></a>Etapa 2. Preparar e salvar o modelo

O formato binário exigido pelo sp\_rxPredict é o mesmo que para PREVER. Portanto, no seu código R, inclui uma chamada para [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)e certifique-se de especificar _realtimeScoringOnly_ = TRUE, como neste exemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Etapa 3. Chamar sp_rxPredict

Você pode chamar sp\_rxPredict como você faria com qualquer outro procedimento armazenado. Na versão atual, o procedimento armazenado usa apenas dois parâmetros:  _@model_  para o modelo em formato binário, e  _@inputData_  para os dados a serem usados na pontuação, definido como uma consulta SQL válida .

Como o formato binário é o mesmo que é usado pela função de previsão, você pode usar a tabela de modelos e dados do exemplo anterior.

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree.model' AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> A chamada para sp\_rxPredict falhará se os dados de entrada para pontuação não incluem colunas que correspondem aos requisitos do modelo. Atualmente, apenas os seguintes tipos de dados .NET têm suporte: double, float, short, ushort, long, ulong e cadeia de caracteres.
> 
> Portanto, talvez seja necessário filtrar tipos sem suporte em seus dados de entrada antes de usá-lo para a pontuação em tempo real.
> 
> Para obter informações sobre tipos SQL correspondentes, consulte [mapeamento de tipo CLR SQL](https://msdn.microsoft.com/library/bb386947.aspx) ou [mapeamento de dados de parâmetro CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-realtime-scoring"></a>Desabilitar a pontuação em tempo real

Para desabilitar a funcionalidade de pontuação em tempo real, abra um prompt de comando com privilégios elevados e execute o seguinte comando:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="realtime-scoring-in-microsoft-r-server-or-machine-learning-server"></a>Em tempo real de pontuação no Microsoft R Server ou o servidor de aprendizado de máquina

Servidor de aprendizado de máquina dá suporte a distribuídas em tempo real de pontuação de modelos publicados como um serviço web. Para obter mais informações, consulte estes tópicos:

+ [Quais são os serviços web no servidor de aprendizado de máquina?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [O que é operacionalização?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Implantar um modelo de Python como um serviço web com sdk azureml-modelo-management](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar um modelo em tempo real ou um bloco de código de R como um novo serviço da web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [pacote de mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
