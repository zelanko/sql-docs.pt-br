---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs: TSQL
helpviewer_keywords: sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d437e6e8d86aa648d9c6ef11a8ca04297cafbaf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Executa o script fornecido como argumento em um local externo. O script deve ser gravado em um idioma com suporte e registrado. A árvore de consulta é controlada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os usuários não podem executar operações arbitrárias na consulta. Para executar **sp_execute_external_script**, você deve primeiro habilitar scripts externos usando o `sp_configure 'external scripts enabled', 1;` instrução.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_execute_external_script   
    @language = N'language,   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```  
  
## <a name="arguments"></a>Argumentos  
 @language= N'*idioma*'  
 Indica a linguagem de script. *idioma* é **sysname**.  

 Os valores válidos são `Python` ou `R`. 
  
 @script= N'*script*'  
 Script de idioma externo especificado como uma entrada de um literal ou variável. *script* é **nvarchar (max)**.  
  
 [ @input_data_1_name = N'*input_data_1_name*']  
 Especifica o nome da variável usado para representar a consulta definida pelo @input_data_1. O tipo de dados da variável no script externo depende do idioma. No caso de R, a variável de entrada é um quadro de dados. No caso do Python, a entrada deve ser tabular. *input_data_1_name* é **sysname**.  
  
 Valor padrão é "InputDataSet".  
  
 [ @input_data_1 = N'*input_data_1*']  
 Especifica os dados de entrada usados pelo script externo na forma de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. *input_data_1* é **nvarchar (max)**.  
  
 [ @output_data_1_name = N'*output_data_1_name*']  
 Especifica o nome da variável no script externo que contém os dados a serem retornados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após a conclusão da chamada de procedimento armazenado. O tipo de dados da variável no script externo depende do idioma. No caso de R, a saída deve ser um quadro de dados. No caso do Python, a saída deve ser um quadro de dados pandas. *output_data_1_name* é **sysname**.  
  
 Valor padrão é "OutputDataSet".  
  
 [ @parallel = 0 | 1 ]  
 Habilitar a execução paralela de scripts R, definindo o `@parallel` parâmetro como 1. O padrão para esse parâmetro é 0 (nenhum paralelismo).  
  
 Para scripts de R que não usam funções de RevoScaleR, usando o `@parallel` parâmetro pode ser útil para processar grandes conjuntos de dados, supondo que o script pode ser facilmente paralelizado. Por exemplo, ao usar o R `predict` função com um modelo para gerar previsões novas, defina `@parallel = 1` como uma dica para o mecanismo de consulta. Se a consulta pode ser colocado em paralelo, linhas são distribuídas de acordo com o **MAXDOP** configuração.  
  
 Se `@parallel = 1` e a saída está sendo transmitida diretamente ao computador cliente, em seguida, o `WITH RESULTS SETS` cláusula é necessária e um esquema de saída deve ser especificado.  
  
 Para scripts de R que usam funções de RevoScaleR, processamento paralelo é tratado automaticamente e você não deve especificar `@parallel = 1` para o **sp_execute_external_script** chamar.  
  
 [ @params = N' *@parameter_name data_type* [OUT | SAÍDA] [,... n]']  
 Uma lista de declarações de parâmetro de entrada que são usados no script externo.  
  
 [ @parameter1 = '*value1*' [OUT | SAÍDA] [,... n]]  
 Uma lista de valores para os parâmetros de entrada usados pelo script externo.  


## <a name="remarks"></a>Comentários  
 Use **sp_execute_external_script** para executar scripts escritos em uma linguagem com suporte, como R. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é composto por um componente de servidor instalado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e um conjunto de ferramentas de estação de trabalho e bibliotecas de conectividade que conectam o cientista de dados ao ambiente de alto desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Instalar os serviços de R (no banco de dados) durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação para habilitar a execução de scripts de R. Para obter mais informações, consulte [configurar o SQL Server R Services &#40; no banco de dados &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
 Você pode controlar os recursos usados por um script externo ao configurar um pool de recursos externos. Para obter mais informações, veja [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Informações sobre a carga de trabalho podem ser obtidas de exibições de catálogo do administrador de recursos, DMVS e contadores. Para obter mais informações, consulte [exibições de catálogo do administrador de recursos &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Administrador de recursos relacionados a exibições de gerenciamento dinâmico &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md), e [do SQL Server, External Scripts de objeto](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

Execução de script de monitor usando [sys.DM external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys.DM external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

 Por padrão, os conjuntos de resultados retornados por esse procedimento armazenado são saída com colunas sem nome. Nomes de coluna usados dentro de um script são locais para o ambiente de script e não são refletidos no conjunto de resultados do meio. Para nomear colunas do conjunto de resultados, use o `WITH RESULTS SET` cláusula de [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Além de retornar um conjunto de resultados, você pode retornar valores escalares de script R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando parâmetros de saída. O exemplo a seguir mostra o uso do parâmetro de saída:  
  
```  
DECLARE @model varbinary(max);  
EXEC sp_execute_external_script  
        @language = N'R'  
        , @script = N'  
    # build classification model to predict tipped or not  
    logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource, family = binomial(link=logit));  
  
    # First, serialize a model and put it into a database table  
    modelbin <- serialize(logitObj, NULL);  
    '  
        , @input_data_1 = N'  
SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance  
  FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)  
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d  
'  
        , @input_data_1_name = N'featureDataSource'  
        , @params = N'@modelbin varbinary(max) OUTPUT'  
        , @modelbin = @model OUTPUT;  
```  


## <a name="streaming-execution-for-r-script"></a>Fluxo de execução de script R  
 Fluxo de execução do script R é suportado pela especificação de `@r_rowsPerRead int parameter` na `@params` coleção.  Streaming permite que os scripts de R para trabalhar com dados que não cabem na memória. Por exemplo, se houver bilhões de linhas para a pontuação usando prever função novo `@r_rowsPerRead` parâmetro pode ser usado para dividir a execução em um fluxo de cada vez. Como esse parâmetro controla o número de linhas que são enviadas para os processos de R, ele também pode ser usado para limitar o número de linhas que estão sendo lidos ao mesmo tempo. Isso pode ser útil para solucionar problemas de desempenho do servidor, se, por exemplo, um modelo grande está sendo treinado. Observe que esse parâmetro só pode ser usado em casos em que a saída do script R não depende de leitura ou examinar todo o conjunto de linhas.  
  
 Ambos o `@r_rowsPerRead` parâmetro para streaming e o `@parallel` argumento deve ser considerado como dicas. Para a dica a ser aplicado, ele deve ser possível gerar um plano de consulta SQL que inclui o processamento paralelo. Se isso não for possível, o processamento paralelo não pode ser habilitado.  
  
> [!NOTE]  
>  Transmissão e processamento paralelo têm suporte apenas no Enterprise Edition. Você pode incluir os parâmetros em suas consultas Standard Edition sem gerar um erro, mas os parâmetros não têm nenhum efeito e scripts de R executados em um único processo.  
  
## <a name="restrictions"></a>Restrições  
 **Tipos de dados:** os seguintes tipos de dados não têm suporte quando usados na consulta de entrada ou parâmetros de `sp_execute_external_script` procedimento e retornar um erro de tipo sem suporte.  
  
 Como alternativa, **CAST** a coluna ou o valor para um tipo com suporte no [!INCLUDE[tsql](../../includes/tsql-md.md)] e enviá-lo para R.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **tempo**  
  
-   **sql_variant**  
  
-   **texto**, **imagem**  
  
-   **xml**  
  
-   **HierarchyID**, **geometria**, **geografia**  
  
-   Tipos definidos pelo usuário de CLR  
  
 **DateTime** valores na entrada são convertidos no lado do R para valores que não se ajustam o intervalo permitido de valores em R. Isso é necessário porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite um intervalo maior de valores que há suporte para a linguagem R.  
  
 Valores de float (por exemplo, + Inf, NaN -Inf) não têm suporte em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , embora ambas as linguagens usam IEEE 754. Apenas o comportamento atual envia os valores a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretamente como um resultado sqlclient no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] gera erro. Converter esses valores em **nulo**.  
  
 Qualquer conjunto de resultados de R que não pode ser mapeado para um [!INCLUDE[tsql](../../includes/tsql-md.md)] tipo de dados, é gerada como NULL.  
  
## <a name="permissions"></a>Permissões  
 Requer **EXECUTE ANY EXTERNAL SCRIPT** permissão de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 Esta seção contém exemplos de como esse procedimento armazenado pode ser usado para executar scripts R usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
### <a name="a-return-a-data-set-from-r-to-sql-server"></a>A. Retornar um conjunto de dados de R para o SQL Server  
 O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para retornar um conjunto de dados iris de R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
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
go  
```  
  
### <a name="b-generate-a-model-based-on-data-from-sql-server"></a>B. Gerar um modelo com base em dados do SQL Server  
 O exemplo a seguir cria um procedimento armazenado que usa **sp_execute_external_script** para gerar um modelo de íris e retornar o modelo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Este exemplo requer a instalação do pacote e1071. Para obter mais informações, consulte [instalar pacotes de R adicionais no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).  
  
```  
DROP PROC IF EXISTS generate_iris_model;  
go  
  
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
go  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Bibliotecas de Python e tipos de dados](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Tipos de dados de R e bibliotecas de R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Problemas conhecidos do SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [Criar biblioteca externa &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção de configuração de servidor External scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server, objeto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
  
