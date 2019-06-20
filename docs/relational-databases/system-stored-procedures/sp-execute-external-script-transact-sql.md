---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 77d5386f05e371a2e653f4f6097257e99457e910
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046717"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Executa um script fornecido como um argumento de entrada para o procedimento. Script é executado na [estrutura de extensibilidade](../../advanced-analytics/concepts/extensibility-framework.md). Script deve ser escrito em uma linguagem registrada e com suporte, em um mecanismo de banco de dados que tenha pelo menos uma extensão: [**R**](../../advanced-analytics/concepts/extension-r.md), [ **Python**](../../advanced-analytics/concepts/extension-python.md), ou [ **Java** (no SQL Server 2019 somente visualização)](../../advanced-analytics/java/extension-java.md). 

Para executar **sp_execute_external_script**, você deve primeiro habilitar scripts externos por meio da instrução `sp_configure 'external scripts enabled', 1;`.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> Aprendizado de máquina (R e Python) e extensões de programação é instalada como um complemento para a instância do mecanismo de banco de dados. Suporte para extensões específicas variam de acordo com a versão do SQL Server.

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
::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>Sintaxe para 2017 e versões anteriores

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
 **@language** = N'*language*'  
 Indica a linguagem de script. *linguagem* está **sysname**.  Dependendo da sua versão do SQL Server, os valores válidos são R (SQL Server 2016 e posterior), (SQL Server 2017 e posterior) do Python e Java (versão prévia do SQL Server 2019). 
  
 **@script** = N'*script*' especificado como uma entrada de literal ou uma variável de script de linguagem externo. *script* is **nvarchar(max)** .  

`[ @input_data_1 =  N'input_data_1' ]` Especifica os dados de entrada usados pelo script externo na forma de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. O tipo de dados *input_data_1* é **nvarchar (max)** .

`[ @input_data_1_name = N'input_data_1_name' ]` Especifica o nome da variável usado para representar a consulta definida pelo @input_data_1. O tipo de dados da variável no script externo depende do idioma. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. *input_data_1_name* está **sysname**.  Valor padrão é *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` Se aplica somente ao SQL Server 2019 e é usado para criar modelos de acordo com a partição. Especifica o nome da coluna usada para ordenar o conjunto de resultados, por exemplo, ao nome do produto. O tipo de dados da variável no script externo depende do idioma. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` Se aplica somente ao SQL Server 2019 e é usado para criar modelos de acordo com a partição. Especifica o nome da coluna usada para segmentar dados, como região geográfica ou data. O tipo de dados da variável no script externo depende do idioma. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` Especifica o nome da variável no script externo que contém os dados a ser retornado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após a conclusão da chamada de procedimento armazenado. O tipo de dados da variável no script externo depende do idioma. Para R, a saída deve ser um quadro de dados. Para o Python, a saída deve ser um quadro de dados pandas. *output_data_1_name* está **sysname**.  Valor padrão é *OutputDataSet*.  

`[ @parallel = 0 | 1 ]` Habilitar execução paralela de scripts do R, definindo o `@parallel` parâmetro como 1. O padrão para esse parâmetro é 0 (nenhum paralelismo). Se `@parallel = 1` e a saída está sendo transmitida diretamente ao computador cliente, em seguida, a `WITH RESULT SETS` cláusula é necessária e um esquema de saída deve ser especificado.  

 + Para scripts do R que não usam funções RevoScaleR, usando o `@parallel` parâmetro pode ser benéfico para o processamento de grandes conjuntos de dados, supondo que o script pode ser paralelizado trivialmente. Por exemplo, ao usar o R `predict` função com um modelo para gerar novas previsões, defina `@parallel = 1` como uma dica para o mecanismo de consulta. Se a consulta pode ser paralelizada, linhas são distribuídas de acordo com o **MAXDOP** configuração.  
  
 + Para scripts do R que usam funções RevoScaleR, processamento paralelo será tratado automaticamente e você não deve especificar `@parallel = 1` para o **sp_execute_external_script** chamar.  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` Uma lista de declarações de parâmetro de entrada que são usados no script externo.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` Uma lista de valores para os parâmetros de entrada usados pelo script externo.  

## <a name="remarks"></a>Comentários

> [!IMPORTANT]
> A árvore de consulta é controlada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usuários não podem executar operações arbitrárias na consulta. 

Use **sp_execute_external_script** para executar scripts escritos em uma linguagem com suporte. Atualmente, os idiomas com suporte são R para SQL Server 2016 R Services e Python e R para serviços de aprendizado de máquina do SQL Server 2017. 

Por padrão, os conjuntos de resultados retornados por esse procedimento armazenado são de saída com colunas sem nome. Nomes de coluna usados dentro de um script são locais para o ambiente de script e não são refletidos no conjunto de resultados resultantes. Para nomear colunas do conjunto de resultados, use o `WITH RESULT SET` cláusula de [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Além de retornar um conjunto de resultados, você pode retornar valores escalares para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando parâmetros de saída. O exemplo a seguir mostra o uso do parâmetro de saída para retornar o modelo serializado do R que foi usado como entrada para o script:  
  
Você pode controlar os recursos usados pelos scripts externos por meio da configuração de um pool de recursos externos. Para obter mais informações, veja [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informações sobre a carga de trabalho podem ser obtidas as exibições de catálogo do administrador de recursos, da DMV e contadores. Para obter mais informações, consulte [exibições de catálogo do administrador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [ SQL Server, objeto Scripts externos](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Monitorar a execução de script

Execução de script de monitor usando [DM external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [DM external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parâmetros para a modelagem de partição

 No SQL Server de 2019, atualmente em visualização pública, você pode definir dois parâmetros adicionais que permitem a modelagem de dados particionados, onde as partições são baseadas em um ou mais colunas você fornecer que naturalmente segmentar um conjunto de dados em partições lógicas criadas e usadas somente durante a execução do script. Colunas que contêm valores repetidos para idade, sexo, região geográfica, data ou hora, estão alguns exemplos que servem para conjuntos de dados particionados.
 
 Os dois parâmetros forem **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**, em que o segundo parâmetro é usado para ordenar o conjunto de resultados. Os parâmetros são passados como entradas para `sp_execute_external_script` com o script externo que executa uma vez para cada partição. Para obter mais informações e exemplos, consulte [Tutorial: Criar modelos com base em partição](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition).

 Você pode executar o script em paralelo com a especificação de `@parallel=1`. Se a consulta de entrada pode ser paralelizada, defina `@parallel=1` como parte de seus argumentos como `sp_execute_external_script`. Por padrão, o otimizador de consulta opera em `@parallel=1` em tabelas com mais de 256 linhas, mas se você quiser lidar com isso explicitamente, esse script inclui o parâmetro como uma demonstração.

 > [!Tip]
> Para workoads de treinamento, você pode usar `@parallel` em qualquer script de treinamento arbitrário, até mesmo aqueles que usam algoritmos de rx não-Microsoft. Normalmente, somente os algoritmos RevoScaleR (com o prefixo de rx) oferecem paralelismo em cenários de treinamento no SQL Server. Mas, com os novos parâmetros no SQL Server vNext, você pode paralelizar um script que chama as funções não especificamente projetadas com esse recurso.
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>Streaming de execução de scripts R e Python  

O streaming permite que o script de R ou Python para trabalhar com mais dados que pode caber na memória. Para controlar o número de linhas que passam durante a transmissão, especifique um valor inteiro para o parâmetro `@r_rowsPerRead` no `@params` coleção.  Por exemplo, se você estiver treinando um modelo que usa dados muito grande, você pode ajustar o valor para ler menos linhas, para garantir que todas as linhas podem ser enviadas em um bloco de dados. Você também pode usar esse parâmetro para gerenciar o número de linhas que estão sendo lidos e processados ao mesmo tempo, para atenuar problemas de desempenho do servidor. 
  
Os dois o `@r_rowsPerRead` parâmetro para streaming e o `@parallel` argumento deve ser considerado dicas. Para a dica a ser aplicado, ele deve ser possível gerar um plano de consulta SQL que inclui o processamento paralelo. Se isso não for possível, o processamento paralelo não pode ser habilitado.  
  
> [!NOTE]  
>  Processamento paralelo e streaming têm suporte apenas na Enterprise Edition. Você pode incluir os parâmetros em suas consultas na Standard Edition sem gerar um erro, mas os parâmetros não têm nenhum efeito e scripts R será executada em um único processo.  
  
## <a name="restrictions"></a>Restrictions  


### <a name="data-types"></a>Tipos de dados

Os seguintes tipos de dados não têm suporte quando usado na consulta de entrada ou parâmetros de **sp_execute_external_script** procedimento e retornar um erro de tipo sem suporte.  

Como alternativa, **CAST** a coluna ou valor em um tipo com suporte no [!INCLUDE[tsql](../../includes/tsql-md.md)] antes de enviá-la para o script externo.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **text**, **image**  
  
-   **xml**  
  
-   **hierarchyid**, **geometry**, **geography**  
  
-   Tipos definidos pelo usuário de CLR

Em geral, qualquer conjunto de resultados que não pode ser mapeado para um [!INCLUDE[tsql](../../includes/tsql-md.md)] tipo de dados, é gerada como NULL.  

### <a name="restrictions-specific-to-r"></a>Restrições específicas para R

Se a entrada inclui **datetime** valores que não se encaixam no intervalo permitido de valores em R, os valores são convertidos em **NA**. Isso é necessário porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que um intervalo maior de valores do que é compatível com a linguagem R.

Valores flutuantes (por exemplo, `+Inf`, `-Inf`, `NaN`) não têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , embora as duas linguagens usam IEEE 754. Comportamento atual apenas envia os valores a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretamente; como resultado, o cliente do SQL em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] gera um erro. Portanto, esses valores são convertidos **nulo**.

## <a name="permissions"></a>Permissões

Requer **EXECUTE ANY EXTERNAL SCRIPT** permissão de banco de dados.  

## <a name="examples"></a>Exemplos

Esta seção contém exemplos de como esse procedimento armazenado pode ser usado para executar scripts R ou Python usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Retornar um conjunto de dados do R para SQL Server  

O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para retornar o conjunto de dados íris incluído com o R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Gerar um modelo de R com base nos dados do SQL Server  

O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para gerar um modelo e retornar o modelo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  Esse exemplo requer a instalação prévia do pacote e1071. Para obter mais informações, consulte [instalar pacotes R adicionais no SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

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

Títulos de coluna usados no código do Python não são de saída para o SQL Server; Portanto, use a instrução com o resultado para especificar os nomes de coluna e tipos de dados SQL para usar.

Para pontuação, você também pode usar a função nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que é normalmente mais rápida porque evita que o tempo de execução do Python ou do R seja chamado.

## <a name="see-also"></a>Confira também

 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Tipos de dados e bibliotecas Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Bibliotecas do R e tipos de dados de R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [Problemas conhecidos para serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [CREATE EXTERNAL LIBRARY &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção external scripts enabled de configuração de servidor](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server, objeto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
