---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 8800df26e505f1fffe25e6f65218481e7a8158f0
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663012"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
O **procedimento armazenado sp_execute_external_script** executa um script fornecido como um argumento de entrada para o procedimento, e é usado com [Serviços de Aprendizagem de Máquina](../../machine-learning/index.yml) e [Extensões de Linguagem](../../language-extensions/language-extensions-overview.md). 

Para serviços de aprendizagem de máquina, [Python](../../machine-learning/concepts/extension-python.md) e [R](../../machine-learning/concepts/extension-r.md) são linguagens suportadas. Para extensões de idioma, java é suportado, mas deve ser definido com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md).

Para executar **sp_execute_external_script,** primeiro você deve instalar serviços de aprendizagem de máquina ou extensões de idioma. Para obter mais informações, consulte [Instale o SQL Server Machine Learning Services (Python e R) no Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md) e [Linux,](../../linux/sql-server-linux-setup-machine-learning.md)ou [instale extensões de linguagem do SQL Server no Windows](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) e [Linux](../../linux/sql-server-linux-setup-language-extensions.md).
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
O **procedimento armazenado sp_execute_external_script** executa um script fornecido como um argumento de entrada para o procedimento e é usado com [Serviços de Aprendizado de Máquina](../../machine-learning/index.yml) no SQL Server 2017. 

Para serviços de aprendizagem de máquina, [Python](../../machine-learning/concepts/extension-python.md) e [R](../../machine-learning/concepts/extension-r.md) são linguagens suportadas. 

Para executar **sp_execute_external_script,** primeiro você deve instalar serviços de aprendizado de máquina. Para obter mais informações, consulte [Instale o SQL Server Machine Learning Services (Python e R) no Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md).
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
O procedimento armazenado **sp_execute_external_script** executa um script fornecido como um argumento de entrada para o procedimento e é usado com [Serviços R](../../machine-learning/r/sql-server-r-services.md) no SQL Server 2016.

Para Serviços R, [R](../../machine-learning/concepts/extension-r.md) é a linguagem suportada.

Para executar **sp_execute_external_script,** primeiro você deve instalar Serviços R. Para obter mais informações, consulte [Instale o SQL Server Machine Learning Services (Python e R) no Windows](../../machine-learning/install/sql-r-services-windows-install.md).
::: moniker-end

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>Sintaxe

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>Sintaxe para 2017 e anterior

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>Argumentos
 linguagem = N '*língua*' ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 Indica a linguagem do script. *linguagem* é **sysname**. Os valores válidos são **R,** **Python**e qualquer linguagem definida com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) (por exemplo, Java).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 Indica a linguagem do script. *linguagem* é **sysname**. No SQL Server 2017, os valores válidos são **R** e **Python**.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 Indica a linguagem do script. *linguagem* é **sysname**. No SQL Server 2016, o único valor válido é **R**.
::: moniker-end

 script = N'*script*' Script de linguagem externa especificado como uma entrada literal ou variável. ** \@** *script* é **nvarchar(max)**.  

`[ @input_data_1 =  N'input_data_1' ]`Especifica os dados de entrada usados pelo [!INCLUDE[tsql](../../includes/tsql-md.md)] script externo na forma de uma consulta. O tipo *de* input_data_1 é **nvarchar(max)**.

`[ @input_data_1_name = N'input_data_1_name' ]`Especifica o nome da variável usada para representar @input_data_1a consulta definida por . O tipo de dados da variável no script externo depende da linguagem. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. *input_data_1_name* é **sysname.**  O valor padrão é *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`Usado para construir modelos por partição. Especifica o nome da coluna usada para ordenar o conjunto de resultados, por exemplo, pelo nome do produto. O tipo de dados da variável no script externo depende da linguagem. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`Usado para construir modelos por partição. Especifica o nome da coluna usada para segmentar dados, como região geográfica ou data. O tipo de dados da variável no script externo depende da linguagem. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`Especifica o nome da variável no script externo que contém [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os dados a serem retornados após a conclusão da chamada do procedimento armazenado. O tipo de dados da variável no script externo depende da linguagem. Para R, a saída deve ser um quadro de dados. Para Python, a saída deve ser um quadro de dados pandas. *output_data_1_name* é **sysname.**  O valor padrão é *OutputDataSet*.  

`[ @parallel = 0 | 1 ]`Habilite a execução paralela `@parallel` de scripts R definindo o parâmetro como 1. O padrão para este parâmetro é 0 (sem paralelismo). Se `@parallel = 1` e a saída estiver sendo transmitida diretamente `WITH RESULT SETS` para a máquina cliente, então a cláusula é necessária e um esquema de saída deve ser especificado.  

 + Para scripts R que não usam funções RevoScaleR, o uso do parâmetro pode ser benéfico para o `@parallel` processamento de grandes conjuntos de dados, assumindo que o script pode ser rotineiro paraparaliado. Por exemplo, ao `predict` usar a função R com `@parallel = 1` um modelo para gerar novas previsões, definir como uma dica para o mecanismo de consulta. Se a consulta puder ser paralelenada, as linhas serão distribuídas de acordo com a configuração **MAXDOP.**  
  
 + Para scripts R que usam funções RevoScaleR, o processamento paralelo `@parallel = 1` é tratado automaticamente e você não deve especificar para a **chamada sp_execute_external_script.**  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`Uma lista de declarações de parâmetro de entrada que são usadas no script externo.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`Uma lista de valores para os parâmetros de entrada usados pelo script externo.  

## <a name="remarks"></a>Comentários

> [!IMPORTANT]
> A árvore de consulta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é controlada por e os usuários não podem executar operações arbitrárias na consulta. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Use **sp_execute_external_script** para executar scripts escritos em um idioma suportado. As linguagens suportadas são **Python** e **R** usadas com Serviços de Aprendizagem de Máquina, e qualquer linguagem definida com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) (por exemplo, Java) usada com extensões de linguagem.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Use **sp_execute_external_script** para executar scripts escritos em um idioma suportado. Os idiomas suportados são **Python** e **R** no SQL Server 2017 Machine Learning Services.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Use **sp_execute_external_script** para executar scripts escritos em um idioma suportado. O único idioma suportado é **O R** no SQL Server 2016 R Services.
::: moniker-end

Por padrão, os conjuntos de resultados retornados por este procedimento armazenado são desaída com colunas não nomeadas. Os nomes das colunas usadas dentro de um script são locais para o ambiente de scripting e não são refletidos no conjunto de resultados desaída. Para nomear colunas de `WITH RESULT SET` conjunto [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)de resultados, use a cláusula de .

Além de retornar um conjunto de resultados, você [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode retornar valores escalares para usando parâmetros OUTPUT. 
  
Você pode controlar os recursos usados por scripts externos configurando um pool de recursos externo. Para obter mais informações, consulte [CRIAR POOL DE RECURSOS EXTERNOs &#40;o Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informações sobre a carga horária podem ser obtidas a partir do catálogo de visualizações do catálogo de recursos, do Detran e dos contadores. Para obter mais informações, consulte [Visualizações do catálogo do governador de recursos &#40;transact-SQL&#41;, visualizações ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) [de gerenciamento dinâmico relacionadas ao governador de recursos &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [SQL Server, External Scripts Object](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorar a execução do script

Monitore a execução do script usando [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parâmetros para modelagem de partição

Você pode definir dois parâmetros adicionais que permitem a modelagem em dados particionados, onde as partições são baseadas em uma ou mais colunas que você fornece que segmentam naturalmente um conjunto de dados em partições lógicas criadas e usadas apenas durante a execução do script. Colunas que contêm valores repetitivos para idade, sexo, região geográfica, data ou hora, são alguns exemplos que se prestam a conjuntos de dados particionados.
 
Os dois parâmetros são **input_data_1_partition_by_columns** e **input_data_1_order_by_columns,** onde o segundo parâmetro é usado para ordenar o conjunto de resultados. Os parâmetros são passados como entradas para `sp_execute_external_script` com o script externo executando uma vez para cada partição. Para obter mais informações e exemplos, consulte [Tutorial: Crie modelos baseados em partição](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition).

Você pode executar o script `@parallel=1`em paralelo especificando . Se a consulta de entrada puder ser `@parallel=1` paralelamente, você `sp_execute_external_script`deve definir como parte de seus argumentos para . Por padrão, o otimizador de `@parallel=1` consulta opera em tabelas com mais de 256 linhas, mas se você quiser lidar com isso explicitamente, este script inclui o parâmetro como uma demonstração.

> [!Tip]
> Para treinar cargas de trabalho, use `@parallel` com qualquer script de treinamento arbitrário, mesmo aqueles que usam algoritmos não Microsoft Rx. Normalmente, somente os algoritmos do RevoScaleR (com o prefixo rx) oferecem paralelismo em cenários de treinamento no SQL Server. Mas com os novos parâmetros no SQL Server vNext, você pode paralelenear um script que chama funções não especificamente projetadas com esse recurso.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Execução de streaming para scripts Python e R  

O streaming permite que o script Python ou R trabalhe com mais dados do que pode caber na memória. Para controlar o número de linhas passadas durante o streaming, `@r_rowsPerRead` especifique um valor inteiro para o parâmetro, na `@params` coleção.  Por exemplo, se você estiver treinando um modelo que usa dados muito amplos, você pode ajustar o valor para ler menos linhas, para garantir que todas as linhas possam ser enviadas em um pedaço de dados. Você também pode usar esse parâmetro para gerenciar o número de linhas que estão sendo lidas e processadas de uma só vez, para mitigar problemas de desempenho do servidor. 
  
Tanto `@r_rowsPerRead` o parâmetro para `@parallel` o streaming quanto o argumento devem ser considerados sugestões. Para que a dica seja aplicada, deve ser possível gerar um plano de consulta SQL que inclua processamento paralelo. Se isso não for possível, o processamento paralelo não pode ser habilitado.  
  
> [!NOTE]  
> Streaming e processamento paralelo são suportados apenas no Enterprise Edition. Você pode incluir os parâmetros em suas consultas no Standard Edition sem levantar um erro, mas os parâmetros não têm efeito e os scripts R são executados em um único processo.  
  
## <a name="restrictions"></a>Restrições  

### <a name="data-types"></a>Tipos de dados

Os seguintes tipos de dados não são suportados quando usados na consulta de entrada ou parâmetros de **sp_execute_external_script** procedimento e retornam um erro de tipo não suportado.  

Como solução de solução, **CAST** a coluna ou [!INCLUDE[tsql](../../includes/tsql-md.md)] valor para um tipo suportado antes de enviá-lo para o script externo.  
  
-   **Cursor**  
  
-   **Timestamp**  
  
-   **datetime2**, **datetimeoffset**, **hora**  
  
-   **Sql_variant**  
  
-   **texto,** **imagem**  
  
-   **xml**  
  
-   **hierarquia,** **geometria,** **geografia**  
  
-   Tipos definidos pelo usuário de CLR

Em geral, qualquer conjunto de resultados [!INCLUDE[tsql](../../includes/tsql-md.md)] que não possa ser mapeado para um tipo de dados, é output as NULL.  

### <a name="restrictions-specific-to-r"></a>Restrições específicas para R

Se a entrada incluir valores **de data-hora** que não se encaixam na faixa de valores admissível em R, os valores serão convertidos em **NA**. Isso é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necessário porque permite uma gama maior de valores do que é suportado na língua R.

Os valores flutuantes `-Inf` `NaN`(por exemplo, `+Inf` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ) não são suportados, embora ambas as línguas usem o IEEE 754. O comportamento atual apenas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia os valores diretamente; como resultado, o cliente SQL em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] lança um erro. Portanto, esses valores são convertidos em **NULOS**.

## <a name="permissions"></a>Permissões

Requer **executar qualquer permissão de** banco de dados DE SCRIPT EXTERNO.  

## <a name="examples"></a>Exemplos

Esta seção contém exemplos de como este procedimento armazenado pode [!INCLUDE[tsql](../../includes/tsql-md.md)]ser usado para executar scripts R ou Python usando .

### <a name="a-return-an-r-data-set-to-sql-server"></a>a. Retornar um conjunto de dados R para o SQL Server  

O exemplo a seguir cria **sp_execute_external_script** um procedimento armazenado que usa sp_execute_external_script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para retornar o conjunto de dados Iris incluído com R para .  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Gerar um modelo R com base em dados do SQL Server  

O exemplo a seguir cria **sp_execute_external_script** um procedimento armazenado que usa sp_execute_external_script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para gerar um modelo de íris e devolver o modelo para .  

> [!NOTE]
>  Este exemplo requer a instalação antecipada do pacote e1071. Para obter mais informações, consulte [Instalar pacotes R adicionais no SQL Server](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md).

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Para gerar um modelo semelhante usando Python, altere o identificador de idioma de `@language=N'R'` para `@language = N'Python'`e faça as modificações necessárias para o argumento `@script`. Caso contrário, todos os parâmetros funcionam do mesmo modo que para o R.

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Criar um modelo de Python e gerar pontuações com base nele

Este exemplo ilustra como usar sp\_execute\_external\_script para gerar pontuações em um modelo simples de Python. 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Os títulos de coluna usados no código Python não são de saída para o SQL Server; portanto, use a declaração WITH RESULT para especificar os nomes da coluna e os tipos de dados para sql a usar.

Para pontuação, você também pode usar a função nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que é normalmente mais rápida porque evita que o runtime do Python ou do R seja chamado.

## <a name="see-also"></a>Confira também

+ [Serviços de Machine Learning do SQL Server](../../machine-learning/index.yml)
+ [Extensões de linguagem do servidor SQL](../../language-extensions/language-extensions-overview.md). 
+ [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Bibliotecas python e tipos de dados](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [Bibliotecas R e Tipos de Dados R](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [Serviços SQL Server R](../../machine-learning/r/sql-server-r-services.md)   
+ [Problemas conhecidos para serviços de aprendizado de máquina do servidor SQL](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [CRIAR BIBLIOTECA EXTERNA &#40;&#41;Transact-SQL](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;&#41;SQL transact](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [Opção external scripts enabled de configuração de servidor](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, objeto Scripts Externos](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
