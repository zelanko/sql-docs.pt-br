---
title: "Início Rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL | Microsoft Docs"
ms.custom: 
ms.date: 09/05/2017"
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 31f39703450ba5fdb157a7d3fd88f6459d222c77
ms.sourcegitcommit: ea68e8a68ee58584dd52035ed3d611a69b6c3818
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2017
---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>Pesquisa de áreas iniciais em OLTP in-memory
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
Este artigo é para o desenvolvedor que está com pressa para aprender os fundamentos dos recursos de desempenho do OLTP in-memory do Microsoft SQL Server e do Banco de Dados SQL do Azure.  
  
Para o OLTP in-memory, este artigo fornece o seguinte:  
  
- Explicações rápidas dos recursos.  
- Exemplos do código principal que implementam os recursos.  
  
  
O SQL Server e o Banco de dados SQL têm apenas pequenas variações no suporte de tecnologia in-memory.  
  
  
No mundo real, os blogueiros se referem ao OLTP in-memory como *Hekaton*.  
  
  
<a name="benefits-of-in-memory-features-21a"></a>  
  
## <a name="benefits-of-in-memory-features"></a>Benefícios dos recursos In-Memory  
  
O SQL Server fornece recursos In-Memory que podem melhorar muito o desempenho de vários sistemas de aplicativos. As considerações mais simples estão descritas nesta seção.  
  
  
### <a name="features-for-oltp-online-transactional-processing"></a>Recursos para OLTP (Processamento de Transações Online)  
  
  
Sistemas que devem processar grandes números de INSERTs do SQL simultaneamente são excelentes candidatos para recursos do OLTP.  
  
- Nossos parâmetros de comparação mostram que é possível obter melhorias de velocidade de 5 a 20 vezes mais rápidas pela adoção de recursos In-Memory.  
  
  
Sistemas que processam cálculos pesados no Transact-SQL são excelentes candidatos.  
  
- Um procedimento armazenado que é dedicado a cálculos pesados pode ser executado até 99 vezes mais rápido.  
  
  
Posteriormente, você pode visitar os seguintes artigos que oferecem demonstrações de ganhos de desempenho do OLTP in-memory:  
  
- [Demonstração: aprimoramento do desempenho do OLTP in-memory](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) oferece uma demonstração em pequena escala dos maiores ganhos potenciais de desempenho.  
- O [banco de dados de exemplo para o OLTP In-Memory](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) oferece uma demonstração de escala maior.  
  
  
  
### <a name="features-for-operational-analytics"></a>Recursos de análise operacional  
  
A análise in-memory refere-se aos SELECTs do SQL, que agregam dados transacionais, normalmente pela inclusão de uma cláusula GROUP BY. O tipo de índice chamado *columnstore* é central para análise operacional.  
  
Há dois cenários principais:  
  
- *Análise operacional em lote* refere-se aos processos de agregação que são executados após o horário comercial ou no hardware secundário, que tem cópias dos dados transacionais.  
  - [SQL Data Warehouse do Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-what-is/) também está relacionada à análise operacional em lote.  
- *Análise operacional em tempo real* refere-se aos processos de agregação que são executados durante o horário comercial e no hardware principal que é usado para cargas de trabalho transacionais.  
  
  
O presente artigo se concentra em OLTP e não em Análises. Para obter informações sobre como os índices columnstore trazem as Análises para o SQL, confira:  
  
- [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
- [Guia de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
> [!NOTE]
> Um vídeo de dois minutos sobre os recursos In-Memory está disponível no [Banco de Dados SQL do Azure - Tecnologias In-Memory](http://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-In-Memory-Technologies). O vídeo é de dezembro de 2015.  


### <a name="columnstore"></a>columnstore

Uma sequência de postagens de blog excelente explica elegantemente os índices columnstore de várias perspectivas. A maioria das postagens descreve o conceito de análise operacional em tempo real, à qual o columnstore dá suporte.  Essas postagens foram criadas por Sunil Agarwal, gerente de programa da Microsoft, em março de 2016.

#### <a name="real-time-operational-analytics"></a>Análise operacional em tempo real

1. [Análise operacional em tempo real usando a tecnologia in-memory](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)
2. [Análise operacional em tempo real – Visão geral do NCCI (índice columnstore não clusterizado)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)
3. [Análise operacional em tempo real: exemplo simples usando NCCI (índice columnstore não clusterizado) no SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)
4. [Análise operacional em tempo real: operações DML e NCCI (índice columnstore não clusterizado) no SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)
5. [Análise operacional em tempo real: NCCI (índice columnstore não clusterizado) filtrado](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)
6. [Análise operacional em tempo real: opção de atraso na compactação para NCCI (índice columnstore não clusterizado)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)
7. [Análise operacional em tempo real: opção de atraso na compactação com NCCI e desempenho](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)
8. [Análise operacional em tempo real: tabelas com otimização de memória e índice columnstore](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)

#### <a name="defragment-a-columnstore-index"></a>Desfragmentar um índice columnstore

1. [Desfragmentação de índice columnStore usando o comando REORGANIZE](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)
2. [Política de mesclagem do índice columnstore para REORGANIZE](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)

#### <a name="bulk-importation-of-data"></a>Importação em massa de dados

1. [Repositório de colunas clusterizado: carregamento em massa](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2014/07/27/clustered-column-store-index-bulk-loading-the-data/)
2. [Índice columnstore clusterizado: otimizações de carregamento de dados – log mínimo](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/10/clustered-columnstore-index-data-load-optimizations-minimal-logging/)
3. [Índice columnstore clusterizado: otimização de carregamento de dados – importação paralela em massa](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/28/clustered-columnstore-index-parallel-bulk-import/)





<a name="features-on-in-memory-oltp-13b"></a>  
  
## <a name="features-of-in-memory-oltp"></a>Recursos do OLTP in-memory  
  
Vejamos os principais recursos do OLTP in-memory.  
  
  
#### <a name="memory-optimized-tables"></a>Tabelas com otimização de memória  
  
A palavra-chave do T-SQL MEMORY_OPTIMIZED, na instrução CREATE TABLE, é como a tabela é criada para existir na memória ativa em vez de no disco.  
  
  
Uma [Tabela com otimização de memória](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) tem uma representação de si mesma na memória ativa e na cópia secundária no disco.  
  
- A cópia em disco é destinada para a recuperação da rotina depois de uma reinicialização após o desligamento do servidor ou do banco de dados. Essa dualidade de memória mais disco é completamente oculta para você e para seu código.  
  
  
#### <a name="natively-compiled-modules"></a>Módulos compilados nativamente  
  
A palavra-chave do T-SQL NATIVE_COMPILATION, na instrução CREATE PROCEDURE, é como um procedimento armazenado compilado de forma nativa é criado. As instruções T-SQL são compiladas para código de computador no primeiro uso do proc nativo toda vez que o banco de dados é alternado online. As instruções T-SQL não suportam mais a interpretação lenta de cada instrução.  
  
- Vimos o resultado da compilação nativa em durações que tem de uma a 100 vezes a duração interpretada.  
  
  
Um módulo nativo pode fazer referência apenas às tabelas com otimização de memória e não podem fazer referência às tabelas baseadas em disco.  
  
Há três tipos de módulos compilados nativamente:  
  
- [Procedimentos armazenados compilados de modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
- Funções definidas pelo usuário (UDFs), que são escalares, compiladas de modo nativo.  
- Gatilhos compilados de modo nativo.  
  
  
#### <a name="availability-in-azure-sql-database"></a>Disponibilidade no Banco de Dados SQL do Azure  
  
O OLTP in-memory e o Columnstore estão disponíveis no banco de dados SQL. Para obter detalhes, veja [Otimizar o desempenho usando tecnologias in-memory no banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory).
  
  
<a name="ensure-compatibility-level-gteq-130-99c"></a>  
  
## <a name="1-ensure-compatibility-level--130"></a>1. Garantir o nível de compatibilidade >= 130  
  
  
Essa seção inicia uma sequência de sessões numeradas que, juntas, demonstram a sintaxe do Transact-SQL que pode ser usada para implementar recursos do OLTP in-memory.  
  
  
Primeiro, é importante que seu banco de dados seja definido para um nível de compatibilidade de pelo menos 130. Next é o código do T-SQL para exibir o nível de compatibilidade efetivo para o qual seu banco de dados atual está definido.  
  
  
  
  
  
    SELECT d.compatibility_level  
        FROM sys.databases as d  
        WHERE d.name = Db_Name();  
  
  
  
  
Next é o código do T-SQL para atualizar o nível, se necessário.  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET COMPATIBILITY_LEVEL = 130;  
  
  
  
  
<a name="elevate-to-snapshot-26n"></a>  
  
## <a name="2-elevate-to-snapshot"></a>2. Elevar para o INSTANTÂNEO  
  
  
Quando uma transação envolve tanto uma tabela baseada em disco quanto uma tabela com otimização de memória, chamamos esse procedimento de *transação entre contêineres*. Em tal transação, é essencial que a porção com otimização de memória da transação opere no nível de isolamento da transação chamado INSTANTÂNEO.  
  
Para impor com segurança este nível para as tabelas com otimização de memória em uma transação entre contêineres, [altere sua configuração de banco de dados](../../t-sql/statements/alter-database-transact-sql-set-options.md) executando o T-SQL a seguir.  
  
  
  
  
    ALTER DATABASE CURRENT  
        SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
  
  
  
  
<a name="create-an-optimized-filegroup-24r"></a>  
  
## <a name="3-create-an-optimized-filegroup"></a>3. Criar um GRUPO DE ARQUIVOS otimizado  
  
  
No Microsoft SQL Server, antes de criar uma tabela com otimização de memória, você deve primeiro criar um grupo de arquivos que você declare como CONTAINS MEMORY_OPTIMIZED_DATA. O GRUPO DE ARQUIVOS é atribuído ao seu banco de dados. Para obter detalhes, confira:  
  
- [GRUPO DE ARQUIVOS com otimização de memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
  
No Banco de Dados SQL do Azure, você não precisa, e não pode, criar um GRUPO DE ARQUIVOS.  

O exemplo de script T-SQL a seguir habilita um banco de dados para OLTP in-memory e define todas as configurações recomendadas. Ele funciona com o SQL Server e o Banco de Dados SQL do Azure: [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql).

Observe que nem todos os recursos do SQL Server têm o suporte para os bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA. Para obter mais detalhes sobre as limitações, consulte [Recursos do SQL Server sem suporte no OLTP in-memory](unsupported-sql-server-features-for-in-memory-oltp.md)
  
<a name="create-a-memory-optimized-table-26y"></a>  
  
## <a name="4-create-a-memory-optimized-table"></a>4. Criar uma tabela com otimização de memória  
  
A palavra-chave fundamental do Transact-SQL é MEMORY_OPTIMIZED.  
  
  
  
  
    CREATE TABLE dbo.SalesOrder  
    (  
        SalesOrderId   integer        not null  IDENTITY  
            PRIMARY KEY NONCLUSTERED,  
        CustomerId     integer        not null,  
        OrderDate      datetime       not null  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
  
As instruções INSERT e SELECT do Transact-SQL em relação a uma tabela com otimização de memória são as mesmas que para uma tabela normal.  
  
#### <a name="alter-table-for-memory-optimized-tables"></a>ALTER TABLE para tabelas com otimização de memória  
  
ALTER TABLE...ADD/DROP pode adicionar ou remover uma coluna de uma tabela com otimização de memória ou de um índice.  
  
- CREATE INDEX e DROP INDEX não podem ser executados em uma tabela com otimização de memória; em vez disso, use .ALTER TABLE... ADD/DROP INDEX.  
- Para obter detalhes, confira [Alterando tabelas com otimização de memória](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).  
  
  
#### <a name="plan-your-memory-optimized-tables-and-indexes"></a>Planejar suas tabelas com otimização de memória  
  
  
- [Índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
- [Construções do Transact-SQL sem suporte pelo OLTP na memória](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
  
<a name="create-a-natively-compiled-stored-procedure-native-proc-29u"></a>  
  
## <a name="5-create-a-natively-compiled-stored-procedure-native-proc"></a>5. Criar um procedimento armazenado compilado de modo nativo (proc. nativo)  
  
  
A palavra-chave fundamental é NATIVE_COMPILATION.  
  
  
  
  
    CREATE PROCEDURE ncspRetrieveLatestSalesOrderIdForCustomerId  
        @_CustomerId   INT  
        WITH  
            NATIVE_COMPILATION,  
            SCHEMABINDING  
    AS  
    BEGIN ATOMIC  
        WITH  
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
            LANGUAGE = N'us_english')  
      
        DECLARE @SalesOrderId int, @OrderDate datetime;  
      
        SELECT TOP 1  
                @SalesOrderId = s.SalesOrderId,  
                @OrderDate    = s.OrderDate  
            FROM dbo.SalesOrder AS s  
            WHERE s.CustomerId = @_CustomerId  
            ORDER BY s.OrderDate DESC;  
      
        RETURN @SalesOrderId;  
    END;  
  
  
  
  
A palavra-chave SCHEMABINDING indica que as tabelas referidas no procedimento nativo não podem ser descartadas, a menos que o proc. nativo seja descartado primeiro. Para obter detalhes, confira [Criando procedimentos armazenados compilados de modo nativo](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md).  
  
Observe que você não precisa criar um procedimento armazenado compilado de modo nativo para acessar uma tabela com otimização de memória. Você também pode fazer referência a tabelas com otimização de memória dos procedimentos armazenados e lotes ad hoc tradicionais.
  
<a name="execute-the-native-proc-31e"></a>  
  
## <a name="6-execute-the-native-proc"></a>6. Executar o proc. nativo  
  
  
Preencha a tabela com duas linhas de dados.  
  
  
  
  
    INSERT into dbo.SalesOrder  
            ( CustomerId, OrderDate )  
        VALUES  
            ( 42, '2013-01-13 03:35:59' ),  
            ( 42, '2015-01-15 15:35:59' );  
  
  
  
  
Uma chamada do tipo EXECUTAR para o procedimento armazenado compilado de modo nativo é reproduzida.  
  
  
  
  
    DECLARE @LatestSalesOrderId int, @mesg nvarchar(128);  
      
    EXECUTE @LatestSalesOrderId =  
        ncspRetrieveLatestSalesOrderIdForCustomerId 42;  
      
    SET @mesg = CONCAT(@LatestSalesOrderId,  
        ' = Latest SalesOrderId, for CustomerId = ', 42);  
    PRINT @mesg;  
      
    -- Here is the actual PRINT output:  
    -- 2 = Latest SalesOrderId, for CustomerId = 42  
  
  
  
  
<a name="guide-to-the-documentation-and-next-steps-32w"></a>  
  
### <a name="guide-to-the-documentation-and-next-steps"></a>Guia para a documentação e próximas etapas  
  
  
Os exemplos simples anteriores oferecem uma base para aprender os recursos mais avançados do OLTP in-memory. As seções a seguir são um guia para as considerações especiais que talvez você precise saber e onde você pode conferir os detalhes sobre cada uma.  
  
  
  
<a name="how-do-in-memory-oltp-features-work-so-much-faster-33v"></a>  
  
## <a name="how-in-memory-oltp-features-work-so-much-faster"></a>Como os recursos do OLTP in-memory funcionam com muito mais rapidez?  
  
  
As subseções a seguir descrevem brevemente como os recursos do OLTP in-memory funcionam internamente para fornecer um desempenho aprimorado.  
  
  
<a name="how-do-memory-optimized-tables-perform-faster-34q"></a>  
  
### <a name="how-memory-optimized-tables-perform-faster"></a>Como as tabelas com otimização de memória têm um desempenho mais rápido?  
  
  
**Natureza dupla:** uma tabela com otimização de memória tem uma natureza dupla: uma representação na memória ativa e a outra no disco rígido. Cada transação está comprometida com ambas as representações da tabela. As transações operam contra a muito mais rápida representação de memória ativa. As tabelas com otimização de memória se beneficiam da maior velocidade da memória ativa em comparação ao disco. Além disso, a maior agilidade da memória ativa torna prática uma estrutura de tabela mais avançada, que é otimizada para a velocidade. A estrutura avançada também não tem páginas, por isso evita a sobrecarga e a contenção de travas e spinlocks.  
  
  
**Nenhum bloqueio:** a tabela com otimização de memória se baseia em uma abordagem *otimista* para os objetivos concorrentes de integridade de dados em relação à simultaneidade e alta taxa de transferência. Durante a transação, a tabela não coloca bloqueios em qualquer versão de linhas atualizadas dos dados. Isso pode reduzir significativamente a contenção em alguns sistemas de alto volume.  
  
  
**Versões de linha:** em vez de bloqueios, a tabela com otimização de memória adiciona uma nova versão de uma linha atualizada na tabela em si, não no tempdb. A linha original é mantida até que a transação seja confirmada. Durante a transação, outros processos podem ler a versão original da linha.  
  
- Quando várias versões de uma linha são criadas para uma tabela baseada em disco, as versões de linha são armazenadas temporariamente no tempdb.  
  
  
**Menos registros em log:** as versões anteriores e posteriores das linhas atualizadas são mantidas na tabela com otimização de memória. O par de linhas fornece grande parte das informações que tradicionalmente são gravadas no arquivo de log. Isso permite que o sistema grave menos informações, e com menos frequência, no log. No entanto, a integridade transacional é garantida.  
  
  
<a name="how-do-native-procs-perform-faster-35x"></a>  
  
### <a name="how-native-procs-perform-faster"></a>Como os proc. nativos têm um desempenho mais rápido?  
  
A conversão de um procedimento regular armazenado e interpretado para um procedimento armazenado compilado de modo nativo reduz significativamente o número de instruções a serem realizadas durante o tempo de execução.  
  
  
<a name="trade-offs-of-in-memory-features-36j"></a>  
  
## <a name="trade-offs-of-in-memory-features"></a>Vantagens e desvantagens dos recursos In-Memory  
  
  
Como é comum na ciência da computação, os ganhos de desempenho fornecidos pelos recursos de memória são uma compensação. Os melhores recursos trazem benefícios que são mais valiosos do que os custos extras do recurso. Você pode encontrar diretrizes abrangentes sobre as vantagens e desvantagens em:

- [Planejar a adoção de recursos de OLTP in-memory no SQL Server](../../relational-databases/in-memory-oltp/plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)

O restante desta seção lista algumas das principais considerações sobre planejamento e vantagens e desvantagens.
  
<a name="trade-offs-of-memory-optimized-tables-37d"></a>  
  
### <a name="trade-offs-of-memory-optimized-tables"></a>Vantagens e desvantagens das tabelas com otimização de memória  
  
  
**Estimar memória:** você deve estimar a quantidade de memória ativa que sua tabela com otimização de memória consumirá. Seu sistema de computador deve ter capacidade de memória suficiente para hospedar uma tabela com otimização de memória. Para obter detalhes, confira:  
  
- [Monitorar e solucionar problemas de uso da memória](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)  
- [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Tamanho da tabela e da linha em tabelas com otimização de memória](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
**Dividir a tabela grande em partes:** uma forma de atender à demanda de muita memória ativa é dividir a tabela grande em partes na memória, que armazenam as linhas de dados *ativas recentes* em relação às outras partes do disco que armazenam as linhas *herdadas inativas* (como pedidos de venda que foram totalmente enviados e concluídos). Esse particionamento é um processo manual de design e implementação. Consulte:  
  
- [Particionamento de nível de aplicativo](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
- [Padrão de aplicativo para particionamento de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
<a name="trade-offs-of-native-procs-38p"></a>  
  
### <a name="trade-offs-of-native-procs"></a>Vantagens e desvantagens dos proc. nativos  
  
- Um procedimento armazenado compilado de modo nativo não pode acessar uma tabela baseada em disco. Um proc. nativo pode acessar somente as tabelas com otimização de memória.  
- Quando um processo nativo for executado pela primeira vez depois que o servidor ou o banco de dados tiver sido colocado online novamente, o proc. nativo deverá ser recompilado uma vez. Isso causa um atraso antes do proc. nativo começar a ser executado.  
  
<a name="advanced-considerations-for-memory-optimized-tables-39n"></a>  
  
## <a name="advanced-considerations-for-memory-optimized-tables"></a>Considerações avançadas das tabelas com otimização de memória  
  
Os[Índices para as tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) são diferentes de algumas maneiras dos índices em tabelas em disco tradicionais. Os Índices de Hash estão disponíveis apenas em tabelas com otimização de memória.
    
- [Índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index)
- [Índice não clusterizado para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index) 
  
Você deve planejar para garantir que haverá memória ativa suficiente para sua tabela planejada de otimização de memória e seus índices. Consulte:  
  
- [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
Uma tabela com otimização de memória pode ser declarada com DURABILITY = SCHEMA_ONLY:  
  
- Essa sintaxe informa ao sistema para descartar todos os dados da tabela com otimização de memória quando o banco de dados é colocado offline. Somente a definição da tabela é persistida.  
- Quando o banco de dados for colocado online novamente, a tabela com otimização de memória será carregada outra vez na memória ativa, vazia de dados.  
- Tabelas SCHEMA_ONLY podem ser uma excelente [alternativa às tabelas de #temporary](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) em tempdb, quando vários milhares de linhas estão envolvidos.  
  
Variáveis de tabela também podem ser declaradas como com otimização de memória. Consulte:  
  
- [Tabela temporária e variável de tabela mais rápidas usando a otimização de memória](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)  
  
<a name="advanced-considerations-for-natively-compiled-modules-40k"></a>  
  
## <a name="advanced-considerations-for-natively-compiled-modules"></a>Considerações avançadas dos módulos compilados de modo nativo  
  
Os tipos de módulos compilados de modo nativo disponíveis por meio do Transact-SQL são:  
  
- Procedimentos armazenados compilados de modo nativo (proc. nativos).  
- [Funções escalares definidas pelo usuário](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)compiladas de modo nativo.  
- Gatilhos compilados de modo nativo (gatilhos nativos).  
  - Apenas os gatilhos que são compilados de modo nativo são permitidos em tabelas com otimização de memória.  
- [Funções com valor de tabela](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)compiladas de modo nativo.  
  - [Melhorando o desempenho da tabela temporária e da variável de tabela usando a otimização de memória](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)  
  
Uma UDF (função definida pelo usuário) compilada nativamente é executada muito mais rapidamente do que uma UDF interpretada. Aqui estão alguns pontos a considerar com UDFs:  
  
- Quando um T-SQL SELECT usa um UDF, o UDF é sempre chamado uma vez por linha retornada.  
  - As UDFs nunca são executadas de forma embutida, em vez disso, sempre são chamadas.  
  - A diferença compilada será menos significativa do que a sobrecarga de chamadas repetidas inerentes a todas as UDFs.  
  - Ainda assim, a sobrecarga de chamadas a UDF geralmente é aceitável no nível de prática.  
  
Para dados de teste e explicação sobre o desempenho dos UDFs nativos, consulte:  
  
  - [Suavizar o impacto do RBAR com UDFs nativas compiladas no SQL Server 2016](https://blogs.msdn.microsoft.com/sqlcat/2016/02/17/soften-the-rbar-impact-with-native-compiled-udfs-in-sql-server-2016/)  
  - Postagem no blog [Natively Compiled User Defined Functions](http://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/) (Funções definidas pelo usuário compiladas nativamente) por Gail Shaw, de janeiro de 2016.  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>Guia de documentação das tabelas com otimização de memória  
  
Consulte estes outros links que abordam considerações especiais para tabelas com otimização de memória:  
  
- [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  - [Determinando se uma tabela ou um procedimento armazenado deve ser movido para OLTP in-memory](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)  
  - O relatório de análise de desempenho de transação no SQL Server Management Studio ajuda você a avaliar se o OLTP in-memory melhorará o desempenho do seu aplicativo de banco de dados.  
  - Use o [Orientador de Otimização de Memória](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) para ajudar você a migrar a tabela de banco de dados baseada em disco para o OLTP in-memory.   
- [Backup, restauração e recuperação de tabelas com otimização de memória](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  - O armazenamento usado por tabelas com otimização de memória pode ser muito maior do que seu tamanho em memória e afeta o tamanho do backup do banco de dados.  
- [Transações com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)  
  - Incluem informações sobre a lógica de repetição no T-SQL, para transações em tabelas com otimização de memória.  
- [Suporte ao Transact-SQL para OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  - T-SQL e tipos de dados com e sem suporte, para tabelas com otimização de memória e proc. nativos.  
- [Associar um banco de dados às tabelas com otimização de memória para um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md), que discute uma consideração avançada opcional.  

<a name="documentation-guide-for-native-procs-42b"></a>  
  
## <a name="documentation-guide-for-native-procs"></a>Guia de documentação dos proc. nativos  

O seguinte artigo e seus artigos filho no sumário, explicam os detalhes sobre procedimentos armazenados compilados nativamente.

- [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>Links relacionados  
  
- Artigo inicial: [OLTP in-memory &#40;otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
    
Aqui estão os artigos que oferecem o código para demonstrar os ganhos de desempenho que você pode obter usando OLTP in-memory:  
  
- [Demonstração: aprimoramento do desempenho do OLTP in-memory](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) oferece uma demonstração em pequena escala dos maiores ganhos potenciais de desempenho.  
- O [banco de dados de exemplo para o OLTP In-Memory](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) oferece uma demonstração de escala maior.  
