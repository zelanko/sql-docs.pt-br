---
title: "Introdução ao Columnstore para análise operacional em tempo real | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: e1328615-6b59-4473-8a8d-4f360f73187d
caps.latest.revision: 40
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e032da9604178eb356de35448eb5d53a9d663214
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="get-started-with-columnstore-for-real-time-operational-analytics"></a>Introdução ao Columnstore para análise operacional em tempo real
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  O SQL Server 2016 apresenta análise operacional em tempo real, a capacidade de executar cargas de trabalho OLTP e analíticas nas mesmas tabelas de banco de dados ao mesmo tempo. Além de executar análise em tempo real, você também pode eliminar a necessidade de ETL e de um data warehouse.  
  
## <a name="real-time-operational-analytics-explained"></a>Análise operacional em tempo real explicado  
 Tradicionalmente, as empresas tinham sistemas separados para cargas de trabalho operacionais (isto é, OLTP) e analíticas. Para tais sistemas, os trabalhos ETL (Extrair, Transformar e Carregar) movem os dados regularmente do repositório operacional para um repositório analítico. Os dados analíticos geralmente são armazenados em um data warehouse ou data mart dedicado para execução de consultas analíticas. Embora essa solução tenha sido o padrão, ela apresenta estes três desafios principais:  
  
-   **Complexidade.** Implementar o ETL pode exigir codificação considerável especialmente para carregar apenas as linhas modificadas. Pode haver complexidade na identificação de quais linhas foram modificadas.  
  
-   **Custo** Implementar o ETL exige o custo da compra de licenças adicionais de hardware e software.  
  
-   **Latência de dados.** Implementar o ETL adiciona um atraso para execução da análise. Por exemplo, se o trabalho ETL for executado no final de cada dia útil, as consultas analíticas serão executadas nos dados com pelo menos um dia. Para muitas empresas, esse atraso é inaceitável porque a empresa depende da análise de dados em tempo real. Por exemplo, a detecção de fraudes requer análise em tempo real em dados operacionais.  
  
 ![visão geral da análise operacional em tempo real](../../relational-databases/indexes/media/real-time-operational-analytics-overview.png "visão geral da análise operacional em tempo real")  
  
 A análise operacional em tempo real oferece uma solução para esses desafios.   
        Não há atraso algum quando as cargas de trabalho OLTP e analíticas são executadas na mesma tabela subjacente.   Em cenários que podem usar análise em tempo real, os custos e a complexidade são enormemente reduzidos com a eliminação da necessidade de ETL e da necessidade de compra e manutenção de um data warehouse separado.  
  
> [!NOTE]  
>  A análise operacional em tempo real visa o cenário de uma fonte de dados individual, como um aplicativo ERP (planejamento de recursos empresariais) no qual é possível executar a carga de trabalho operacional e analítica. Isso não substitui a necessidade de um data warehouse separado quando você precisar integrar dados de várias fontes antes de executar a carga de trabalho analítica ou quando você exigir desempenho extremo de análise usando dados pré-agregados, como cubos.  
  
 A análise em tempo real usa um índice columnstore atualizável em uma tabela rowstore.  O índice columnstore mantém uma cópia dos dados para que as cargas de trabalho OLTP e analítica sejam executadas em cópias separadas dos dados. Isso minimiza o impacto no desempenho de ambas as cargas de trabalho em execução ao mesmo tempo.  O SQL Server mantém automaticamente as mudanças no índice para que as alterações no OLTP estejam sempre atualizadas para análise. Com esse design, é possível e prático executar análise em tempo real em dados atualizados. Isso funciona para tabelas com otimização de memória e baseadas em disco.  
  
## <a name="get-started-example"></a>Exemplo de introdução  
 Para começar com a análise em tempo real:  
  
1.  Identifique as tabelas em seu esquema operacional que contenham dados obrigatórios para análise.  
  
2.  Em cada tabela, descarte todos os índices btree desenvolvidos basicamente para acelerar a análise existente em sua carga de trabalho OLTP. Substitua-os por um único índice columnstore.  Isso pode melhorar o desempenho geral da carga de trabalho OLTP, já que haverá menos índices para manter.  
  
    ```  
    --This example creates a nonclustered columnstore index on an existing OLTP table.  
    --Create the table  
    CREATE TABLE t_account (  
        accountkey int PRIMARY KEY,  
        accountdescription nvarchar (50),  
        accounttype nvarchar(50),  
        unitsold int  
    );  
  
    --Create the columnstore index with a filtered condition  
    CREATE NONCLUSTERED COLUMNSTORE INDEX account_NCCI   
    ON t_account (accountkey, accountdescription, unitsold)   
    ;  
  
    ```  
  
     O índice columnstore em uma tabela na memória permite análise operacional integrando tecnologias OLTP in-memory e columnstore in-memory para oferecer alto desempenho a cargas de trabalho OLTP e analíticas. O índice columnstore em uma tabela na memória deve incluir todas as colunas.  
  
    ```  
    -- This example creates a memory-optimized table with a columnstore index.  
    CREATE TABLE t_account (  
        accountkey int NOT NULL PRIMARY KEY NONCLUSTERED,  
        Accountdescription nvarchar (50),  
        accounttype nvarchar(50),  
        unitsold int,  
        INDEX t_account_cci CLUSTERED COLUMNSTORE  
        )  
        WITH (MEMORY_OPTIMIZED = ON );  
    GO  
  
    ```  
  
3.  Isso é tudo o que você precisa fazer!  
  
 Agora você está pronto para executar análise operacional em tempo real sem fazer alterações no seu aplicativo.  As consultas analíticas serão executadas no índice columnstore e as operações OLTP continuarão sendo executadas nos índices btree OLTP. As cargas de trabalho OLTP continuarão sendo executadas, mas incorrerão em alguma sobrecarga adicional para manter o índice columnstore. Veja as otimizações de desempenho na próxima seção.  
  
## <a name="blog-posts"></a>Postagens de blog  
 Leia as postagens no blog de Sunil Agarwal para saber mais sobre análise operacional em tempo real.  Talvez seja mais fácil entender as seções de dicas de desempenho se você ler essas postagens primeiro.  
  
-   [Business case for real-time operational analytics (Caso de negócios para análise operacional em tempo real)](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)  
  
-   [Using a nonclustered columnstore index for real-time operational analytics (Usando um índice columnstore não clusterizado para análise operacional em tempo real)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)  
  
-   [A simple example using a nonclustered columnstore index (Um exemplo simples usando um índice columnstore não clusterizado)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)  
  
-   [How SQL Server maintains a nonclustered columnstore index  on a transactional workload (Como o SQL Server mantém um índice columnstore não clusterizado em uma carga de trabalho transacional)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)  
  
-   [Minimizing the impact of nonclustered columnstore index maintenance by using a filtered index (Minimizando o impacto da manutenção do índice columnstore não clusterizado usando um índice filtrado)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)  
  
-   [Minimizing the impact of nonclustered columnstore index maintenance by using compression delay (Minimizando o impacto da manutenção do índice columnstore não clusterizado usando o atraso da compactação)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)  
  
-   [Minimizing impact of a nonclustered columnstore index maintenance by using compression delay - performance numbers (Minimizando o impacto da manutenção de um índice columnstore não clusterizado usando atraso de compactação — número de desempenho)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)  
  
-   [Real time operational analytics with memory-optimized tables (Análise operacional em tempo real com tabelas com otimização de memória)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)  
  
-   [Minimize index fragmentation in a columnstore indes (Minimizar fragmentação de índice em um índice columnstore)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
  
-   [Columnstore index and the merge policy for rowgroups (Índice columnstore e a política de mesclagem para rowgroups)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
## <a name="performance-tip-1-use-filtered-indexes-to-improve-query-performance"></a>Dica de desempenho nº 1: use índices filtrados para melhorar o desempenho da consulta  
 Executar a análise operacional em tempo real pode afetar o desempenho da carga de trabalho OLTP.  Esse impacto deve ser mínimo. O exemplo abaixo mostra como usar índices filtrados para minimizar o impacto do índice columnstore não clusterizado na carga de trabalho transacional enquanto ainda estiver entregando análise em tempo real.  
  
 Para minimizar a sobrecarga de manter um índice columnstore não clusterizado em uma carga de trabalho operacional, você pode usar uma condição filtrada para criar um índice columnstore não clusterizado apenas de dados *passivos* ou que mudam de modo constante e lento. Por exemplo, em um aplicativo de gerenciamento de pedidos, você pode criar um índice columnstore não clusterizado dos pedidos que já foram despachados. Depois que o pedido tiver sido enviado, ele raramente muda e, portanto, pode ser considerado como dados passivos. Com o índice filtrado, os dados no índice columnstore não clusterizado exigem menos atualizações, reduzindo, assim, o impacto na carga de trabalho transacional.  
  
 As consultas analíticas acessam de modo transparente os dados passivos e ativos, conforme a necessidade de fornecer análise em tempo real. Se uma parte significativa da carga de trabalho operacional estiver tocando os dados "ativos", essas operações não exigirão manutenção adicional do índice columnstore. Uma prática recomendada é ter um índice clusterizado rowstore em colunas usadas na definição do índice filtrado.   O SQL Server usa o índice clusterizado para verificar rapidamente as linhas que não atenderam à condição filtrada. Sem esse índice clusterizado, uma verificação de tabela completa da tabela rowstore será exigida para encontrar essas linhas, que podem afetar negativamente o desempenho da consulta analítica de modo significativo. Na ausência do índice clusterizado, você pode criar um índice btree não clusterizado filtrado complementar para identificar tais linhas, mas não é recomendado, pois acessar grandes intervalos de linhas por meio de índices btree não clusterizados custa caro.  
  
> [!NOTE]  
>  Um índice columnstore não clusterizado filtrado é permitido apenas em tabelas baseadas em disco. Ele não é permitido em tabelas com otimização de memória  
  
### <a name="example-a-access-hot-data-from-btree-index-warm-data-from-columnstore-index"></a>Exemplo A: acessar dados ativos do índice btree, dados passivos do índice columnstore  
 Este exemplo usa uma condição filtrada (accountkey > 0) para estabelecer quais linhas estarão no índice columnstore. O objetivo é criar a condição filtrada e as consultas subsequentes para acessar dados "ativos" que mudam frequentemente no índice btree e acessar os dados "passivos" mais estáveis no índice columnstore.  
  
 ![Índices combinados para dados ativos e passivos](../../relational-databases/indexes/media/de-columnstore-warmhotdata.png "Índices combinados para dados ativos e passivos")  
  
> [!NOTE]  
>  O otimizador de consulta vai considerar, mas nem sempre escolherá, o índice columnstore para o plano de consulta. Quando o otimizador de consulta escolher o índice columnstore filtrado, ele combinará de modo transparente as linhas do índice columnstore, bem como as linhas que não atendem à condição filtrada para permitir análise em tempo real. Isso é diferente de um índice filtrado não clusterizado regular, que pode ser usado apenas em consultas que restringem a si mesmas a linhas presentes no índice.  
  
```  
--Use a filtered condition to separate hot data in a rowstore table  
-- from “warm” data in a columnstore index.  
  
-- create the table  
CREATE TABLE  orders (  
         AccountKey         int not null,  
         Customername       nvarchar (50),  
        OrderNumber         bigint,  
        PurchasePrice       decimal (9,2),  
        OrderStatus         smallint not null,  
        OrderStatusDesc     nvarchar (50))  
  
-- OrderStatusDesc  
-- 0 => 'Order Started'  
-- 1 => 'Order Closed'  
-- 2 => 'Order Paid'  
-- 3 => 'Order Fullfillment Wait'  
-- 4 => 'Order Shipped'  
-- 5 => 'Order Received'  
  
CREATE CLUSTERED INDEX  orders_ci ON orders(OrderStatus)  
  
--Create the columnstore index with a filtered condition  
CREATE NONCLUSTERED COLUMNSTORE INDEX orders_ncci ON orders  (accountkey, customername, purchaseprice, orderstatus)  
where orderstatus = 5  
;  
  
-- The following query returns the total purchase done by customers for items > $100 .00  
-- This query will pick  rows both from NCCI and from 'hot' rows that are not part of NCCI  
SELECT top 5 customername, sum (PurchasePrice)  
FROM orders  
WHERE purchaseprice > 100.0   
Group By customername  
```  
  
 A consulta analítica será executada com o plano de consulta a seguir. Você pode ver que as linhas que não atendem à condição filtrada são acessadas por meio do índice btree clusterizado.  
  
 ![Plano de consulta](../../relational-databases/indexes/media/query-plan-columnstore.png "Plano de consulta")  
  
 Veja o blog para obter detalhes sobre o [índice columnstore não clusterizado filtrado.](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)  
  
## <a name="performance-tip-2-offload-analytics-to-always-on-readable-secondary"></a>Dica de desempenho nº 2: transferir a análise para o secundário legível Always On  
 Mesmo que você possa minimizar a manutenção do índice columnstore usando um índice columnstore filtrado, as consultas analíticas ainda podem exigir recursos consideráveis de computação (CPU, E/S, memória), que afetam o desempenho da carga de trabalho operacional. Para a maioria das cargas de trabalho de missão crítica, nossa recomendação é usar a configuração Always On. Nessa configuração, você pode eliminar o impacto de executar a análise transferindo-a para um secundário legível.  
  
## <a name="performance-tip-3-reducing-index-fragmentation-by-keeping-hot-data-in-delta-rowgroups"></a>Dica de desempenho nº 3: reduzir a fragmentação de índice mantendo dados ativos em rowgroups delta  
 Tabelas com índice columnstore poderão ser significativamente fragmentadas (isto é, linhas excluídas) se a carga de trabalho atualizar/excluir linhas que foram compactadas. Um índice columnstore fragmentado leva à utilização ineficaz de memória/armazenamento. Além do uso ineficaz de recursos, ele também afeta negativamente o desempenho da consulta de análise devido à E/S extra e à necessidade de filtrar as linhas excluídas no conjunto de resultados.  
  
 As linhas excluídas não são fisicamente removidas até que você execute a desfragmentação do índice com o comando REORGANIZE ou recrie o índice columnstore na tabela inteira ou nas partições afetadas. REORGANIZE e INDEX REBUILD são operações caras que eliminam recursos que, de outra forma, poderiam ser usados para a carga de trabalho. Além disso, no caso de linhas compactadas com muita antecedência, talvez elas precisem ser recompactadas várias vezes devido às atualizações, gerando sobrecarga desnecessária de compactação.  
Você pode minimizar a fragmentação de índice usando a opção COMPRESSION_DELAY.  
  
```  
  
-- Create a sample table  
create table t_colstor (  
               accountkey                      int not null,  
               accountdescription              nvarchar (50) not null,  
               accounttype                     nvarchar(50),  
               accountCodeAlternatekey         int)  
  
-- Creating nonclustered columnstore index with COMPRESSION_DELAY. The columnstore index will keep the rows in closed delta rowgroup for 100 minutes   
-- after it has been marked closed  
CREATE NONCLUSTERED COLUMNSTORE index t_colstor_cci on t_colstor (accountkey, accountdescription, accounttype)   
                       WITH (DATA_COMPRESSION= COLUMNSTORE, COMPRESSION_DELAY = 100);  
  
;  
```  
  
 Veja o blog para obter detalhes sobre [atraso na compactação.](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)  
  
 Veja as práticas recomendadas  
  
-   **Inserir/consultar a carga de trabalho:**se a carga de trabalho for basicamente inserir dados e consultá-los, o padrão COMPRESSION_DELAY de 0 será a opção recomendada. As linhas recentemente inseridas serão compactadas uma vez que 1 milhão de linhas foram inseridas em um único rowgroup delta.  
    Alguns exemplos de tal carga de trabalho são (a) carga de trabalho DW tradicional (b) análise de fluxo de clique quando você precisa analisar o padrão de clique em um aplicativo Web.  
  
-   **Carga de trabalho OLTP:** se a carga de trabalho for DML pesada (isto é, combinação pesada de Atualizar, Excluir e Inserir), você poderá ver a fragmentação do índice columnstore examinando o sys DMV. dm_db_column_store_row_group_physical_stats. Caso veja que mais de 10% das linhas são marcadas como excluídas em rowgroups recentemente compactados, você poderá usar a opção COMPRESSION_DELAY para adicionar atraso quando as linhas se tornarem qualificadas para compactação. Por exemplo, se para sua carga de trabalho, os dados recentemente inseridos permanecerem "ativos" (isto é, forem atualizados várias vezes) digamos que por 60 minutos, você deverá escolher COMPRESSION_DELAY para ser 60.  
  
 Esperamos que a maioria dos clientes não precise fazer nada. O valor padrão da opção COMPRESSION_DELAY deve funcionar para eles.  
Para usuários avançados, é recomendável executar a consulta abaixo e coletar a % de linhas excluídas nos últimos 7 dias.  
  
```  
SELECT row_group_id,cast(deleted_rows as float)/cast(total_rows as float)*100 as [% fragmented], created_time  
FROM sys. dm_db_column_store_row_group_physical_stats  
WHERE object_id = object_id('FactOnlineSales2')   
             AND  state_desc='COMPRESSED'   
             AND deleted_rows>0   
             AND created_time > GETDATE() - 7  
ORDER BY created_time DESC  
```  
  
 Se o número de linhas excluídas em rowgroups compactados for superior a 20%, lidando com rowgroups antigos com variação inferior a 5% (referido como rowgroups frios) defina COMPRESSION_DELAY = (youngest_rowgroup_created_time –  current_time). Observe que essa abordagem funciona melhor com uma carga de trabalho relativamente homogênea e estável.  
  
## <a name="see-also"></a>Consulte também  
 [Guia de Índices Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)   
 [Carregamento de dados dos índices columnstore](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Desempenho de consultas de índices ColumnStore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Índices columnstore para Data Warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Desfragmentação de índices columnstore](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  

