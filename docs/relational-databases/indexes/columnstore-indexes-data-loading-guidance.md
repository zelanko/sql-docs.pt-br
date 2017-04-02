---
title: "Carregamento de dados dos &#237;ndices columnstore | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b29850b5-5530-498d-8298-c4d4a741cdaf
caps.latest.revision: 31
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 28
---
# Carregamento de dados dos &#237;ndices columnstore
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Carregue dados em um índice columnstore usando o carregamento em massa SQL padrão e os métodos de inserção de fluxo. Esses métodos incluem bcp, Integration Services e a instrução merge ou insert do Transact-SQL.  
  
 Novato em índices columnstore? Examine os termos e conceitos no [Guia de índices columnstore](../Topic/Columnstore%20Indexes%20Guide.md).  
  
 Precisa de uma discussão aprofundada? Veja esta [postagem de blog](http://blogs.msdn.com/b/sqlcat/archive/2015/03/11/data-loading-performance-considerations-on-tables-with-clustered-columnstore-index.aspx).  
  
##  <a name="dataload_cci"></a> Carregamento em massa em um índice columnstore clusterizado  
 Para carregamento em massa de linhas em um índice columnstore clusterizado, você pode usar a ferramenta de linha de comando bcp, o Integration Services ou selecionar linhas em uma tabela de preparo.  
  
 ![Carregando em um índice columnstore clusterizado](../../relational-databases/indexes/media/sql-server-pdw-columnstore-loadprocess.gif "Carregando em um índice columnstore clusterizado")  
  
 Como sugere o diagrama, um carregamento em massa:  
  
1.  Não classifica previamente os dados. Os dados são inseridos em rowgroups na ordem em que são recebidos.  
  
2.  Se o tamanho do lote for superior ou igual a 102.400, as linhas serão carregadas diretamente em rowgroups compactados. É recomendável escolher um tamanho de lote superior ou igual a 102.400 para importação em massa eficiente, pois você pode evitar mover linhas de dados para um rowgroup delta antes que as linhas sejam finalmente movidas para rowgroups compactados por um thread em segundo plano, o TM (Motor de Tupla).  
  
3.  Se o tamanho do lote for inferior a 102.400 ou se as linhas restantes forem inferiores a 102.400, as linhas serão carregadas em rowgroups delta.  
  
 Veja a seguir as otimizações disponíveis com o carregamento em massa no índice columnstore clusterizado  
  
-   Carregamento paralelo: você pode fazer várias importações em massa (bcp, ou inserção em massa) simultaneamente carregando um arquivos de dados separado. Diferentemente de rowstore, não é preciso especificar TABLOCK porque cada thread de importação em massa carregará dados exclusivamente em um rowgroup separado (rowgroups compactados ou delta) com bloqueio exclusivo nele.   O uso de TABLOCK forçará um bloqueio exclusivo na tabela e você não poderá importar dados paralelamente.  
  
-   Otimização de log: o carregamento em massa será minimamente registrado quando os dados forem carregados no rowgroup compactado. Não haverá registro mínimo quando os dados forem carregados no rowgroup delta com tamanho de lote inferior a 102.400.  
  
-   Otimização de bloqueio: no carregamento em um rowgroup compactado, o bloqueio X no rowgroup é adquirido. No entanto, ao carregar em massa no rowgroup delta, um bloqueio X é adquirido em rowgroup, mas o SQL Server ainda bloqueia os bloqueios PAGE/EXTENT porque o bloqueio do rowgroup X não faz parte da hierarquia de bloqueio.  
  
 Se você tiver um ou mais índices não clusterizados, não haverá otimização de registro nem bloqueio para o índice em si, mas as otimizações no índice columnstore clusterizado, conforme descrito acima, permanecerão.  
  
## Como o deltastore funciona  
 Os índices columnstore clusterizados coletam até 1.048.576 linhas em deltastore antes de compactá-las no rowgroup compactado. Isso melhora a compactação do índice columnstore. Quando um rowgroup deltastore contiver 1.048.576 linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marcará o rowgroup como fechado. Um processo em segundo plano, chamado *motor de tupla*, encontra cada rowgroup fechado e o compacta no columnstore  
  
 Para cada índice columnstore clusterizado, podem existir vários deltastores.  
  
-   Se um deltastore estiver bloqueado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará obter um bloqueio em outro deltastore. Se não houver nenhum deltastore disponível, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um novo deltastore.  
  
-   Para uma tabela particionada, poderá haver vários deltastores para cada partição.  
  
 Esses cenários descrevem quando as linhas carregadas vão diretamente para o columnstore ou quando elas vão para o deltastore.  
  
 No exemplo, cada rowgroup pode ter de 102.400 a 1.048.576 linhas por rowgroup. Na prática, o tamanho máximo de um rowgroup poderá ser inferior a 1.048.576 linhas quando houver pressão de memória.  
  
|Linhas para carregamento em massa|Linhas adicionadas ao rowgroup compactado|Linhas adicionadas ao rowgroup delta|  
|-----------------------|-------------------------------------------|--------------------------------------|  
|102.000|0|102.000|  
|145.000|145.000<br /><br /> Tamanho do rowgroup: 145.000|0|  
|1,048,577|1.048.576<br /><br /> Tamanho do rowgroup: 1.048.576.|1|  
|2,252,152|2,252,152<br /><br /> Tamanhos do rowgroup: 1.048.576, 1.048.576, 155.000.|0|  
  
 O exemplo a seguir mostra os resultados do carregamento de 1.048.577 linhas em uma tabela. Os resultados mostram um rowgroup COMPRESSED no columnstore (como segmentos de coluna compactados) e 1 linha no deltastore.  
  
```  
SELECT object_id, index_id, partition_number, row_group_id, delta_store_hobt_id, state state_desc, total_rows, deleted_rows, size_in_bytes   
FROM sys.dm_db_column_store_row_group_physical_stats  
```  
  
 ![Rowgroup and deltastore for a batch load](../../relational-databases/indexes/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  
## Carregar de uma tabela de preparo  
 Um padrão comum do carregamento de dados é carregar os dados em uma tabela de preparo, fazer alguma transformação e carregá-la na tabela de destino usando o comando a seguir  
  
```  
INSERT INTO <columnstore index>  SELECT <list of columns> FROM <Staging Table>  
  
```  
  
 Esse comando carrega os dados no índice columnstore de forma semelhante ao BCP ou à Inserção em Massa, mas em um único lote. Se o número de linhas na tabela de preparo for inferior a 102.400, as linhas serão carregadas em um rowgroup delta, caso contrário, as linhas serão carregadas diretamente no rowgroup compactado.  Uma importante limitação era que essa operação INSERT era single-threaded. Para carregar dados paralelamente, você podia criar várias tabelas de preparo ou emitir INSERT/SELECT com intervalos não sobrepostos de linhas da tabela de preparo.  Essa limitação não existe no SQL Server 2016. O comando abaixo carrega os dados da tabela de preparo paralelamente, mas você precisará especificar TABLOCK  
  
```  
INSERT INTO <columnstore index>  WITH (TABLOCK)  SELECT <list of columns> FROM <Staging Table>  
```  
  
 Veja as otimizações a seguir disponíveis ao fazer carregamento da tabela de preparo no índice columnstore clusterizado  
  
-   Otimização de log: minimamente registrado quando os dados forem carregados no rowgroup compactado. Não haverá registro mínimo quando os dados forem carregados no rowgroup delta.  
  
-   Otimização de bloqueio: no carregamento em um rowgroup compactado, o bloqueio X no rowgroup é adquirido. No entanto, com o rowgroup delta, um bloqueio X é adquirido em rowgroup, mas o SQL Server ainda bloqueia os bloqueios PAGE/EXTENT porque o bloqueio do rowgroup X não faz parte da hierarquia de bloqueio.  
  
 Se você tiver um ou mais índices não clusterizados, não haverá otimização de registro nem bloqueio para o índice em si, mas as otimizações no índice columnstore clusterizado, conforme descrito acima, permanecerão.  
  
## Carregar com inserção de fluxo  
 *Inserção de fluxo* refere-se à maneira que as linhas são carregadas no columnstore usando INSERT INTO. Cada linha é adicionada a um rowgroup delta. As linhas fluem diretamente para um rowgroup deltastore onde elas se acumulam até que o rowgroup seja fechado após atingir 1.048.576 linhas ou até que o índice columnstore seja recriado.  
  
```  
INSERT INTO <table-name> VALUES (<set of values>)  
```  
  
 Observe que os threads simultâneos que usam INSERT INTO para inserir valores em um índice columnstore clusterizado podem inserir linhas no mesmo rowgroup deltastore.  
  
 Depois que o rowgroup contiver 1.048.576 linhas, o rowgroup delta será marcado como fechado, mas ainda fica disponível para consultas e operações de atualização/exclusão, mas as linhas recentemente inseridas vão para um rowgroup deltastore existente ou recentemente criado. Há um thread em segundo plano, *TM (Motor de Tupla)*, que compacta os rowgroups delta fechados periodicamente a cada 5 minutos mais ou menos. Você pode invocar explicitamente o comando a seguir para compactar o rowgroup delta fechado  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE  
```  
  
 Se quiser forçar um rowgroup delta a ser fechado e compactado, você poderá executar o comando a seguir. Convém executar esse comando se você tiver terminado de carregar as linhas e não espera linhas novas. Ao fechar e compactar explicitamente o rowgroup delta, você poderá salvar mais armazenamento e melhorar o desempenho da consulta analítica. Uma prática recomendada é invocar esse comando se você não espera que novas linhas sejam inseridas.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE with (COMPRESS_ALL_ROW_GROUPS = ON)  
```  
  
## Carregar em uma tabela particionada  
 Para dados particionados, primeiro o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui cada linha a uma partição e, depois, executa operações columnstore nos dados na partição. Cada partição tem seus próprios rowgroups e pelo menos um deltastore.  
  
## Carregar em um índice columnstore não clusterizado  
 Em uma tabela rowstore com dados de um índice columnstore não clusterizado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre insere dados na tabela base. Os dados nunca são inseridos diretamente no índice columnstore.  
  
## Consulte também  
 [Guia de Índices Columnstore](../Topic/Columnstore%20Indexes%20Guide.md)   
 [Resumo de recursos com versão dos índices columnstore](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [Desempenho de consultas de índices ColumnStore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [Índices columnstore para Data Warehouse](../Topic/Columnstore%20Indexes%20for%20Data%20Warehousing.md)   
 [Desfragmentação de índices columnstore](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  