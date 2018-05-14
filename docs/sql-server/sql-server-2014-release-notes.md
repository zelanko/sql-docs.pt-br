---
title: Notas de versão do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2018
ms.prod: sql
ms.prod_service: sql
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: f9a8d57f209e5c8c813fd08c8faff6ce5504c97b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]
Este artigo descreve problemas conhecidos com as versões [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], incluindo service packs relacionados.

## <a name="sql-server-2014-service-pack-2-sp2"></a>SQL Server 2014 Service Pack 2 (SP2)

O SQL Server 2014 SP2 contém rollups de hotfixes lançados para a Atualização Cumulativa 7 do SQL Server 2014 SP1. Ele contém melhorias destinadas ao desempenho, escalabilidade e diagnóstico com base nos comentários dos clientes e da comunidade do SQL.

### <a name="performance-and-scalability-improvements-in-sp2"></a>Melhorias de desempenho e escalabilidade no SP2

|Recurso|Description|Para obter mais informações|
|---|---|---|
|Particionamento automático de Soft NUMA|É possível configurar automaticamente o Soft NUMA em sistemas que estejam relatando 8 ou mais CPUs por nó NUMA.|[Soft-NUMA (SQL Server)](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)|
|Buffer Pool Extension|Permite que o pool de buffers do SQL Server seja dimensionado para mais de 8 TB.|[Extensão do pool de buffers](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension)|
|Dimensionamento do objeto de Memória Dinâmica| Particionar dinamicamente o objeto de memória com base no número de nós e núcleos. Essa melhoria elimina a necessidade do Sinalizador de Rastreamento 8048 após o SQL 2014 SP2.|[Dimensionamento do objeto de Memória Dinâmica](https://blogs.msdn.microsoft.com/sql_server_team/dynamic-memory-object-scaling/)|
|Dica MAXDOP para comandos DBCC CHECK*|Essa melhoria é útil para executar DBCC CHECKDB com uma configuração de MAXDOP diferente do valor sp_configure.|[Dicas (Transact-SQL) – Consulta](https://docs.microsoft.com/sql/t-sql/queries/hints-transact-sql-query)|
|Melhoria do spinlock do SOS_RWLock|Remove a necessidade de spinlock para SOS_RWLock e usa técnicas sem bloqueio semelhantes ao OLTP in-memory. |[SOS_RWLock Redesign](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)|
|Implementação nativa espacial|Melhoria significativa no desempenho de consulta espacial.|[Melhorias de desempenho especial nos SQL Server 2012 e 2014](https://support.microsoft.com/help/3107399/spatial-performance-improvements-in-sql-server-2012-and-2014)

### <a name="supportability-and-diagnostics-improvements-in-sp2"></a>Melhorias de diagnóstico e da capacidade de suporte no SP2

|Recurso|Description|Para obter mais informações|
|---|---|---|
|Registro em log do tempo limite de AlwaysON|Foi adicionada uma nova funcionalidade de registro em log para mensagens de Tempo limite de concessão para que a hora atual e os tempos de renovação esperados sejam registrados. |[Melhoria no diagnóstico de tempo limite de concessão do grupo de disponibilidade AlwaysOn](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)
|Contadores de desempenho e XEvents AlwaysON|Os novos contadores de desempenho e XEvents AlwaysON para melhorar o diagnóstico ao solucionar problemas de latência com AlwaysON. |[KB 3107172](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve) e [KB 3107400](https://support.microsoft.com/help/3107400/improved-tempdb-spill-diagnostics-in-showplan-xml-schema-in-sql-server)
|Limpeza do controle de alterações|Um novo sp_flush_CT_internal_table_on_demand de procedimento armazenado limpa as tabelas internas de controle de alterações sob demanda.|[KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)
|Clonagem de banco de dados|Use o novo comando DBCC para solucionar os problemas de bancos de dados de produção existentes por meio da clonagem do esquema, metadados e estatísticas, mas sem os dados. Os bancos de dados clonados não se destinam ao uso em ambientes de produção.|[KB 3177838](https://support.microsoft.com/help/3177838/how-to-use-dbcc-clonedatabase-to-generate-a-schema-and-statistics-only)
|Adições de DMF|Novo sys.dm_db_incremental_stats_properties de DMF expõe informações por partição para estatísticas incrementais.|[KB 3170114](https://support.microsoft.com/help/3170114/update-to-add-dmf-sys-dm-db-incremental-stats-properties-in-sql-server)
|DMF para recuperar o buffer de entrada no SQL Server|Um novo DMF para recuperar o buffer de entrada para uma sessão/solicitação (sys.dm_exec_input_buffer) agora está disponível. Isso é funcionalmente equivalente ao DBCC INPUTBUFFER.|[sys.dm_exec_input_buffer](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql)
|Suporte de DROP DDL para replicação|Permite que uma tabela que está incluída como um artigo na publicação de replicação transacional seja descartada do banco de dados e da publicação.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)
|Privilégio IFI para a conta de serviço do SQL|Determine se a IFI (Inicialização Instantânea de Arquivo) está em vigor na inicialização do serviço SQL Server.|[Inicialização de arquivo de bancos de dados](https://docs.microsoft.com/sql/relational-databases/databases/database-instant-file-initialization)
|Concessões de memória – Tratando problemas|Você pode aproveitar as dicas de diagnóstico ao executar consultas limitando suas concessões de memória para evitar a contenção de memória.|[KB 3107401](https://support.microsoft.com/help/3107401/new-query-memory-grant-options-are-available-min-grant-percent-and-max)
|Criação de perfil por operador leve para execução de consulta |Otimiza a coleta de estatísticas de execução de consulta por operador como o número real de linhas.|[Escolha dos desenvolvedores: consultar o andamento – a qualquer momento, em qualquer lugar](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)
|Consultar diagnóstico de execução|A leitura de linhas reais agora é relatada nos planos de execução de consulta para ajudar a melhorar a solução de problemas de desempenho de consulta.|[KB 3107397](https://support.microsoft.com/help/3107397/improved-diagnostics-for-query-execution-plans-that-involve-residual-p)
|Consultar o diagnóstico de execução para despejo de tempdb|Aviso de hash e avisos de classificação agora tem colunas adicionais para rastrear as estatísticas de E/S físicas, a memória usada e as linhas afetadas. |[Melhorar o diagnóstico de despejo de temptdb](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve)
|Suporte de tempdb |Use uma nova mensagem de log de erros para o número de arquivos tempdb, e as alterações de arquivo de dados tempdb, na inicialização do servidor.|[KB 2963384](https://support.microsoft.com/help/2963384/fix-sql-server-crashes-when-the-log-file-of-tempdb-database-is-full-in)


Além disso, observe as seguintes correções:
- Agora a pilha de chamadas Xevent inclui nomes de módulo e deslocamento, em vez de endereços absolutos.
- Melhoria na correlação entre XE e DMV – Query_hash e query_plan_hash são usados para identificar uma consulta com exclusividade. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como o SQL Server não tem “bigint sem sinal”, a conversão nem sempre funciona. Essa melhoria introduz novas colunas de ação/filtro de XEvent equivalentes a query_hash e a query_plan_hash, exceto quando elas estão definidas como INT64. Essa correção ajuda a correlacionar consultas entre XE e DMVs.
- Suporte para UTF-8 em BULK INSERT e BCP – Suporte para exportação e importação de dados codificados no conjunto de caracteres UTF-8 agora está habilitado em BULK INSERT e BCP.

### <a name="download-pages-and-more-information-for-sp2"></a>Páginas de download e mais informações para o SP2

- [Baixar o Service Pack 2 para Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=53168)
- [O SQL Server 2014 Service Pack 2 já está disponível](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2012 SP2 Express](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164)
- [Construtor de Relatórios do SQL Server 2014 SP2](https://www.microsoft.com/download/details.aspx?id=53163)
- [Suplemento do Microsoft SQL Server 2014 SP2 Reporting Services para Microsoft SharePoint](https://www.microsoft.com/download/details.aspx?id=53162)
- [Estatísticas Semânticas de Idioma do SQL Server 2014 SP2](https://www.microsoft.com/download/details.aspx?id=53165)
- [Informações de Versão do SQL Server 2014 Service Pack 2](https://support.microsoft.com/help/3171021/sql-server-2014-service-pack-2-release-information)

## <a name="sql-server-2014-service-pack-1-sp1"></a>SQL Server 2014 Service Pack 1 (SP1)

O SQL Server 2014 SP1 contém correções fornecidas no SQL Server 2014 Atualização Cumulativa 1 até a Atualização Cumulativa 5, bem como um rollup de correções fornecidas anteriormente no SQL Server 2012 SP2.

> [!NOTE]
> Se a instância do SQL Server tem um catálogo SSISDB habilitado e você receber um erro de instalação ao atualizar para o SP1, siga as instruções descritas para esse problema em [Erro 912 ou 3417 ao instalar o SQL Server 2014 SP1](https://support.microsoft.com/help/3018269/error-912-or-3417-when-you-install-sql-server-2014-sp1-build-12-0-4050/).

### <a name="download-pages-and-more-information-for-sp1"></a>Páginas de download e mais informações para o SP1

- [Baixar o Service Pack 1 para Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=46694)
- [O SQL Server 2014 Service Pack 1 foi lançado – Atualizado](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2014-service-pack-1-has-released-updated/)
- [Microsoft SQL Server 2014 SP1 Express](https://www.microsoft.com/download/details.aspx?id=46697)
- [Microsoft SQL Server 2014 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=46696)


## <a name="before-you-install-sql-server-2014-rtm"></a>Antes de instalar o SQL Server 2014 RTM

### <a name="limitations-and-restrictions-in-sql-server-2014-rtm"></a>Limitações e restrições no SQL Server 2014 RTM

1.  A atualização do SQL Server 2014 CTP 1 para o SQL Server 2014 RTM NÃO é suportada.  
2.  A instalação do SQL Server 2014 CTP 1 em conjunto com o SQL Server 2014 RTM NÃO é suportada.  
3.  Os recursos de anexação ou restauração de um banco de dados do SQL Server 2014 CTP 1 ao SQL Server 2014 RTM não têm suporte.  

**Solução alternativa:** não há.

#### <a name="upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm"></a>Atualização do SQL Server 2014 CTP 2 para o SQL Server RTM
A atualização tem suporte total. Em especial, você pode:

1.  Anexar um banco de dados do SQL Server 2014 CTP 2 a uma instância do SQL Server 2014 RTM.    
2.  Restaurar um banco de dados removido do SQL Server 2014 CTP 2 para uma instância do SQL Server 2014 RTM.    
3.  Atualização in-loco do SQL Server 2014 RTM.
4.  Atualização sem interrupção do SQL Server 2014 RTM. É necessário alternar para o modo de failover manual antes de iniciar a atualização sem interrupção. Consulte [Fazer upgrade e atualização dos servidores de grupo de disponibilidade com tempo de inatividade e perda de dados mínimos](http://msdn.microsoft.com/library/dn178483.aspx) para obter detalhes.    
5.  Os dados coletados pelos conjuntos de coleta de desempenho da transação instalados no SQL Server 2014 CTP 2 não podem ser visualizados com o SQL Server Management Studio no SQL Server 2014 RTM, e vice-versa.
  
#### <a name="downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>Fazer downgrade do SQL Server 2014 RTM para o SQL Server 2014 CTP 2  
Não há suporte para essa ação.  
  
**Solução:** Não há solução para a desatualização. Recomendamos que você faça backup do banco de dados antes de atualizar para o SQL Server 2014 RTM.  
  
#### <a name="incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>Versão incorreta do StreamInsight Client na mídia/ISO/CAB do SQL Server 2014  
A versão incorreta do StreamInsight.msi e do StreamInsightClient.msi está localizada no seguinte caminho na mídia/ISO/CAB do SQL Server (StreamInsight\\\<Arquitetura\>\\\<ID de idioma\>).  
  
**Solução alternativa:** baixe e instale a versão correta da página de download do [SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
### <a name="ProdDoc"></a>Documentação do Produto RTM
  
O conteúdo do Construtor de Relatórios e do PowerPivit não está disponível em alguns idiomas. 

**Problema:** o conteúdo do Construtor de Relatórios não está disponível nos idiomas a seguir:  
  
-   Grego (el-GR)  
-   Norueguês (Bokmal) (nb-NO)  
-   Finlandês (fi-FI)  
-   Dinamarquês (da-DK)  
  
No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], esse conteúdo estava disponível em um arquivo CHM enviado com o produto e que estava disponível nesses idiomas. Os arquivos CHM não vêm mais com o produto e o conteúdo do Construtor de Relatórios só está disponível no MSDN. O MSDN não oferece suporte a esses idiomas. O Construtor de Relatórios também foi removido do TechNet e não está mais disponível nesses idiomas com suporte.  
  
**Solução alternativa:** não há.  
  
**Problema:** o conteúdo do Power Pivot não está disponível nos idiomas a seguir:
  
-   Grego (el-GR)  
-   Norueguês (Bokmal) (nb-NO)  
-   Finlandês (fi-FI)  
-   Dinamarquês (da-DK)  
-   Tcheco (cs-CZ)  
-   Húngaro (hu-HU)  
-   Holandês (Países Baixos) (nl-NL)  
-   Polonês (pl-PL)  
-   Sueco (sv-SE)  
-   Turco (tr-TR)  
-   Português (Portugal) (pt-PT)  
  
No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], este conteúdo estava disponível no TechNet e estava disponível nestes idiomas. Esse conteúdo foi removido do TechNet e não está mais disponível nesses idiomas com suporte.  
  
**Solução alternativa:** não há.  
  
### <a name="DBEngine"></a>Mecanismo de Banco de Dados (RTM)
  
#### <a name="changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>Alterações feitas à edição Standard no SQL Server 2014 RTM  
O padrão do SQL Server 2014 tem as seguintes alterações:  
  
-   O recurso de extensão do pool de buffers permite usar o tamanho máximo de até 4 vezes a memória configurada.    
-   A memória máxima foi aumentada de 64 GB para 128 GB.  
 
#### <a name="memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>O Orientador de Otimização de Memória sinaliza restrições padrão como incompatíveis  
**Problema:** O orientador de otimização de memória no SQL Server Management Studio sinaliza todas as restrições padrão como incompatíveis. Nem todas as restrições padrão têm suporte em uma tabela com otimização de memória; o orientador de otimização do não faz distinção entre tipos com e sem suporte de restrições padrão. As restrições padrão com suporte incluem todas as constantes, expressões e funções internas compatíveis com os procedimentos armazenados compilados de forma nativa. Para ver a lista de funções com suporte em procedimentos armazenados compilados de forma nativa, veja [Construções suportadas em procedimentos armazenados compilados de forma nativa](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx).  
  
**Solução alternativa:** se você quiser usar o orientador para identificar bloqueadores, ignore as restrições padrão correspondentes. Para usar o orientador de otimização de memória para migrar as tabelas que têm restrições padrão correspondentes, mas nenhum outro bloqueador, siga estas etapas:  
  
1.  Remova as restrições padrão da definição de tabela.    
2.  Use o orientador de otimização do gerar um script de migração na tabela.    
3.  Adicione as restrições padrão novamente no script de migração.    
4.  Execute o script de migração.  
  
#### <a name="informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>A mensagem informativa “acesso ao arquivo negado” é relatada incorretamente como um erro no log de erros do SQL Server 2014  
**Problema:** ao reiniciar um servidor que possui bancos de dados que contêm tabelas com otimização de memória, você pode ver o seguinte tipo de mensagens de erro no log de erros do SQL Server 2014:  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
Esta mensagem é apenas informativa, e nenhuma ação do usuário é necessária.  
  
**Solução alternativa:** não há. Essa é uma mensagem informativa.  
  
#### <a name="missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>Os detalhes de índice ausentes relatam incorretamente as colunas incluídas para a tabela com otimização de memória  
**Problema:** se o SQL Server 2014 detectar um índice ausente para uma consulta em uma tabela com otimização de memória, relatará um índice ausente em SHOWPLAN_XML, bem como nos DMVs do índice ausente, como sys.dm_db_missing_index_details. Em alguns casos, os detalhes de índice ausentes conterão as colunas incluídas. Uma vez que todas as colunas são incluídas implicitamente com todos os índices nas tabelas com otimização de memória, não é permitido especificar explicitamente as colunas incluídas com os índices otimizados por memória.  
  
**Solução:** não especifique a cláusula INCLUDE com os índices das tabelas com otimização de memória.  
  
#### <a name="missing-index-details-omit-missing-indexes-when-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>Os detalhes de índice ausentes omitem os índices ausentes quando um índice de hash existe, mas não é apropriado para a consulta  
**Problema:** se você tiver um índice de HASH nas colunas de uma tabela com otimização de memória referenciada em uma consulta, mas o índice não puder ser usado na consulta, SQL Server 2014 sem sempre relatará um índice ausente em SHOWPLAN_XML e no DMV sys.dm_db_missing_index_details.  
  
Em particular, se uma consulta contiver os predicados de igualdade que envolvem um subconjunto de colunas de chave de índice ou se contiver os predicados de desigualdade que envolvem as colunas de chave de índice, o índice de HASH não pode ser usado como está, e um índice diferente será necessário para executar a consulta de forma eficaz.  
  
**Solução:** Caso você esteja usando índices de hash, inspecione as consultas e os planos de consulta para determinar se as consultas podem se beneficiar das operações de busca de índice em um subconjunto de chave de índice, ou as operações de busca de índice em predicados de desigualdade. Se você precisar buscar em um subconjunto de chave de índice, use um índice não clusterizado, ou use um índice de HASH exatamente nas colunas em que você precisa buscar. Se você precisar buscar em um predicado de desigualdade, use um índice não clusterizado em vez de HASH.  
  
#### <a name="failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>Ocorrerá uma falha ao usar uma tabela com otimização de memória e uma variável de tabela com otimização de memória na mesma consulta, se a opção READ_COMMITTED_SNAPSHOT do banco de dados for definida como ON  
**Problema:** se a opção READ_COMMITTED_SNAPSHOT do banco de dados for definida como ON, e você acessar uma tabela com otimização de memória e uma variável de tabela com otimização de memória na mesma instrução fora do contexto de uma transação de usuário, você poderá encontrar essa mensagem de erro:  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**Solução:** utilize a dica de tabela WITH (SNAPSHOT) com a variável de tabela, ou defina a opção MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT do banco de dados para ON, usando a seguinte instrução:  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>Procedimento e estatísticas de execução de consulta para que os procedimentos armazenados compilados de forma nativa armazenem o tempo de trabalho em múltiplos de 1000  
**Problema:** depois de habilitar a coleção de procedimento ou coleção de estatísticas de execução de consulta para procedimentos armazenados compilados de forma nativa usando sp_xtp_control_proc_exec_stats ou sp_xtp_control_query_exec_stats, você verá o *_worker_time relatado em múltiplos de 1000, nos DMVs sys.dm_exec_procedure_stats e sys.dm_exec_query_stats. As execuções de consulta com um período de trabalho inferior a 500 microssegundos serão relatadas como tendo um worker_time de 0.  
  
**Solução alternativa:** não há. Não confie no worker_time relatado nos DMVs das estatísticas de execução para consultas de curta duração em procedimentos armazenados compilados de forma nativa.  
  
#### <a name="error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>Erro com SHOWPLAN_XML para os procedimentos armazenados compilados de forma nativa que contêm expressões longas  
**Problema:** se um procedimento armazenado compilado de forma nativa contiver uma expressão longa, obter o SHOWPLAN_XML para o procedimento usando a opção SET SHOWPLAN_XML ON do T-SQL ou usando a opção "Exibir plano de execução estimado" no Management Studio, poderá resultar no seguinte erro:  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**Solução:** Duas soluções sugeridas:  
  
1.  Adicione parênteses à expressão, semelhante ao seguinte exemplo:  
  
    Em vez de:  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    Gravação:  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  Crie um segundo procedimento com uma expressão ligeiramente simplificada, para as finalidades de plano de execução - a forma geral do plano deve ser a mesma. Por exemplo, em vez de:  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    Gravação:  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>Usar um parâmetro ou uma variável de cadeia de caracteres com DATEPART e funções relacionadas em um procedimento armazenado compilado de forma nativa resultará em um erro  
**Problema:** ao usar um procedimento armazenado compilado de forma nativa que usa o parâmetro ou variável de cadeia de caracteres com as funções internas DATEPART, DAY, MONTH e YEAR, uma mensagem de erro indica que o datetimeoffset do tipo de dados não é compatível com procedimentos armazenados compilados de forma nativa.  
  
**Solução:** Atribua o parâmetro ou variável de cadeia de caracteres a uma nova variável do tipo datetime2, e use essa variável na função DATEPART, DAY, MONTH ou YEAR. Por exemplo:  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>O Native Compilation Advisor sinaliza as cláusulas DELETE FROM incorretamente  
**Problema:** o Orientador de Compilação Nativa sinaliza as cláusulas DELETE FROM dentro de um procedimento armazenado incorretamente como incompatível.  
  
**Solução alternativa:** não há.  
  
#### <a name="register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>O registro com o SSMS adiciona metadados do DAC com IDs de instância incompatíveis  
**Problema:** ao registrar ou excluir um pacote de aplicativos da camada de dados (.dacpac) com o SQL Server Management Studio, as tabelas de sysdac* não são atualizadas corretamente para permitir que um usuário consulte o histórico do dacpac para o banco de dados.  O instance_id para o sysdac_history_internal e o sysdac_instances_internal não correspondem para permitir uma junção.  
  
**Solução alternativa:** esse problema é corrigido com a redistribuição do feature pack da [Estrutura do aplicativo da camada de dados](https://www.microsoft.com/download/details.aspx?id=42295).  Depois que a atualização for aplicada, todas as novas entradas de histórico usarão o valor listado para instance_id na tabela sysdac_instances_internal.  
  
Se você já tiver o problema com valores de instance_id incompatíveis, a única maneira de corrigir os valores incompatíveis é se conectar ao servidor como um usuário com privilégios para gravar no banco de dados MSDB e atualizar os valores de instance_id para correspondência.  Se há vários eventos de registro e cancelamento de registro do mesmo banco de dados, talvez seja necessário examinar a data/hora para ver quais registros correspondem ao valor atual de instance_id.  
  
1.  Conecte-se ao servidor no SQL Server Management Studio usando um logon que tenha permissões de atualização para o MSDB.    
2.  Abra uma nova consulta usando o banco de dados MSDB.    
3.  Execute esta consulta para ver todas as instâncias de dac ativas.  Localize a instância que você deseja corrigir e anote o instance_id:  
  
    `select * from` sysdac_instances_internal  
  
4.  Execute esta consulta para ver todas as entradas de histórico:  
  
    `select * from` sysdac_history_internal  
  
5.  Identifique as linhas que devem corresponder à instância que você está corrigindo. 
6.  Atualize o valor de sysdac_history_internal.instance_id para o valor que você observou na etapa 3 (na tabela sysdac_instances_internal):  
  
    `update` sysdac_history_internal `set` instance_id = '\<valor da etapa 3\>' `where` \<expressão que corresponde às linhas que deseja atualizar\>  
  
### <a name="SSRS"></a>Reporting Services (RTM)
  
#### <a name="the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>O servidor de relatório do Modo Nativo do SQL Server 2012 Reporting Services não pode ser executado lado a lado com componentes do SQL Server 2014 Reporting Services SharePoint  
**Problema:** o serviço do Windows do modo Nativo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] “SQL Server Reporting Services” (ReportingServicesService.exe) falha ao iniciar quando há componentes do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint instalados no mesmo servidor.  
  
**Solução alternativa:** Desinstalar os componentes do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint e reiniciar o serviço do Microsoft SQL Server 2012 Reporting Services do Windows.  
  
**Mais Informações:**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] O modo nativo não pode ser executado lado a lado em uma das seguintes condições:  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Suplemento para produtos do SharePoint    
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Serviço Compartilhado do SharePoint  
  
A instalação lado a lado impede que o Serviço do Windows no modo nativo do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inicie. Mensagens de erro semelhantes às mostradas aqui aparecerão no Log de Eventos do Windows:  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
Para obter mais informações, consulte [Dicas, truques e soluções de problemas do SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
#### <a name="required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>A ordem de atualização necessária para vários nós do SharePoint Farm para o SQL Server 2014 Reporting Services  
**Problema:** a renderização de relatório em uma farm de vários nós falha se as instâncias do Serviço Compartilhado do SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] forem atualizadas antes de todas as instâncias do suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para os produtos do SharePoint.  
  
**Solução:** em uma farm do SharePoint com vários nós:  
  
1.  Atualize primeiro todas as instâncias do suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para os produtos do SharePoint.    
2.  Em seguida, atualize todas as instâncias do serviço compartilhado do SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
Para obter mais informações, consulte [Dicas, truques e soluções de problemas do SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254)  
  
### <a name="AzureVM"></a>SQL Server 2014 RTM em máquinas virtuais do Microsoft Azure  
  
#### <a name="the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>O assistente para adicionar réplica do Azure retorna um erro ao configurar um ouvinte do grupo de disponibilidade no Microsoft Azure  
**Problema:** Se um grupo de disponibilidade tiver um ouvinte, o assistente para adicionar réplica do Azure retornará um erro ao tentar configurar o ouvinte no Windows Azure.  
  
Esse problema se deve ao fato dos ouvintes do grupo de disponibilidade exigirem a atribuição de um endereço IP em cada sub-rede que hospeda réplicas do grupo de disponibilidade, inclusive a sub-rede do Azure.  
  
**Solução alternativa:**  
  
1.  Na página do ouvinte, atribua um endereço IP estático livre na sub-rede do Azure que hospedará a réplica do grupo de disponibilidade para o ouvinte do grupo de disponibilidade.  
  
    Essa solução alternativa permitirá que o Assistente conclua a adição da réplica no Microsoft Azure.  
  
2.  Ao concluir o assistente, você precisará concluir a configuração de ouvinte no Windows Azure conforme descrito em [Configuração de ouvinte para grupos de disponibilidade AlwaysOn no Windows Azure](http://msdn.microsoft.com/library/dn376546.aspx)  
  
### <a name="SSAS"></a>Analysis Services (RTM)
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>É necessário baixar, instalar e registrar o MSOLAP.5 para uma nova farm do SharePoint 2010 configurado com o SQL Server 2014  
**Problema:**  
  
-   Para uma farm do SharePoint 2010, é necessário baixar, instalar e registrar o MSOLAP.5 para uma nova farm do SharePoint 2013 configurado com o SQL Server 2014 configurada com uma implantação do SQL Server 2014 RTM, as pastas de trabalho do PowerPivot não podem se conectar aos modelos de dados porque o provedor referenciado na cadeia de conexão não está instalado.  
  
**Solução alternativa:**  
  
1.  Baixe o provedor MSOLAP.5 do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Instale o provedor nos servidores de aplicativos que executam os Serviços do Excel. Para obter mais informações, consulte a seção "Microsoft Analysis Services OLE DB Provider para Microsoft SQL Server 2012 SP1" [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registre o MSOLAP.5 como um provedor confiável em Serviços do Excel do SharePoint. Para obter mais informações, consulte [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Mais Informações:**  
  
-   O[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] inclui MSOLAP.6. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] usam MSOLAP.5. Se o MSOLAP.5 não estiver instalado no computador que executa os Serviços do Excel, os Serviços do Excel não poderão carregar os modelos de dados.  
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>É necessário baixar, instalar e registrar o MSOLAP.5 para uma nova farm do SharePoint 2013 configurado com o SQL Server 2014  
**Problema:**  
  
-   Para um farm do SharePoint 2013 configurada com uma implantação do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] , as pastas de trabalho do Excel que referenciam o provedor MSOLAP.5 não podem se conectar aos modelos de dados da tabela porque o provedor referenciado na cadeia de conexão não está instalado.  
  
**Solução alternativa:**  
  
1.  Baixe o provedor MSOLAP.5 do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Instale o provedor nos servidores de aplicativos que executam os Serviços do Excel. Para obter mais informações, consulte a seção "Microsoft Analysis Services OLE DB Provider para Microsoft SQL Server 2012 SP1" [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registre o MSOLAP.5 como um provedor confiável em Serviços do Excel do SharePoint. Para obter mais informações, consulte [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Mais Informações:**  
  
-   O[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] inclui MSOLAP.6. mas as pastas de trabalho PowerPivot do SQL Server 2014 usam MSOLAP.5. Se o MSOLAP.5 não estiver instalado no computador que executa os Serviços do Excel, os Serviços do Excel não poderão carregar os modelos de dados.  
  
#### <a name="corrupt-data-refresh-schedules-rtm"></a>Agenda de atualização de dados corrompidos (RTM)
**Problema:**  
  
-   Você atualiza uma agenda de atualização e a agenda torna-se corrompida e inutilizável.  
  
**Solução alternativa:**  
  
1.  No Microsoft Excel, desmarque as propriedades avançadas personalizadas. Consulte a seção “Solução alternativa” do seguinte artigo da base de dados de conhecimento [KB 2927748](http://support.microsoft.com/kb/2927748).  
  
**Mais Informações:**  
  
-    Quando você atualiza uma agenda de atualização de dados para uma pasta de trabalho, se o comprimento serializado da agenda de atualização for menor que a agenda original, o tamanho do buffer não será atualizado corretamente e as novas informações de agenda serão mescladas com as antigas informações de agenda resultando em uma agenda corrompida.  
  
### <a name="DQS"></a>Data Quality Services (RTM)
  
#### <a name="no-cross-version-support-for-data-quality-services-in-master-data-services"></a>Não há suporte entre versões para o Data Quality Services no Master Data Services  
**Problema:** Os cenários a seguir não têm suporte:  
  
-   Master Data Services 2014 hospedado em um banco de dados do Mecanismo de Banco de Dados do SQL Server no SQL Server 2012 com o Data Quality Services 2012 instalado.  
  
-   Master Data Services 2012 hospedado em um banco de dados do Mecanismo de Banco de Dados do SQL Server no SQL Server 2014 com o Data Quality Services 2014 instalado.  
  
**Solução:** Use a mesma versão do Master Data Services que o banco de dados do mecanismo de banco de dados e o Data Quality Services.  
  
### <a name="UA"></a>Problemas do supervisor de atualização (RTM)
  
#### <a name="sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>O Supervisor de Atualização do SQL Server 2014 relata problemas de atualização irrelevantes do SQL Server Reporting Services  
**Problema:** o supervisor de atualização do SQL Server (SSUA) fornecido com o SQL Server 2014 relata vários erros ao analisar o servidor do SQL Server Reporting Services.  
  
**Solução:** Esse problema é corrigido no supervisor de atualização do SQL Server fornecido no [SQL Server 2014 Feature Pack para SSUA](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
#### <a name="sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>O Supervisor de Atualização do SQL Server 2014 relata um erro ao analisar o servidor do SQL Server Integration Services  
**Problema:** o Supervisor de Atualização do SQL Server (SSUA) fornecido com a mídia SQL Server 2014 relata um erro ao analisar o servidor do SQL Server Integration Services.  O erro que é exibido para o usuário é:  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**Solução:** Esse problema é corrigido no supervisor de atualização do SQL Server fornecido no [SQL Server 2014 Feature Pack para SSUA](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]