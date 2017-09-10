---
title: EXPLIQUE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b83d9a72ce1adbb37a80da8bfd52824b02fa16b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="explain-transact-sql"></a>EXPLIQUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna o plano de consulta para um [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] instrução sem executar a instrução. Use **EXPLICAR** para visualizar quais operações exigirá a movimentação de dados e exibir os custos estimados das operações de consulta.  
  
 Para obter mais informações sobre planos de consulta, consulte "Noções básicas sobre planos de consulta" o [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  

```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *SQL_statement*  
 O [!INCLUDE[DWsql](../../includes/dwsql-md.md)] instrução na qual **EXPLICAR** será executado. *SQL_statement* pode ser qualquer um destes comandos: **selecione**, **inserir**, **atualização**, **excluir**,  **CREATE TABLE AS SELECT**, **criar tabela remota**.  
  
## <a name="permissions"></a>Permissões  
 Requer o **SHOWPLAN** permissão e a permissão para executar *SQL_statement*. Consulte [permissões: GRANT, DENY, REVOKE &#40; Depósito de dados SQL do Azure, Parallel Data Warehouse &#41; ](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>Valor de retorno  
 O valor de retorno de **EXPLICAR** comando é um documento XML com a estrutura mostrado abaixo. Este documento XML de lista todas as operações no plano de consulta para determinada consulta, cada delimitados pelo `<dsql_operation>` marca. O valor de retorno é do tipo **nvarchar (max)**.  
  
 O plano de consulta retornada mostra instruções SQL sequenciais; Quando a consulta é executada pode envolver operações em paralelo, para que algumas das instruções sequenciais mostradas podem executar ao mesmo tempo.  
  
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
  
 As marcas XML contêm essas informações:  
  
|Marca XML|Resumo, atributos e conteúdo|  
|-------------|--------------------------------------|  
|\<dsql_query >|Elemento de nível superior/documento.|
|\<SQL >|Duplica a *SQL_statement*.|  
|\<params >|Essa marca não é usada no momento.|  
|\<dsql_operations >|Resume e contém as etapas de consulta e inclui informações de custo para a consulta. Também contém todos os `<dsql_operation>` blocos. Essa marca contém informações de contagem para a consulta inteira:<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost* é o tempo total estimado para a consulta seja executada em ms.<br /><br /> *total_number_operations* é o número total de operações para a consulta. Uma operação que serão colocados em paralelo e executada em vários nós é contada como uma única operação.|  
|\<dsql_operation >|Descreve uma única operação no plano de consulta. O \<dsql_operation > marca contém o tipo de operação como um atributo:<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type* é um dos valores encontrados na [consultando dados (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c).<br /><br /> O conteúdo a `\<dsql_operation>` bloco é dependente do tipo de operação.<br /><br /> Consulte a tabela a seguir.|  
  
|Tipo de operação|Conteúdo|Exemplo|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE, MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE e TRIM_MOVE|`<operation_cost>`elemento com esses atributos. Valores refletem somente a operação local:<br /><br /> -   *custo* é o custo do operador local e mostra o tempo estimado para a operação em execução, em ms.<br />-   *accumulative_cost* é a soma de todas as operações vistas no plano, incluindo valores somados para operações paralelas, em ms.<br />-   *average_rowsize* é o tamanho médio da linha estimado (em bytes) de linhas recuperado e passado durante a operação.<br />-   *output_rows* é a cardinalidade de saída (nó) e mostra o número de linhas de saída.<br /><br /> `<location>`: Os nós ou distribuições em que a operação ocorrerá. Opções são: "Control", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "Distribuição" e "SubsetNodes".<br /><br /> `<source_statement>`: Mover os dados de origem para a ordem aleatória.<br /><br /> `<destination_table>`: A tabela temporária interna os dados serão movidos para.<br /><br /> `<shuffle_columns>`: (Aplicável somente para operações de SHUFFLE_MOVE). Uma ou mais colunas que serão usadas como colunas de distribuição para a tabela temporária.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: Consulte `<operation_cost>` acima.<br /><br /> `<DestinationCatalog>`: O nó de destino ou a nós.<br /><br /> `<DestinationSchema>`: O esquema de destino em DestinationCatalog.<br /><br /> `<DestinationTableName>`: O nome da tabela de destino ou "TableName".<br /><br /> `<DestinationDatasource>`: As informações de nome ou conexão da fonte de dados de destino.<br /><br /> `<Username>`e `<Password>`: esses campos indicam que um nome de usuário e senha para o destino podem ser necessárias.<br /><br /> `<BatchSize>`: O tamanho do lote da operação de cópia.<br /><br /> `<SelectStatement>`: A instrução select usada para executar a cópia.<br /><br /> `<distribution>`: A distribuição em que a cópia é executada.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: A tabela de origem para a operação.<br /><br /> `<destionation_table>`: A tabela de destino para a operação.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: Consulte `<location>` acima.<br /><br /> `<sql_operation>`: Identifica o comando SQL que será executado em um nó.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: O catálogo de destino.<br /><br /> `<DestinationSchema>`: O esquema de destino em DestinationCatalog.<br /><br /> `<DestinationTableName>`: O nome da tabela de destino ou "TableName".<br /><br /> `<DestinationDatasource>`: O nome da fonte de dados de destino.<br /><br /> `<Username>`e `<Password>`: esses campos indicam que um nome de usuário e senha para o destino podem ser necessárias.<br /><br /> `<CreateStatement>`: A instrução de criação de tabela do banco de dados de destino.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: O identificador do conjunto de resultados.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: O identificador do objeto criado.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 **EXPLICAR** pode ser aplicado a *otimizável* consultas, que são consultas que podem ser melhoradas ou modificadas com base nos resultados de uma **EXPLICAM** comando. Com o suporte **EXPLICAR** comandos estão listados acima. Tentativa de usar **EXPLICAR** com uma consulta sem suporte tipo irá retornar um erro ou a consulta de eco.  
  
 **EXPLIQUE** não tem suporte em uma transação de usuário.  
  
## <a name="examples"></a>Exemplos  
 A exemplo a seguir mostra um **EXPLICAR** comando executado em um **selecione** instrução e o resultado XML.  
  
 **Enviar uma instrução EXPLICAR**  
  
 O comando enviado para este exemplo é:  
  
```  
USE AdventureWorksPDW2012;  
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
  
 Depois de executar a instrução usando o **EXPLICAR** opção, na guia mensagem apresenta uma única linha intitulada **explicam**e começando com o texto XML `\<?xml version="1.0" encoding="utf-8"?>` clique em XML para abrir o texto inteiro em um Janela XML. Para entender melhor os comentários a seguir, você deve ativar a exibição de números de linha no SSDT.  
  
#### <a name="to-turn-on-line-numbers"></a>Para ativar os números de linha  
  
1.  Com a saída aparecem no **explicam** guia SSDT, o **ferramentas** menu, selecione **opções**.  
  
2.  Expanda o **Editor de texto** seção, expanda **XML**e, em seguida, clique em **geral**.  
  
3.  No **exibição** área, seleção **números de linha**.  
  
4.  Clique em **OK**.  
  
 **Exemplo de saída de EXPLICAR**  
  
 O resultado do XML do **EXPLICAR** comando com números de linha ativados é:  
  
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
  
 **Significado da saída EXPLICAR**  
  
 O resultado acima contém 144 linhas numeradas. A saída dessa consulta pode diferir ligeiramente. A lista a seguir descreve as seções significativas.  
  
-   Linhas de 3 a 16 fornecem uma descrição da consulta que está sendo analisada.  
  
-   Linha 17, especifica que o número total de operações será 9. Você pode encontrar o início de cada operação, procurando as palavras **dsql_operation**.  
  
-   Linha 18 inicia a operação de 1. Linhas 18 e 19 indicam que um **RND_ID** operação criará um número de ID aleatório que será usado para uma descrição do objeto. O objeto descrito na saída acima é **TEMP_ID_16893**. O número será diferente.  
  
-   Linha 20 inicia a operação de 2. Linhas de 21 a 25: em todos os nós de computação, crie uma tabela temporária denominada **TEMP_ID_16893**.  
  
-   Linha 26 inicia a operação de 3. Linhas 27 a 37: mover os dados **TEMP_ID_16893** , usando uma difusão. A consulta enviada a cada nó de computação é fornecida. Linha 37 Especifica a tabela de destino é **TEMP_ID_16893**.  
  
-   Linha 38 inicia a operação de 4. Linhas 39 a 40: criar uma ID aleatória para uma tabela. **TEMP_ID_16894** é o número de identificação no exemplo acima. O número será diferente.  
  
-   Linha 41 inicia a operação de 5. Linhas 42 por meio de 46: em todos os nós, crie uma tabela temporária denominada **TEMP_ID_16894**.  
  
-   Linha 47 inicia a operação de 6. Linhas de 48 a 91: mover os dados de várias tabelas (incluindo **TEMP_ID_16893**) para tabela **TEMP_ID_16894**, usando uma ordem aleatória da operação de mover. A consulta enviada a cada nó de computação é fornecida. Linha 90 Especifica a tabela de destino como **TEMP_ID_16894**. Linha 91 Especifica as colunas.  
  
-   Linha 92 inicia a operação de 7. 93 linhas por meio de 97: em todos os nós de computação, descarte a tabela temporária **TEMP_ID_16893**.  
  
-   Linha 98 inicia a operação de 8. 99 linhas por meio de 135: retornar resultados para o cliente. Usa a consulta fornecida para obter os resultados.  
  
-   Linha 136 inicia a operação de 9. Linhas 137 por meio de 140: em todos os nós, descarte a tabela temporária **TEMP_ID_16894**.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A exemplo a seguir mostra um **EXPLICAR** comando executado em um **selecione** instrução e o resultado XML.  
  
 **Enviar uma instrução EXPLICAR**  
  
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
  
 Depois de executar a instrução usando o **EXPLICAR** opção, na guia mensagem apresenta uma única linha intitulada **explicam**e começando com o texto XML `\<?xml version="1.0" encoding="utf-8"?>` clique em XML para abrir o texto inteiro em um Janela XML. Para entender melhor os comentários a seguir, você deve ativar a exibição de números de linha no SSDT.  
  
#### <a name="to-turn-on-line-numbers"></a>Para ativar os números de linha  
  
1.  Com a saída aparecem no **explicam** guia SSDT, o **ferramentas** menu, selecione **opções**.  
  
2.  Expanda o **Editor de texto** seção, expanda **XML**e, em seguida, clique em **geral**.  
  
3.  No **exibição** área, seleção **números de linha**.  
  
4.  Clique em **OK**.  
  
 **Exemplo de saída de EXPLICAR**  
  
 O resultado do XML do **EXPLICAR** comando com números de linha ativados é:  
  
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
  
 **Significado da saída EXPLICAR**  
  
 O resultado acima contém 144 linhas numeradas. A saída dessa consulta pode diferir ligeiramente. A lista a seguir descreve as seções significativas.  
  
-   Linhas de 3 a 16 fornecem uma descrição da consulta que está sendo analisada.  
  
-   Linha 17, especifica que o número total de operações será 9. Você pode encontrar o início de cada operação, procurando as palavras **dsql_operation**.  
  
-   Linha 18 inicia a operação de 1. Linhas 18 e 19 indicam que um **RND_ID** operação criará um número de ID aleatório que será usado para uma descrição do objeto. O objeto descrito na saída acima é **TEMP_ID_16893**. O número será diferente.  
  
-   Linha 20 inicia a operação de 2. Linhas de 21 a 25: em todos os nós de computação, crie uma tabela temporária denominada **TEMP_ID_16893**.  
  
-   Linha 26 inicia a operação de 3. Linhas 27 a 37: mover os dados **TEMP_ID_16893** , usando uma difusão. A consulta enviada a cada nó de computação é fornecida. Linha 37 Especifica a tabela de destino é **TEMP_ID_16893**.  
  
-   Linha 38 inicia a operação de 4. Linhas 39 a 40: criar uma ID aleatória para uma tabela. **TEMP_ID_16894** é o número de identificação no exemplo acima. O número será diferente.  
  
-   Linha 41 inicia a operação de 5. Linhas 42 por meio de 46: em todos os nós, crie uma tabela temporária denominada **TEMP_ID_16894**.  
  
-   Linha 47 inicia a operação de 6. Linhas de 48 a 91: mover os dados de várias tabelas (incluindo **TEMP_ID_16893**) para tabela **TEMP_ID_16894**, usando uma ordem aleatória da operação de mover. A consulta enviada a cada nó de computação é fornecida. Linha 90 Especifica a tabela de destino como **TEMP_ID_16894**. Linha 91 Especifica as colunas.  
  
-   Linha 92 inicia a operação de 7. 93 linhas por meio de 97: em todos os nós de computação, descarte a tabela temporária **TEMP_ID_16893**.  
  
-   Linha 98 inicia a operação de 8. 99 linhas por meio de 135: retornar resultados para o cliente. Usa a consulta fornecida para obter os resultados.  
  
-   Linha 136 inicia a operação de 9. Linhas 137 por meio de 140: em todos os nós, descarte a tabela temporária **TEMP_ID_16894**.  
  
  


