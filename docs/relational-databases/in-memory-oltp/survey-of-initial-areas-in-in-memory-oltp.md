---
title: "Início Rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL | Microsoft Docs"
ms.custom: 
ms.date: 12/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82286b0d52ff37697ad9197b88c45935137a8dae
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>Pesquisa de áreas iniciais em OLTP in-memory
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
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
- O[banco de dados de exemplo para o OLTP In-Memory](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) oferece uma demonstração de escala maior.  
  
  
  
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
  
A palavra-chave do T-SQL NATIVE_COMPILATION, na instrução CREATE PROCEDURE, é como um proc. nativo é criado. As instruções T-SQL são compiladas para código de computador no primeiro uso do proc nativo toda vez que o banco de dados é alternado online. As instruções T-SQL não suportam mais a interpretação lenta de cada instrução.  
  
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
  
  
Os[Índices para as tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) são diferentes de algumas maneiras dos índices em tabelas em disco tradicionais.  
  
- Os[índices de hash](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) estão disponíveis apenas em tabelas com otimização de memória.  
  
  
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
  - A [excelente postagem no blog escrita por Gail Shaw](http://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/), em janeiro de 2016.  
  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>Guia de documentação das tabelas com otimização de memória  
  
  
Aqui estão os links para outros artigos que abordam as considerações especiais para tabelas com otimização de memória:  
  
- [Migrando para o OLTP in-memory](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
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
  
  
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>Links relacionados  
  
- Artigo inicial: OLTP in-memory [(otimização na memória)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
Aqui estão os artigos que oferecem o código para demonstrar os ganhos de desempenho que você pode obter usando OLTP in-memory:  
  
- [Demonstração: aprimoramento do desempenho do OLTP in-memory](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) oferece uma demonstração em pequena escala dos maiores ganhos potenciais de desempenho.  
- O[banco de dados de exemplo para o OLTP In-Memory](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) oferece uma demonstração de escala maior.  
  
  
  
\<!--  
  
e1328615-6b59-4473-8a8d-4f360f73187d , dn817827.aspx ,  “Introdução ao Columnstore para análise operacional em tempo real”  
  
f98af4a5-4523-43b1-be8d-1b03c3217839 , gg492088.aspx , “Guias de índices Columnstore”  
  
14dddf81-b502-49dc-a6b6-d18b1ae32d2b , dn133165.aspx , “Tabelas com otimização de memória”  
  
d5ed432c-10c5-4e4f-883c-ef4d1fa32366 , dn133184.aspx , “Procedimentos armazenados compilados nativamente”  
  
14106cc9-816b-493a-bcb9-fe66a1cd4630 , dn639109.aspx , “O grupo de arquivos com otimização de memória”  
  
f222b1d5-d2fa-4269-8294-4575a0e78636 , dn465873.aspx , “Associar um banco de dados com tabelas com otimização de memória a um pool de recursos”  
  
86805eeb-6972-45d8-8369-16ededc535c7 , dn511012.aspx , “Índices em tabelas com otimização de memória”  
  
16ef63a4-367a-46ac-917d-9eebc81ab29b , dn133166.aspx , “Diretrizes para usar índices em tabelas com otimização de memória”  
  
e3f8009c-319d-4d7b-8993-828e55ccde11 , dn246937.aspx , “Construções do Transact-SQL sem suporte no OLTP in-memory”  
  
2cd07d26-a1f1-4034-8d6f-f196eed1b763 , dn133169.aspx , “Transações em tabelas com otimização de memória”  
OBSERVAÇÃO: CONSULTE mt668425.aspx “Comportamentos e diretrizes para transações tabelas com otimização de memória”, que serão substituídos em breve.  
f2a35c37-4449-49ee-8bba-928028f1de66 , dn169141.aspx , “Diretrizes para lógica de repetição das transações em tabelas com otimização de memória”  
  
7a458b9c-3423-4e24-823d-99573544c877 , dn465869.aspx , “Monitorar e solucionar problemas de uso de memória”  
  
5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8 , dn282389.aspx , “Estimar requisitos de memória para tabelas com otimização de memória”  
  
b0a248a4-4488-4cc8-89fc-46906a8c24a1 , dn205318.aspx , “Tamanho da tabela e da linha em tabelas com otimização de memória”  
  
162d1392-39d2-4436-a4d9-ee5c47864c5a , dn296452.aspx , “Particionamento no nível do aplicativo”  
  
3f867763-a8e6-413a-b015-20e9672cc4d1 , dn133171.aspx , “Padrão de aplicativo para particionamento de tabelas com otimização de memória”  
  
86805eeb-6972-45d8-8369-16ededc535c7 , dn511012.aspx , “Índices em tabelas com otimização de memória”  
  
d82f21fa-6be1-4723-a72e-f2526fafd1b6 , dn465872.aspx , “Gerenciando memória para OLTP com otimização de memória”  
  
622aabe6-95c7-42cc-8768-ac2e679c5089 , dn133174.aspx , “Criando e gerenciando armazenamento para objetos com otimização de memória”  
  
bd102e95-53e2-4da6-9b8b-0e4f02d286d3 , dn535766.aspx , “Variáveis de tabela com otimização de memória”; “variável de tabela de uma tabela com otimização de memória”  
OBSOLETE. Consulte 38512a22-7e63-436f-9c13-dde7cf5c2202 , mt718711.aspx , “Tabela temporária e variável de tabela mais rápidas usando a otimização de memória”  
  
  
f0d5dd10-73fd-4e05-9177-07f56552bdf7 , ms191320.aspx , “Criar funções definidas pelo usuário (Mecanismo de Banco de Dados)”; “funções com valor de tabela”  
  
d2546e40-fdfc-414b-8196-76ed1f124bf5 , dn935012.aspx , “Funções escalares definidas pelo usuário para OLTP in-memory”; “funções escalares definidas pelo usuário”  
  
405cdac5-a0d4-47a4-9180-82876b773b82 , dn247639.aspx , “Migrando para OLTP in-memory”  
  
3f083347-0fbb-4b19-a6fb-1818d545e281 , dn624160.aspx , “Backup, restauração e recuperação de tabelas com otimização de memória”  
  
690b70b7-5be1-4014-af97-54e531997839 , dn269114.aspx , “Alterando tabelas com otimização de memória”  
  
  
b1cc7c30-1747-4c21-88ac-e95a5e58baac , dn133080.aspx , “Propriedades novas e atualizadas, exibições do sistema, procedimentos armazenados, tipos de espera e DMVs para OLTP in-memory”  
. . . . .  
TAMBÉM: “Suporte ao Transact-SQL para OLTP in-memory”  
  
  
c1ef96f1-290d-4952-8369-2f49f27afee2 , dn205133.aspx , “Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory”  
  
181989c2-9636-415a-bd1d-d304fc920b8a , dn284308.aspx , “Orientador de otimização de memória”  
  
55548cb2-77a8-4953-8b5a-f2778a4f13cf , dn452282.aspx , “Monitorando o desempenho de procedimentos armazenados compilados nativamente”  
  
d3898a47-2985-4a08-bc70-fd8331a01b7b , dn358355.aspx , “Orientador de compilação nativa”  
  
f43faad4-2182-4b43-a76a-0e3b405816d1 , dn296678.aspx , “Problemas de migração de procedimentos armazenados compilados nativamente”  
  
e1d03d74-2572-4a55-afd6-7edf0bc28bdb , dn133186.aspx , “OLTP in-memory (otimização na memória)”  
  
c6def45d-d2d4-4d24-8068-fab4cd94d8cc , dn530757.aspx , “Demonstração: aprimoramento do desempenho do OLTP in-memory”  
  
405cdac5-a0d4-47a4-9180-82876b773b82 , dn247639.aspx , “Migrando para OLTP in-memory”  
  
f76fbd84-df59-4404-806b-8ecb4497c9cc , bb522682.aspx , “Opções de ALTER DATABASE SET (Transact-SQL)”  
  
e6b34010-cf62-4f65-bbdf-117f291cde7b , dn452286.aspx , “Criando procedimentos armazenados compilados nativamente”  
  
df347f9b-b950-4e3a-85f4-b9f21735eae3 , mt465764.aspx , “Banco de dados de exemplo para OLTP in-memory”  
  
38512a22-7e63-436f-9c13-dde7cf5c2202 , mt718711.aspx , “Tabela temporária e variável de tabela mais rápidas usando a otimização de memória”  
  
38512a22-7e63-436f-9c13-dde7cf5c2202 , mt718711.aspx , “Tabela temporária e variável de tabela mais rápidas usando a otimização de memória”  
  
  
  
  
H1 # Início Rápido 1: tecnologias na memória para cargas de trabalho transacionais mais rápidas  
{1c25a164-547d-43c4-8484-6b5ee3cbaf3a} em maiúsculas  
mt718711.aspx no MSDN  
  
GeneMi , 2016-05-07  00:07am  
-->  
  
  
  


