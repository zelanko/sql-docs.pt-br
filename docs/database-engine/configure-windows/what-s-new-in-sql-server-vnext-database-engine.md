---
title: "Novidades do SQL Server vNext (Mecanismo de Banco de Dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Novidades do SQL Server vNext (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

**Observação**: o SQL Server vNext também inclui os recursos adicionados nos service packs do SQL Server 2016. Para esses itens, consulte [Novidades do SQL Server 2016 (Mecanismo de Banco de Dados)](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).

## <a name="sql-server-database-engine-ctp-13"></a>Mecanismo de Banco de Dados do SQL Server (CTP 1.3)
- Melhorias indiretas de desempenho do ponto de verificação.
- Suporte a grupos de disponibilidade sem cluster adicionado.
- Configuração de Grupos de Disponibilidade de Confirmação de Réplica Mínima adicionada.
- Os Grupos de Disponibilidade agora podem trabalhar no Windows-Linux para permitir as migrações e testes entre sistemas operacionais.
- Suporte à Política de Retenção de Tabelas Temporais adicionado,
- Novo DMV SYS.DM_DB_STATS_HISTOGRAM
- Suporte à criação e recriação de índice de columnstore não clusterizado online adicionado
- Cinco novas exibições de gerenciamento dinâmico para retornar informações sobre o processo do Linux. Para saber mais, veja [Exibições de Gerenciamento Dinâmico de Processos do Linux](../../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) é adicionado para análise de estatísticas.

## <a name="sql-server-database-engine-ctp-12"></a>Mecanismo de Banco de Dados do SQL Server (CTP 1.2)

- O Database Tuning Advisor (DTA) lançado com o SQL Server Management Studio versão 16.4, ao analisar o SQL Server 2016 e posterior, tem opções adicionais.    
   - Desempenho aprimorado. Para saber mais, veja [Melhorias de desempenho usando as recomendações do Orientador de Otimização do Mecanismo de Banco de Dados (DTA)](../../relational-databases/performance/performance-improvements-using-dta-recommendations.md).
   - A opção `-fc` para permitir recomendações de índices de columnstore. Para saber mais, veja [Utilitário DTA](../../tools/dta/dta-utility.md) e [Recomendações de índice Columnstore no Orientador de Otimização do Mecanismo de Banco de Dados (DTA)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md).  
   - A opção `-iq` para permitir que o DTA analise uma carga de trabalho do Repositório de Consultas. Para saber mais, veja [Ajustar o Banco de Dados Usando Cargas de Trabalho do Repositório de Consulta](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md).
   

## <a name="sql-server-database-engine-ctp-11"></a>Mecanismo de Banco de Dados do SQL Server (CTP 1.1)

<a name="InMemoryBulletsCtp11"/>
- Para obter a funcionalidade na memória, aprimoramentos adicionais para tabelas otimizadas para memória e funções compiladas nativamente serão listadas abaixo e exemplos de código estarão disponíveis em um [texto subsequente](#InMemory_CodeSamples):
    - Suporte para colunas computadas em tabelas com otimização de memória, incluindo índices em colunas computadas.
    - Suporte completo para funções JSON em módulos compilados nativamente e em restrições de verificação.
    - Operador `CROSS APPLY` em módulos compilados nativamente.   
- Foram adicionadas as novas funções de cadeia de caracteres [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../../t-sql/functions/translate-transact-sql.md) e [TRIM](../../t-sql/functions/trim-transact-sql.md).   
- Agora há suporte para a cláusula `WITHIN GROUP` pela função [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md).
- Foram adicionadas duas novas famílias de agrupamento em japonês (Japanese_Bushu_Kakusu_140 e Japanese_XJIS_140), além da opção de agrupamento de Seletor sensível à variação (_VSS) para uso em agrupamentos em japonês. Para obter mais detalhes, consulte [Suporte a Agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
- As novas opções de acesso em massa, [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), permitem acessar os dados diretamente de um arquivo especificado como o formato CSV e de arquivos armazenados no Armazenamento de Blobs do Azure por meio da nova opção `BLOB_STORAGE` de [EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).


## <a name="sql-server-database-engine-ctp-10"></a>Mecanismo de Banco de Dados do SQL Server (CTP 1.0)

- **COMPATIBILITY_LEVEL** 140 do banco de dados foi adicionado.   Os clientes executando neste nível obterão os últimos recursos de linguagem e comportamentos de otimizador de consulta. Isso inclui alterações em cada versão de pré-lançamento que a Microsoft lançar.
- Melhorias na forma como os limites de atualização de estatísticas incrementais são computados (necessário modo de compatibilidade&140;).
- O [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) foi adicionado.
- Adicionamos vários aprimoramentos de desempenho e idioma para tabelas na memória:
    - Agora há suporte a `sp_spaceused` para tabelas na memória.
    - Agora há suporte a `sp_rename` para os módulos nativos.
    - Agora há suporte para instruções `CASE` para os módulos nativos.
    - A limitação de 8 índices em tabelas na memória foi removida.
    - Agora há suporte para `TOP (N) WITH TIES` nos módulos nativos.
    - `ALTER TABLE` em tabelas na memória agora é consideravelmente mais rápido em alguns casos.
    - A transação refazer tabelas na memória agora é executada em paralelo. Isso substancialmente reduz o tempo para fazer failovers ou reiniciar, em alguns casos.
    - Arquivos de ponto de verificação na memória agora podem ser armazenados no Armazenamento do Azure. Isso fornece funcionalidades equivalentes para arquivos MDF em comparação a arquivos LDF, que já têm essa capacidade.
- Índices Columnstore clusterizados agora oferecem suporte a colunas LOB (nvarchar(max), varchar(max), varbinary(max)).
- A função de agregação [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) foi adicionada.  
- Novas permissões: `DATABASE SCOPED CREDENTIAL` agora é uma classe de protegível, suporte `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP` e `VIEW DEFINITION` permissões. `ADMINISTER DATABASE BULK OPERATIONS` que é restrito ao banco de dados SQL agora está visível no `sys.fn_builtin_permissions`.   
- A DMV [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) foi adicionada para fornecer informações de sistema operacional para Windows e Linux.   
- As funções de banco de dados são criadas com R Services para gerenciar permissões associadas aos pacotes. Para obter mais informações, consulte [Gerenciamento de pacotes de R para o SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 
<a name="InMemory_CodeSamples"/> 
## <a name="code-samples-for-new-in-memory-enhancements"></a>Exemplos de código para novos aprimoramentos na memória

As subseções a seguir fornecem exemplos de código Transact-SQL que ilustram os novos recursos na memória que estão listados com marcadores no texto anterior neste artigo.

A lista de marcadores do CTP 1.1 para Na memória está [aqui](#InMemoryBulletsCtp11).

#### <a name="computed-column-in-a-memory-optimized-table"></a>Coluna computada em uma tabela com otimização de memória

Esta instrução CREATE TABLE ilustra os seguintes recursos que foram mencionados no texto sobre o CTP 1.1 anterior:

- Restrição CHECK JSON em uma coluna.
- Novas colunas computadas.
- Um índice em uma coluna computada.

```tsql
CREATE TABLE Product(
    ProductID  int            PRIMARY KEY NONCLUSTERED,
    Name       nvarchar(400)  NOT NULL,
    Price      float,

    Data      nvarchar(4000)  CONSTRAINT [Data contains JSON]  CHECK (ISJSON(Data)=1),

    MadeIn  AS CAST(JSON_VALUE(Data, '$.MadeIn')            as NVARCHAR(50)) PERSISTED,
    Cost    AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float       ),

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)
)
        WITH (MEMORY_OPTIMIZED=ON);
```

#### <a name="cross-apply-and-json-functions"></a>CROSS APPLY e as funções JSON

Esta instrução CREATE PROCEDURE, para um procedimento armazenado nativamente compilado, ilustra os seguintes recursos que foram mencionados no texto sobre o CTP 1.1 anterior:

- Operador CROSS APPLY.
- Funções JSON.

```tsql
CREATE OR ALTER PROCEDURE ProductList()
    WITH SCHEMABINDING, NATIVE_COMPILATION
as begin
    atomic with (transaction isolation level = snapshot,  language = N'English')

    SELECT
            ProductID, Name, Price, Tags,
            Data,
            JSON_VALUE(Data,'$.MadeIn') AS MadeIn,
            value
        FROM Product
        CROSS APPLY OPENJSON(Data, '$.SalesReasons')
        FOR JSON PATH
end;
```
