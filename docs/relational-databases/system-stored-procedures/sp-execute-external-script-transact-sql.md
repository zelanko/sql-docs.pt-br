---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5660860a3a03a268b0903a0222753f1ea9bc5382
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263102"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Executa o script fornecido como argumento em um local externo. O script deve ser gravado em um idioma com suporte e registrado. Para executar **sp_execute_external_script**, você deve primeiro habilitar scripts externos por meio da instrução, `sp_configure 'external scripts enabled', 1;`.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe

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

## <a name="arguments"></a>Argumentos
 @language = N'*idioma*'  
 Indica a linguagem de script. *idioma* é **sysname**.  

 Os valores válidos são `Python` ou `R`. 
  
 @script = N'*script*'  
 Script de idioma externo especificado como uma entrada de um literal ou variável. *script* é **nvarchar (max)**.  
  
 [ @input_data_1_name = N'*input_data_1_name*']  
 Especifica o nome da variável usado para representar a consulta definida pelo @input_data_1. O tipo de dados da variável no script externo depende do idioma. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. *input_data_1_name* é **sysname**.  
  
 Valor padrão é `InputDataSet`.  
  
 [ @input_data_1 = N'*input_data_1*']  
 Especifica os dados de entrada usados pelo script externo na forma de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. O tipo de dados *input_data_1* é **nvarchar (max)**.
  
 [ @output_data_1_name = N'*output_data_1_name*']  
 Especifica o nome da variável no script externo que contém os dados a serem retornados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após a conclusão da chamada de procedimento armazenado. O tipo de dados da variável no script externo depende do idioma. Para R, a saída deve ser um quadro de dados. Para Python, a saída deve ser um quadro de dados pandas. *output_data_1_name* é **sysname**.  
  
 Valor padrão é "OutputDataSet".  
  
 [ @parallel = 0 | 1] Ativar execução paralela de scripts R, definindo o `@parallel` parâmetro como 1. O padrão para esse parâmetro é 0 (nenhum paralelismo).  
  
 Para scripts de R que não usam funções de RevoScaleR, usando o `@parallel` parâmetro pode ser útil para processar grandes conjuntos de dados, supondo que o script pode ser facilmente paralelizado. Por exemplo, ao usar o R `predict` função com um modelo para gerar previsões novas, defina `@parallel = 1` como uma dica para o mecanismo de consulta. Se a consulta pode ser colocado em paralelo, linhas são distribuídas de acordo com o **MAXDOP** configuração.  
  
 Se `@parallel = 1` e a saída está sendo transmitida diretamente ao computador cliente, em seguida, o `WITH RESULTS SETS` cláusula é necessária e um esquema de saída deve ser especificado.  
  
 Para scripts de R que usam funções de RevoScaleR, processamento paralelo é tratado automaticamente e você não deve especificar `@parallel = 1` para o **sp_execute_external_script** chamar.  
  
 [ @params = N' *@parameter_name data_type* [OUT | SAÍDA] [,... n]']  
 Uma lista de declarações de parâmetro de entrada que são usados no script externo.  
  
 [ @parameter1 = '*value1*' [OUT | SAÍDA] [,... n]]  
 Uma lista de valores para os parâmetros de entrada usados pelo script externo.  

## <a name="remarks"></a>Remarks

Use **sp_execute_external_script** para executar scripts escritos em uma linguagem com suporte. Atualmente, as linguagens com suporte são R para SQL Server 2016 e Python e R para 2017 do SQL Server. 

> [!IMPORTANT]
> A árvore de consulta é controlada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os usuários não podem executar operações arbitrárias na consulta. 

Por padrão, os conjuntos de resultados retornados por esse procedimento armazenado são saída com colunas sem nome. Nomes de coluna usados dentro de um script são locais para o ambiente de script e não são refletidos no conjunto de resultados do meio. Para nomear colunas do conjunto de resultados, use o `WITH RESULTS SET` cláusula de [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Além de retornar um conjunto de resultados, você pode retornar valores escalares para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando parâmetros de saída. O exemplo a seguir mostra o uso do parâmetro de saída para retornar o modelo R serializado que foi usado como entrada para o script:  

Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é composta de um componente de servidor instalado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e um conjunto de ferramentas de estação de trabalho e bibliotecas de conectividade que conectam o cientista de dados para o ambiente de alto desempenho de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve instalar a componentes durante de aprendizado de máquina [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação para habilitar a execução de scripts externos. Para obter mais informações, consulte [configurar serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).  
  
Você pode controlar os recursos usados pelos scripts externos ao configurar um pool de recursos externos. Para obter mais informações, veja [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informações sobre a carga de trabalho podem ser obtidas de exibições de catálogo do administrador de recursos, DMVS e contadores. Para obter mais informações, consulte [exibições de catálogo do administrador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)e [ Objeto de Scripts do SQL Server, externo](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

Execução de script de monitor usando [sys.DM external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys.DM external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

## <a name="streaming-execution-for-r-and-python-scripts"></a>Fluxo de execução de scripts R e Python  

Streaming permite que o script R ou Python trabalhar com mais dados do que pode caber na memória. Para controlar o número de linhas passado durante a transmissão, especifique um valor inteiro para o parâmetro `@r_rowsPerRead` no `@params` coleção.  Por exemplo, se o treinamento de um modelo que usa dados muito grande, você pode ajustar o valor para ler menos linhas, para garantir que todas as linhas podem ser enviadas em um bloco de dados. Você também pode usar esse parâmetro para gerenciar o número de linhas que estão sendo lidos e processados ao mesmo tempo, para atenuar problemas de desempenho do servidor. 
  
Ambos o `@r_rowsPerRead` parâmetro para streaming e o `@parallel` argumento deve ser considerado como dicas. Para a dica a ser aplicado, ele deve ser possível gerar um plano de consulta SQL que inclui o processamento paralelo. Se isso não for possível, o processamento paralelo não pode ser habilitado.  
  
> [!NOTE]  
>  Transmissão e processamento paralelo têm suporte apenas no Enterprise Edition. Você pode incluir os parâmetros em suas consultas Standard Edition sem gerar um erro, mas os parâmetros não têm nenhum efeito e scripts de R executados em um único processo.  
  
## <a name="restrictions"></a>Restrições  


### <a name="data-types"></a>Tipos de dados

Os seguintes tipos de dados não têm suporte quando usados na consulta de entrada ou parâmetros de `sp_execute_external_script` procedimento e retornar um erro de tipo sem suporte.  

Como alternativa, **CAST** a coluna ou o valor para um tipo com suporte no [!INCLUDE[tsql](../../includes/tsql-md.md)] antes de enviá-la para o script externo.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **text**, **image**  
  
-   **xml**  
  
-   **HierarchyID**, **geometria**, **geografia**  
  
-   Tipos definidos pelo usuário de CLR

Em geral, qualquer conjunto de resultados que não pode ser mapeado para um [!INCLUDE[tsql](../../includes/tsql-md.md)] tipo de dados, é gerada como NULL.  

### <a name="restrictions-specific-to-r"></a>Restrições específicas para R

Se a entrada inclui **datetime** valores que não se ajustam o intervalo permitido de valores em R, os valores são convertidos em **NA**. Isso é necessário porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite um intervalo maior de valores que há suporte para a linguagem R.

Valores flutuantes (por exemplo, `+Inf`, `-Inf`, `NaN`) não são suportados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , embora ambas as linguagens usam IEEE 754. Apenas o comportamento atual envia os valores a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretamente, como resultado, o cliente SQL no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] gera um erro. Portanto, esses valores são convertidos em **nulo**.

## <a name="permissions"></a>Permissões

Requer **EXECUTE ANY EXTERNAL SCRIPT** permissão de banco de dados.  

## <a name="examples"></a>Exemplos

Esta seção contém exemplos de como esse procedimento armazenado pode ser usado para executar scripts R ou Python usando [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Retornar um conjunto de dados R para o SQL Server  

O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para retornar o conjunto de dados Iris incluído no R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

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

O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para gerar um modelo de íris e retornar o modelo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  Este exemplo requer a instalação avançada do pacote e1071. Para obter mais informações, consulte [instalar pacotes R adicionais no SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

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

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Criar um modelo de Python e gerar pontuações dele

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

Títulos de coluna usados no código Python não são enviados como saída para o SQL Server. Portanto, use a instrução WITH RESULTS para especificar os nomes de coluna e tipos de dados a serem usados pelo SQL.

Para pontuação, você também pode usar a função nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que é normalmente mais rápida porque evita que o tempo de execução do Python ou do R seja chamado.

## <a name="see-also"></a>Consulte também

 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Bibliotecas de Python e tipos de dados](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Tipos de dados de R e bibliotecas de R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
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
