---
title: EXPLAIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b364a92732be8e12233faf51b03d92154c2a6d28
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53979492"
---
# <a name="explain-transact-sql"></a>EXPLAIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna o plano de consulta de uma instrução [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] sem executar a instrução. Use **EXPLAIN** para visualizar quais operações exigirão a movimentação de dados e para exibir os custos estimados das operações de consulta.  
  
 Para obter mais informações sobre planos de consulta, confira "Entendendo os planos de consulta" em [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SQL_statement*  
 A instrução [!INCLUDE[DWsql](../../includes/dwsql-md.md)] na qual **EXPLAIN** será executado. *SQL_statement* pode ser qualquer um destes comandos: **SELECT**, **INSERT**, **UPDATE**, **DELETE**, **CREATE TABLE AS SELECT**, **CREATE REMOTE TABLE**.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **SHOWPLAN** e a permissão para executar *SQL_statement*. Veja [Permissões: GRANT, DENY, REVOKE &#40;SQL Data Warehouse do Azure, Parallel Data Warehouse&#41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>Valor retornado  
 O valor retornado do comando **EXPLAIN** é um documento XML com a estrutura mostrada abaixo. Este documento XML lista todas as operações no plano de consulta para determinada consulta, cada uma delimitada pela marcação `<dsql_operation>`. O valor retornado é do tipo **nvarchar(max)**.  
  
 O plano de consulta retornado mostra instruções SQL sequenciais. Quando a consulta é executada, ela pode envolver operações em paralelo, portanto algumas das instruções sequenciais mostradas podem ser executadas ao mesmo tempo.  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 As marcas XML contêm estas informações:  
  
|Marcação XML|Resumo, atributos e conteúdo|  
|-------------|--------------------------------------|  
|\<dsql_query>|Elemento de nível superior/documento.|
|\<sql>|Duplica a *SQL_statement*.|  
|\<params>|Essa marcação não é usada no momento.|  
|\<dsql_operations>|Resume e contém as etapas de consulta e inclui as informações de custo da consulta. Também contém todos os blocos de `<dsql_operation>`. Essa marcação contém as informações de contagem da consulta inteira:<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost* é o tempo total estimado para que a consulta seja executada, em ms.<br /><br /> *total_number_operations* é o número total de operações para a consulta. Uma operação que será colocada em paralelo e executada em vários nós é considerada uma única operação.|  
|\<dsql_operation>|Descreve uma única operação no plano de consulta. A marcação \<dsql_operation> contém o tipo de operação como um atributo:<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type* é um dos valores encontrados em [Consultando dados (SQL Server PDW)](https://msdn.microsoft.com/3f4f5643-012a-4c36-b5ec-691c4bbe668c).<br /><br /> O conteúdo no bloco `\<dsql_operation>` depende do tipo de operação.<br /><br /> Veja a tabela abaixo.|  
  
|Tipo de operação|Conteúdo|Exemplo|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE e TRIM_MOVE|Elemento `<operation_cost>` com esses atributos. Os valores refletem somente a operação local:<br /><br /> -   *cost* é o custo do operador local e mostra o tempo estimado para que a operação seja executada, em ms.<br />-   *accumulative_cost* é a soma de todas as operações vistas no plano, incluindo a soma dos valores de operações paralelas, em ms.<br />-   *average_rowsize* é o tamanho médio da linha estimado (em bytes) das linhas recuperadas e passadas durante a operação.<br />-   *output_rows* é a cardinalidade da saída (nó) e mostra o número de linhas de saída.<br /><br /> `<location>`: os nós ou as distribuições em que a operação ocorrerá. As opções são: "Control", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "Distribution" e "SubsetNodes".<br /><br /> `<source_statement>`: os dados de origem para a movimentação em ordem aleatória.<br /><br /> `<destination_table>`: a tabela temporária interna para a qual os dados serão movidos.<br /><br /> `<shuffle_columns>`: (Aplicável somente para operações SHUFFLE_MOVE). Uma ou mais colunas que serão usadas como as colunas de distribuição para a tabela temporária.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: Veja `<operation_cost>` acima.<br /><br /> `<DestinationCatalog>`: o nó ou os nós de destino.<br /><br /> `<DestinationSchema>`: O esquema de destino em DestinationCatalog.<br /><br /> `<DestinationTableName>`: O nome da tabela de destino ou "TableName".<br /><br /> `<DestinationDatasource>`: as informações de nome ou de conexão da fonte de dados de destino.<br /><br /> `<Username>` e `<Password>`: esses campos indicam que um nome de usuário e uma senha para o destino podem ser necessários.<br /><br /> `<BatchSize>`: o tamanho do lote da operação de cópia.<br /><br /> `<SelectStatement>`: a instrução select usada para executar a cópia.<br /><br /> `<distribution>`: a distribuição em que a cópia é executada.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: a tabela de origem da operação.<br /><br /> `<destination_table>`: a tabela de destino da operação.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: Veja `<location>` acima.<br /><br /> `<sql_operation>`: identifica o comando SQL que será executado em um nó.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: o catálogo de destino.<br /><br /> `<DestinationSchema>`: O esquema de destino em DestinationCatalog.<br /><br /> `<DestinationTableName>`: O nome da tabela de destino ou "TableName".<br /><br /> `<DestinationDatasource>`: o nome da fonte de dados de destino.<br /><br /> `<Username>` e `<Password>`: esses campos indicam que um nome de usuário e uma senha para o destino podem ser necessários.<br /><br /> `<CreateStatement>`: a instrução de criação de tabela do banco de dados de destino.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: o identificador do conjunto de resultados.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: o identificador do objeto criado.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 **EXPLAIN** pode ser aplicado a consultas *otimizáveis*, que são consultas que podem ser melhoradas ou modificadas com base nos resultados de um comando **EXPLAIN**. Os comandos **EXPLAIN** compatíveis estão listados acima. A tentativa de usar **EXPLAIN** com um tipo de consulta não compatível retornará um erro ou uma duplicação da consulta.  
  
 Não há compatibilidade com **EXPLAIN** em uma transação de usuário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra um comando **EXPLAIN** executado em uma instrução **SELECT** e o resultado XML.  
  
 **Enviando uma instrução EXPLAIN**  
  
 O comando enviado para este exemplo é:  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 Depois de executar a instrução usando a opção **EXPLAIN**, a guia de mensagem apresentará uma única linha intitulada **explain** começando com o texto XML `\<?xml version="1.0" encoding="utf-8"?>`. Clique no XML para abrir o texto inteiro em um janela de XML. Para entender melhor os comentários a seguir, você deve ativar a exibição de números de linha no SSDT.  
  
#### <a name="to-turn-on-line-numbers"></a>Para ativar os números de linha  
  
1.  Com a saída aparecendo no SSDT na guia **explain**, no menu **FERRAMENTAS**, selecione **Opções**.  
  
2.  Expanda a seção **Editor de Texto**, expanda o **XML** e, em seguida, clique em **Geral**.  
  
3.  Na área **Exibição**, marque **Números de linha**.  
  
4.  Clique em **OK**.  
  
 **Exemplo de saída de EXPLAIN**  
  
 O resultado XML do comando **EXPLAIN** com números de linha ativados é:  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **Significado da saída de EXPLAIN**  
  
 O resultado acima contém 144 linhas numeradas. A sua saída dessa consulta poderá ser um pouco diferente. A lista a seguir descreve as seções significativas.  
  
-   As linhas 3 a 16 fornecem uma descrição da consulta que está sendo analisada.  
  
-   A linha 17 especifica que o número total de operações será 9. Encontre o início de cada operação procurando as palavras **dsql_operation**.  
  
-   A linha 18 inicia a operação 1. As linhas 18 e 19 indicam que uma operação **RND_ID** criará um número de ID aleatório que será usado para uma descrição do objeto. O objeto descrito na saída acima é **TEMP_ID_16893**. O seu número será diferente.  
  
-   A linha 20 inicia a operação 2. Linhas 21 a 25: em todos os nós de computação, criam uma tabela temporária denominada **TEMP_ID_16893**.  
  
-   A linha 26 inicia a operação 3. Linhas 27 a 37: movem os dados para **TEMP_ID_16893** usando uma difusão. A consulta enviada a cada nó de computação é fornecida. A linha 37 especifica que a tabela de destino é **TEMP_ID_16893**.  
  
-   A linha 38 inicia a operação 4. Linhas 39 a 40: criam uma ID aleatória para uma tabela. **TEMP_ID_16894** é o número da ID no exemplo acima. O seu número será diferente.  
  
-   A linha 41 inicia a operação 5. Linhas 42 a 46: em todos os nós, criam uma tabela temporária denominada **TEMP_ID_16894**.  
  
-   A linha 47 inicia a operação 6. Linhas 48 a 91: movem os dados de várias tabelas (incluindo a **TEMP_ID_16893**) para a tabela **TEMP_ID_16894**, usando uma operação de movimentação em ordem aleatória. A consulta enviada a cada nó de computação é fornecida. A linha 90 especifica a tabela de destino como **TEMP_ID_16894**. A linha 91 especifica as colunas.  
  
-   A linha 92 inicia a operação 7. Linhas 93 a 97: em todos os nós de computação, removem a tabela temporária **TEMP_ID_16893**.  
  
-   A linha 98 inicia a operação 8. Linhas 99 a 135: retornam resultados para o cliente. Usa a consulta fornecida para obter os resultados.  
  
-   A linha 136 inicia a operação 9. Linhas 137 a 140: Em todos os nós, removem a tabela temporária **TEMP_ID_16894**.  
  
  

