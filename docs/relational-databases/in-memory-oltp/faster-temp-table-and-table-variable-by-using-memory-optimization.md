---
title: "Tabela temporária e variável de tabela mais rápidas usando a otimização de memória | Microsoft Docs"
ms.custom: 
ms.date: 10/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e2cc5b0632f57849d027b1e0c57eac8473721f49
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="faster-temp-table-and-table-variable-by-using-memory-optimization"></a>Tabela temporária e variável de tabela mais rápidas usando a otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
Se você usar tabelas temporárias, tabelas variáveis ou parâmetros com valor de tabela, considere convertê-las para aproveitar as tabelas com otimização de memória e variáveis de tabela para melhorar o desempenho. As alterações de código normalmente são mínimas.  
  
Este artigo descreve:  
  
- Cenários favorecem a conversão para in-memory.  
- Etapas técnicas para implementar as conversões para in-memory.  
- Pré-requisitos da conversão para in-memory.  
- Um exemplo de código que destaca os benefícios de desempenho de otimização de memória
  
  
## <a name="a-basics-of-memory-optimized-table-variables"></a>A. Noções básicas de variáveis de tabelas com otimização de memória  
  
Uma variável de tabela com otimização de memória fornece excelente eficiência usando o mesmo algoritmo com otimização de memória e estruturas de dados que são usadas por tabelas com otimização de memória. A eficiência é maximizada quando a variável de tabela é acessada de dentro de um módulo compilado nativamente.  
  
  
Uma tabela com otimização de memória variável:  
  
- É armazenado somente na memória e não tem nenhum componente no disco.  
- Não envolve nenhuma atividade de E/S.  
- Não envolve nenhuma utilização ou contenção de tempdb.  
- Pode ser passado para um procedimento armazenado como um parâmetro com valor de tabela (TVP).  
- Deve ter pelo menos um índice, hash ou não clusterizado.  
  - Para um índice de hash, o bucket idealmente deve ser de 1 a 2 vezes o número de chaves de índice exclusivo esperado, porém normalmente não há problema em superestimar a contagem de bucket (até 10 vezes). Para obter detalhes, consulte [Índices de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  

  
  
#### <a name="object-types"></a>Tipos de objeto  
  
OLTP in-memory fornece os seguintes objetos que podem ser usados para tabelas temp com otimização de memória e variáveis de tabela:  
  
- Tabelas com otimização de memória  
  - Durability = SCHEMA_ONLY  
- Variáveis de tabela com otimização de memória  
  - Deve ser declarado em duas etapas (em vez de embutidos):  
    - `CREATE TYPE my_type AS TABLE ...;` , então  
    - `DECLARE @mytablevariable my_type;`.  
  
  
## <a name="b-scenario-replace-global-tempdb-x23x23table"></a>B. Cenário: substituir tabela tempdb global &#x23;&#x23;  
  
Substituir uma tabela temporária global por uma tabela com otimização memória SCHEMA_ONLY é bastante simples. A maior alteração é criar a tabela no momento da implantação, não em tempo de execução. A criação de tabelas com otimização de memória demora mais do que a criação de tabelas tradicionais, devido a otimizações de tempo de compilação. Criar e descartar as tabelas com otimização de memória como parte da carga de trabalho online afetaria o desempenho da carga de trabalho, bem como o desempenho de restauração em secundários do AlwaysOn e recuperação de banco de dados.

Suponha que você tenha a seguinte tabela temporária global.  
  
  
  
  
    CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
Considere substituir a tabela temporária global pela seguinte tabela com otimização de memória que tem DURABILITY = SCHEMA_ONLY.  
  
  
  
  
    CREATE TABLE dbo.soGlobalB  
    (  
        Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
        Column2   NVARCHAR(4000)  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY        = SCHEMA_ONLY);  
  
  
  
  
#### <a name="b1-steps"></a>Etapas B.1  
  
A conversão de temporário global para SCHEMA_ONLY é o seguinte:  
  
  
1. Crie a tabela **dbo.soGlobalB** uma vez, como faria com qualquer tabela no disco tradicional.  
2. No Transact-SQL, remova a criação da tabela **&#x23;&#x23;tempGlobalB**.  É importante criar a tabela com otimização de memória no momento da implantação, não em um tempo de execução, para evitar a sobrecarga de compilação que acompanha a criação da tabela.
3. No seu T-SQL, substitua todos os menções de **&#x23;&#x23;tempGlobalB** com **dbo.soGlobalB**.  
  
  
## <a name="c-scenario-replace-session-tempdb-x23table"></a>C. Cenário: substituir a tabela tempdb de sessão &#x23;  
  
As preparações para substituir uma tabela temporária de sessão envolvem mais T-SQL que para o cenário anterior da tabela temporária global. Felizmente o T-SQL extra não significa a necessidade de mais esforço para realizar a conversão.  

Assim como no cenário de tabela temporária global, a maior alteração é criar a tabela no momento da implantação, não no tempo de execução, para evitar a sobrecarga de compilação.
  
Suponha que você tem a seguinte tabela temporária de sessão.  
  
  
  
  
    CREATE TABLE #tempSessionC  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
Primeiro, crie a seguinte função de valor de tabela para filtrar em **@@spid**. A função poderá ser usada por todas as tabelas SCHEMA_ONLY convertidas de tabelas temporárias de sessão.  
  
  
  
  
    CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
        RETURNS TABLE  
        WITH SCHEMABINDING , NATIVE_COMPILATION  
    AS  
        RETURN  
            SELECT 1 AS fn_SpidFilter  
                WHERE @SpidFilter = @@spid;  
  
  
  
  
Em segundo lugar, crie a tabela SCHEMA_ONLY, bem como uma política de segurança na tabela.  
  
  
Observe que cada tabela com otimização de memória deve ter pelo menos um índice.  
  
- Para a tabela dbo.soSessionC, um HASH de índice pode ser melhor se for possível calcular o BUCKET_COUNT apropriado. Porém para este exemplo, simplificamos um índice NONCLUSTERED.  
  
  
  
  
    CREATE TABLE dbo.soSessionC  
    (  
        Column1     INT         NOT NULL,  
        Column2     NVARCHAR(4000)  NULL,  
  
        SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  
  
        INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
        --INDEX ix_SpidFilter HASH  
        --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
          
        CONSTRAINT CHK_soSessionC_SpidFilter  
            CHECK ( SpidFilter = @@spid ),  
    )  
        com  
            (MEMORY_OPTIMIZED = ON,  
             DURABILITY = SCHEMA_ONLY);  
    go  
  
  
    CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
        ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
        ON dbo.soSessionC  
        WITH (STATE = ON);  
    go  
  
  
  
  
Em terceiro lugar, seu código geral T-SQL:  
  
1. Altere todas as referências à tabela temporária em suas instruções Transact-SQL para a nova tabela com otimização de memória:
    - _Antiga:_ &#x23;tempSessionC  
    - _Nova:_ dbo.soSessionC  
2. Substitua as instruções `CREATE TABLE #tempSessionC` no seu código com `DELETE FROM dbo.soSessionC`, para garantir que uma sessão não seja exposta ao conteúdo da tabela inserido por uma sessão anterior com o mesmo session_id. É importante criar a tabela com otimização de memória no momento da implantação, não em um tempo de execução, para evitar a sobrecarga de compilação que acompanha a criação da tabela.
3. Remova as instruções `DROP TABLE #tempSessionC` do seu código. Opcionalmente, você pode inserir uma instrução `DELETE FROM dbo.soSessionC` caso o tamanho de memória seja um problema potencial
  
  
  
  
## <a name="d-scenario-table-variable-can-be-memoryoptimizedon"></a>D. Cenário: uma variável da tabela pode ser MEMORY_OPTIMIZED=ON  
  
  
Uma variável de tabela tradicional representa uma tabela no banco de dados tempdb. Para um desempenho muito mais rápido, você pode otimizar a memória da variável de tabela.  
  
Aqui está o T-SQL para uma variável de tabela tradicional. Seu escopo termina quando o lote ou a sessão termina.  
  
  
  
  
    DECLARE @tvTableD TABLE  
        ( Column1   INT   NOT NULL ,  
          Column2   CHAR(10) );  
  
  
  
  
#### <a name="d1-convert-inline-to-explicit"></a>D. 1 Conversão embutida para explícita  
  
A sintaxe anterior deve criar a variável de tabela *embutida*. A sintaxe embutida não dá suporte à otimização da memória. Por isso, vamos converter a sintaxe embutida na sintaxe explícita para o TYPE.  
  
*Escopo:* a definição TYPE criada pelo primeiro lote delimitada por go persiste mesmo depois que o servidor é desligado e reiniciado. Porém, após o primeiro delimitador go, a tabela declarada @tvTableC persiste somente até o próximo go ser atingido e o lote terminar.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
          
    SET NoCount ON;  
    DECLARE @tvTableD dbo.typeTableD  
    ;  
    INSERT INTO @tvTableD (Column1) values (1), (2)  
    ;  
    SELECT * from @tvTableD;  
    go  
  
  
  
  
#### <a name="d2-convert-explicit-on-disk-to-memory-optimized"></a>D.2 Conversão explícita em disco para otimização de memória  
  
Uma variável de tabela com otimização de memória não reside em tempdb. A otimização de memória resulta em um aumento de velocidade geralmente 10 vezes mais rápido ou ainda maior.  
  
A conversão para a otimização de memória é obtida em apenas uma etapa. Aprimore a criação de TYPO explícito para o seguinte, que adiciona:  
  
- Um índice. Novamente, cada tabela com otimização de memória deve ter pelo menos um índice.  
- MEMORY_OPTIMIZED = ON.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL   INDEX ix1,  
            Column2  CHAR(10)  
        )  
        com  
            (MEMORY_OPTIMIZED = ON);  
  
  
  
  
Concluído.  
  
  
## <a name="e-prerequisite-filegroup-for-sql-server"></a>E. FILEGROUP de pré-requisito for SQL Server  
  
No Microsoft SQL Server, para usar recursos de otimização de memória, o banco de dados deve ter um FILEGROUP declarado com **MEMORY_OPTIMIZED_DATA**.  
  
- O Banco de Dados SQL do Azure não exige a criação deste FILEGROUP.  
  
  
*Pré-requisito:* o seguinte código Transact-SQL para um FILEGROUP é um pré-requisito para os exemplos de código T-SQL longos nas próximas seções deste artigo.  
  
1. Você deve usar SSMS.exe ou outra ferramenta que pode enviar o T-SQL.  
2. Cole o código T-SQL do FILEGROUP de exemplo no SSMS.  
3. Edite o T-SQL para alterar seus nomes específicos e caminhos de diretório de sua preferência.  
  - Todos os diretórios no valor do FILEGROUP já devem existir, exceto o diretório final, que não deve existir anteriormente.  
4. Execute o T-SQL editado.  
  - Não é necessário executar o T-SQL do FILEGROUP mais de uma vez, mesmo se você ajustar repetidamente e executar novamente a comparação T-SQL de velocidade na próxima subseção.  
  
  
  
 
  
    ALTER DATABASE InMemTest2  
        ADD FILEGROUP FgMemOptim3  
            CONTAINS MEMORY_OPTIMIZED_DATA;  
    go  
    ALTER DATABASE InMemTest2  
        ADD FILE  
        (  
            NAME = N'FileMemOptim3a',  
            FILENAME = N'C:\DATA\FileMemOptim3a'  
                     --  C:\DATA\    já existentes.  
        )  
        TO FILEGROUP FgMemOptim3;  
    go  
  
  
O script a seguir cria o grupo de arquivos para você e define as configurações de banco de dados recomendadas: [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)
  
Para obter mais informações sobre `ALTER DATABASE ... ADD` para FILE e FILEGROUP, consulte:  
  
- [Opções de arquivo e grupos de arquivos ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
- [O grupo de arquivos com otimização de memória](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## <a name="f-quick-test-to-prove-speed-improvement"></a>F. Teste rápido para comprovar a melhoria de velocidade  
  
  
Esta seção fornece código Transact-SQL que você pode executar para testar e comparar o ganho de velocidade para INSERT-DELETE usando uma variável de tabela com otimização de memória. O código é composto de duas partes que são praticamente as mesmas, exceto na primeira metade em que o tipo de tabela tem otimização de memória.  
  
O teste de comparação dura cerca de 7 segundos. Para executar o exemplo:  
  
1. *Pré-requisito:* você já deve ter executado o FILEGROUP T-SQL da seção anterior.  
2. Execute o seguinte script T-SQL INSERT-DELETE.  
  - Observe a instrução “Go 5001”, que reenvia os tempos de T-SQL 5001. Você pode ajustar o número e executar novamente.  
  
Ao executar o script em um Banco de Dados SQL do Azure, execute de uma VM na mesma região.
  
  
    PRINT ' ';  
    PRINT '---- Next, memory-optimized, faster. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
    CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
         AS TABLE  
         (  
              Column1  INT NOT NULL INDEX ix1,  
              Column2  CHAR(10)  
         )  
         WITH  
              (MEMORY_OPTIMIZED = ON);  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _mem.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
  
    ---- End memory-optimized.  
    -------------------------------------------------  
    ---- Start traditional on-disk.  
  
    PRINT ' ';  
    PRINT '---- Next, tempdb based, slower. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
        AS TABLE  
        (  
            Column1  INT NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    ----  
  
    PRINT '---- Tests done. ----';  
  
    go  
  
    /*** Actual output, SQL Server 2016:  
  
    ---- Next, memory-optimized, faster. ----  
    2016-04-20 00:26:58.033  = Begin time, _mem.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:26:58.733  = End time, _mem.  
  
    ---- Next, tempdb based, slower. ----  
    2016-04-20 00:26:58.750  = Begin time, _tempdb.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:27:05.440  = End time, _tempdb.  
    ---- Tests done. ----  
    ***/  
  

  
  
  
## <a name="g-predict-active-memory-consumption"></a>G. Prever o consumo de memória ativa  
  
Você pode aprender a prever as necessidades de memória ativa de suas tabelas com otimização de memória com os seguintes recursos:  
  
- [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Tamanho da tabela e da linha em tabelas com otimização de memória: exemplo de cálculo](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
Para variáveis de tabela maiores, índices não clusterizados usam mais memória do que para *tabelas*com otimização de memória. Quanto maior a contagem de linhas e a chave de índice, mais a diferença aumenta.  
  
Se a variável de tabela com otimização de memória é acessada apenas com um valor de chave exato por acesso, um índice de hash pode ser uma escolha melhor do que um índice não clusterizado. No entanto, se você não puder estimar o BUCKET_COUNT apropriado, um índice NONCLUSTERED é uma boa segunda opção.  
  
## <a name="h-see-also"></a>H. Consulte também  
  
- [Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
- [Definindo a durabilidade dos objetos com otimização de memória](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
