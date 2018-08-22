---
title: Como executar pontuação em tempo real ou pontuação nativa no aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dfea308f268d666ce070c21a7dd9afa513f95406
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40395223"
---
# <a name="how-to-perform-real-time-scoring-or-native-scoring-in-sql-server"></a>Como executar pontuação em tempo real ou pontuação nativa no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo demonstra duas abordagens no SQL Server para prever resultados em quase tempo real usando modelos previamente treinados escritos em R. Tanto a pontuação em tempo real como a pontuação nativa são projetados para permitir que você use um modelo do machine learning sem a necessidade de instalar o R. Considerando um modelo previamente treinado em um formato compatível com - salvo em um banco de dados do SQL Server - você pode usar técnicas de acesso a dados padrão para gerar rapidamente as pontuações de previsão sobre novas entradas.

## <a name="choose-a-scoring-method"></a>Escolha um método de classificação

As opções a seguir têm suporte para previsão de lote rápida:

+ **Pontuação nativa**: a função PREDICT de T-SQL no banco de dados SQL, SQL Server 2017 Linux e Windows do SQL Server 2017.
+ **Pontuação em tempo real**: usando o sp\_rxPredict o procedimento armazenado no SQL Server 2016 ou SQL Server 2017 (somente Windows).

> [!NOTE]
> Recomenda-se o uso da função PREDICT no SQL Server 2017.
> Usar sp\_rxPredict requer que você habilitar a integração do SQLCLR. Considere as implicações de segurança antes de você habilitar essa opção.

O processo geral de preparar o modelo e, em seguida, gerar pontuações é semelhante:

1. Crie um modelo usando um algoritmo com suporte.
2. Serialize o modelo usando um formato binário especial.
3. Tornar o modelo disponível para o SQL Server. Normalmente, isso significa armazenar o modelo serializado em uma tabela do SQL Server.
4. Chame a função ou procedimento armazenado e passar o modelo e dados de entrada.

### <a name="requirements"></a>Requisitos

+ A função PREDICT está disponível em todas as edições do SQL Server 2017 e é habilitada por padrão. Você não precisa instalar o R ou habilitar recursos adicionais.

+ Se usar sp\_rxPredict, algumas etapas adicionais são necessárias. Ver [habilitar a pontuação em tempo real](#bkmk_enableRtScoring).

+ Neste momento, somente o RevoScaleR e o MicrosoftML podem criar modelos compatíveis. Tipos de modelo adicionais podem ser disponibilizados no futuro. Para obter a lista dos algoritmos com suporte no momento, consulte [pontuação em tempo real](../real-time-scoring.md).

### <a name="serialization-and-storage"></a>Serialização e armazenamento

Para usar um modelo com qualquer uma das opções rápidas de pontuação, salve o modelo usando um formato serializado especial, que foi otimizado para o tamanho e a eficiência de pontuação.

+ Chame `rxSerializeModel` escrever um modelo com suporte para o **brutos** formato.
+ Chamar `rxUnserializeModel` para reconstituir o modelo para uso em outro código de R ou para exibir o modelo.

Para obter mais informações, consulte [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel).

**Usando o SQL**

No código SQL, você pode treinar o modelo usando `sp_execute_external_script`e inserir diretamente os modelos treinados em uma tabela, em uma coluna do tipo **varbinary (max)**.

Para obter um exemplo simple, consulte [neste tutorial](../tutorials/rtsql-create-a-predictive-model-r.md)

**Usando o R**

No código R, há duas maneiras de salvar o modelo em uma tabela:

+ Chamar o `rxWriteObject` função, do pacote RevoScaleR, gravar o modelo diretamente no banco de dados.

  O `rxWriteObject()` função pode recuperar objetos de R de uma fonte de dados ODBC como o SQL Server ou gravar objetos do SQL Server. A API é modelada de um repositório de chave-valor simples.
  
  Se você usar essa função, certifique-se de que serialize o modelo usando a nova função de serialização primeiro. Em seguida, defina as *serializar* argumento em `rxWriteObject` como FALSE, para evitar repetir a etapa de serialização.

+ Você pode também salvar o modelo em formato bruto em um arquivo e, em seguida, ler o arquivo para o SQL Server. Essa opção pode ser útil se você estiver movendo ou copiando modelos entre ambientes.

## <a name="native-scoring-with-predict"></a>Pontuação com PREDICT nativa

Neste exemplo, você deve cria um modelo e, em seguida, chame a função de previsão em tempo real do T-SQL.

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

Use a seguinte instrução para popular a tabela de dados com os dados do **iris** conjunto de dados.

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

O código a seguir cria um modelo baseado na **íris** conjunto de dados e salva-à tabela denominada **modelos**.

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
> Certifique-se de usar o [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) função do RevoScaleR para salvar o modelo. O padrão do R `serialize` função não é possível gerar o formato necessário.

Você pode executar uma instrução a seguir para exibir o modelo armazenado em formato binário:

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Etapa 2. Executar previsão no modelo

A seguinte instrução de previsão simple obtém uma classificação do modelo de árvore de decisão usando o **pontuação nativa** função. Ele prevê a espécie de íris com base em atributos que você fornecer, comprimento da pétala e largura.

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

Se você receber o erro, "Erro durante a execução da função PREDICT. Modelo está corrompido ou inválido", isso normalmente significa que sua consulta não retornou um modelo. Verifique se você digitou o nome do modelo corretamente ou se a tabela de modelos está vazia.

> [!NOTE]
> Como as colunas e valores retornados por **PREDICT** pode variar por tipo de modelo, você deve definir o esquema dos dados retornados usando uma **WITH** cláusula.

## <a name="real-time-scoring-with-sprxpredict"></a>Pontuação com sp_rxPredict em tempo real

Esta seção descreve as etapas necessárias para configurar **em tempo real** previsão e fornece um exemplo de como chamar a função de T-SQL.

### <a name ="bkmk_enableRtScoring"></a> Etapa 1. Habilitar o procedimento de pontuação em tempo real

Você deve habilitar esse recurso para cada banco de dados que você deseja usar para pontuação. O administrador do servidor deve executar o utilitário de linha de comando, RegisterRExt.exe, que está incluído no pacote RevoScaleR.

> [!NOTE]
> Para a pontuação em tempo real para funcionar, funcionalidade de SQL CLR precisa ser habilitado na instância; Além disso, o banco de dados precisa ser marcado como confiável. Quando você executar o script, essas ações são executadas para você. No entanto, considere as implicações de segurança adicionais antes de fazer isso!

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta onde se encontra RegisterRExt.exe. O caminho a seguir pode ser usado em uma instalação padrão:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Execute o seguinte comando, substituindo o nome da sua instância e o banco de dados de destino no qual você deseja habilitar os procedimentos armazenados estendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por exemplo, para adicionar o procedimento armazenado estendido para o banco de dados CLRPredict na instância padrão, digite:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    O nome da instância é opcional se o banco de dados na instância padrão. Se você estiver usando uma instância nomeada, você deve especificar o nome da instância.

3. RegisterRExt.exe cria os seguintes objetos:

    + Assemblies confiáveis
    + O procedimento armazenado `sp_rxPredict`
    + Uma nova função de banco de dados, `rxpredict_users`. O administrador de banco de dados pode usar essa função para conceder permissão aos usuários que usam a funcionalidade de pontuação em tempo real.

4. Adicionar quaisquer usuários que precisam executar `sp_rxPredict` à nova função.

> [!NOTE]
> 
> No SQL Server 2017, as medidas de segurança adicionais estão em vigor para evitar problemas com a integração CLR. Essas medidas impõem restrições adicionais sobre o uso desse procedimento armazenado também. 

### <a name="step-2-prepare-and-save-the-model"></a>Etapa 2. Preparar e salvar o modelo

O formato binário exigido pelo sp\_rxPredict é o mesmo que o formato necessário para usar a função PREDICT. Portanto, no seu código R, incluir uma chamada para [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)e não se esqueça de especificar `realtimeScoringOnly = TRUE`, como neste exemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Etapa 3. Chamar sp_rxPredict

Você pode chamar sp\_rxPredict como você faria com qualquer outro procedimento armazenado. Na versão atual, o procedimento armazenado usa apenas dois parâmetros:  _\@modelo_ para o modelo em formato binário, e  _\@inputData_ para os dados a serem usados na pontuação, definido como uma consulta SQL válida.

Como o formato binário é o mesmo que é usado pela função de previsão, você pode usar a tabela de dados e modelos do exemplo anterior.

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> A chamada para sp\_rxPredict falhará se os dados de entrada para pontuação não incluem colunas que correspondem aos requisitos do modelo. Atualmente, somente os seguintes tipos de dados de .NET têm suporte: double, float, short, ushort, long, ulong e cadeia de caracteres.
> 
> Portanto, você talvez precise filtrar os tipos sem suporte em seus dados de entrada antes de usá-lo para pontuação em tempo real.
> 
> Para obter informações sobre tipos SQL correspondentes, consulte [mapeamento de tipo de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [Mapeando dados de parâmetro CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Desabilitar a pontuação em tempo real

Para desabilitar a funcionalidade de pontuação em tempo real, abra um prompt de comando com privilégios elevados e execute o seguinte comando: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="real-time-scoring-in-other-microsoft-product"></a>Pontuação em tempo real em outros produtos da Microsoft

Se você estiver usando um servidor autônomo ou um Microsoft Machine Learning Server em vez de análise do SQL Server no banco de dados, você tem outras opções além de procedimentos armazenados e funções de T-SQL para gerar previsões.

O servidor autônomo e o Machine Learning Server suportam o conceito de um *serviço web* para implantação de código. Você pode agrupar um R ou Python modelo previamente treinado como um serviço web, chamado em tempo de execução para avaliar as novas entradas de dados. Para obter mais informações, consulte estes tópicos:

+ [Quais são os serviços web no Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [O que é operacionalização?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Implantar um modelo de Python como um serviço web com o azureml-modelo-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar um modelo em tempo real ou um bloco de código do R como um novo serviço web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [pacote mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
