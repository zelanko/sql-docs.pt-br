---
title: "Novidades no mecanismo de banco de dados – SQL Server 2017 | Microsoft Docs"
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-engine
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3ab26cac71a11ed7e9d98401b01930f27784433a
ms.sourcegitcommit: 16347f3f5ed110b5ce4cc47e6ac52b880eba9f5f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="whats-new-in-database-engine---sql-server-2017"></a>Novidades no mecanismo de banco de dados – SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Este tópico descreve as melhorias feitas no [!INCLUDE[ssdenoversion-md](../includes/ssdenoversion-md.md)] para o [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]. Clique nos links para obter mais informações sobre cada item.

> [!NOTE]  
> O SQL Server 2017 também inclui os recursos adicionados aos service packs do SQL Server 2016. Para esses itens, consulte [Novidades do SQL Server 2016 (Mecanismo de Banco de Dados)](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).

**Aprimoramentos**  

- O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. Um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios sysadmin. A partir do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A `clr strict security` está habilitada por padrão e trata assemblies `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. A Microsoft recomenda que todos os assemblies sejam assinados por um certificado ou uma chave assimétrica com um logon correspondente que recebeu a permissão `UNSAFE ASSEMBLY` no banco de dados mestre. Os assemblies CLR podem ser adicionados a uma lista de permissões, como uma solução alternativa para o recurso `clr strict security`. [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) e [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) são adicionados para oferecer suporte à lista de permissões de assemblies confiáveis. Para obter mais informações, consulte [Segurança estrita do CLR](configure-windows/clr-strict-security.md).  
- Uma nova DMF, [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), foi introduzida, para expor atributos no nível de resumo e informações sobre arquivos de log de transações; útil para monitorar a integridade do log de transações.  
- A recompilação de índice online retomável. A recompilação de índice online retomável permite retomar uma operação de rebuild de índice online do ponto em que foi interrompida após uma falha (como um failover para uma réplica ou espaço em disco insuficiente). Também é possível pausar e retomar uma operação de recompilação de índice online posteriormente. Por exemplo, talvez seja necessário liberar temporariamente os recursos do sistema para executar uma tarefa de alta prioridade ou concluir a recompilação de índice em outra janela de manutenção, caso as janelas de manutenção disponíveis sejam muito curtas para uma tabela grande. Por fim, a recompilação de índice online retomável não exige espaço de log significativo, o que permite executar o truncamento de log durante a execução da operação de recompilação retomável. Veja [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) e [Diretrizes para operações de índice online](../relational-databases/indexes/guidelines-for-online-index-operations.md).
- **Opção IDENTITY_CACHE para ALTER DATABASE SCOPED CONFIGURATION**. Uma nova opção IDENTITY_CACHE foi adicionada à instrução T-SQL `ALTER DATABASE SCOPED CONFIGURATION`. Quando essa opção é definida como `OFF`, ela permite que o Mecanismo de Banco de Dados evite lacunas nos valores das colunas de identidade, caso um servidor seja reiniciado inesperadamente ou faça failover para um servidor secundário. Veja [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).   
-  [!INCLUDE[ssnoversion](../includes/ssnoversion.md)] agora oferece recursos de banco de dados do gráfico para modelar dados orientados a relacionamento mais úteis. Isso inclui a nova sintaxe [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) para criar tabelas de nó e de borda e a palavra-chave [MATCH](../t-sql/queries/match-sql-graph.md) para consultas. Para obter mais informações, consulte [Processamento de gráficos com o SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md).   
- Uma nova geração de melhorias do processo de consulta que adaptará estratégias de otimização para as condições de tempo de execução da carga de trabalho do aplicativo. Para a primeira versão da família de recursos de **processamento de consulta adaptável**, temos três novas melhorias: **junções adaptáveis de modo de lote**, **comentários de concessão de memória de modo de lote** e **execução intercalada** para funções com valor de tabela de várias instruções.  Veja [Processamento de consultas adaptável em bancos de dados SQL](../relational-databases/performance/adaptive-query-processing.md).
- O ajuste automático é um recurso de banco de dados que fornece informações sobre possíveis problemas de desempenho de consultas, recomenda soluções e corrige automaticamente os problemas identificados. O ajuste automático do [!INCLUDE[ssnoversion](../includes/ssnoversion.md)] notifica você sempre que um possível problema de desempenho é detectado e permite aplicar as ações corretivas ou permite que o [!INCLUDE[ssde-md](../includes/ssde-md.md)] corrija automaticamente os problemas de desempenho. Para obter mais informações, consulte [Ajuste automático](../relational-databases/automatic-tuning/automatic-tuning.md).
- MELHORIA DE DESEMPENHO PARA BUILD DE ÍNDICE NÃO CLUSTERIZADO EM TABELAS COM OTIMIZAÇÃO DE MEMÓRIA. O desempenho da recompilação de índice bwtree (não clusterizado) em tabelas MEMORY_OPTIMIZED durante a recuperação de banco de dados foi otimizado de modo significativo. Essa melhoria reduz consideravelmente o tempo de recuperação de banco de dados quando os índices não clusterizados são usados.  
- [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) tem três colunas novas: socket_count, cores_per_socket e numa_node_count. Isso é útil quando você executa o servidor em uma VM, já que exceder o NUMA pode gerar hosts sobrecarregados que resultam em problemas de desempenho.
- Uma nova coluna modified_extent_page_count\, foi introduzida em [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) para controlar as alterações diferenciais em cada arquivo de banco de dados do banco de dados. A nova coluna modified_extent_page_count permite criar uma solução de backup inteligente, que faz o backup diferencial se o percentual de páginas alteradas no banco de dados está abaixo de um limite (digamos, 70-80%); caso contrário, ela faz o backup de banco de dados completo.
- SELECT INTO… Em FileGroup – [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) agora dá suporte ao carregamento de uma tabela em um grupo de arquivos que não é um grupo de arquivos padrão do usuário, usando o suporte à palavra-chave **ON** adicionado à sintaxe SELECT INTO do T-SQL.
- Melhorias de configuração do Tempdb – a configuração permite especificar um tamanho inicial do arquivo do tempdb de até **256 GB (262.144 MB)** por arquivo, com um aviso para os clientes informando se o tamanho do arquivo é definido como um valor maior que 1 GB e se a IFI não está habilitada. É importante entender a implicação de não habilitar a IFI (inicialização instantânea de arquivo), nos casos em que o tempo de configuração pode aumentar exponencialmente, dependendo do tamanho inicial do arquivo de dados do tempdb especificado. A IFI não é aplicável ao tamanho do log de transações e, portanto, a especificação de um valor maior do log de transações pode invariavelmente aumentar o tempo de configuração ao iniciar o tempdb durante a configuração, independentemente da configuração da IFI para a conta de serviço do SQL Server.
- Uma nova DMV [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) foi introduzida para controlar o uso do repositório de versão por banco de dados. Essa nova DMV é útil no monitoramento do uso do repositório de versão no tempdb, a fim de planejar de modo proativo o dimensionamento do tempdb de acordo com o requisito de uso do repositório de versão por banco de dados, sem cobrança de desempenho nem sobrecargas de executá-lo em servidores de produção.
- Uma nova DMF [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) foi introduzida para expor as informações de VLF semelhantes a DBCC LOGINFO, a fim de monitorar, emitir alertas e evitar possíveis problemas de log de transações causados pelo número de VLFs, tamanho de VLF ou problemas de redução de arquivo enfrentados pelos clientes.
- Melhor desempenho de backup para bancos de dados pequenos em servidores de alto nível – ao fazer backup de bancos de dados no SQL Server, o processo de backup exige iterações múltiplas do pool de buffers para esvaziar as E/Ss em andamento. Como resultado, o tempo de backup não é apenas a função do tamanho do banco de dados, mas também uma função do tamanho do pool de buffers ativo. No SQL Server 2017, o backup é otimizado para evitar iterações múltiplas do pool de buffers, resultando em ganhos substanciais no desempenho de backup de bancos de dados pequenos a médios. O ganho de desempenho é reduzido, à medida que o tamanho do banco de dados aumenta e à medida que as páginas a serem copiadas em backup e a E/S de backup levam mais tempo, comparado ao pool de buffers de iteração.  
- O Repositório de Consultas agora acompanha as informações resumidas das estatísticas de espera. O acompanhamento das categorias de estatísticas de espera por consulta no Repositório de Consultas possibilita o próximo nível da experiência de solução de problemas de desempenho, fornecendo ainda mais informações sobre o desempenho da carga de trabalho e seus afunilamentos, ao mesmo tempo que preserva as principais vantagens do Repositório de Consultas.  
- Tabelas temporais com controle de versão do sistema agora dão suporte a CASCADE DELETE e CASCADE UPDATE.  
- Melhorias indiretas de desempenho do ponto de verificação.
- Suporte a grupos de disponibilidade sem cluster adicionado.
- Configuração de Grupos de Disponibilidade de Confirmação de Réplica Mínima adicionada.
- Os Grupos de Disponibilidade agora podem trabalhar no Windows-Linux para permitir as migrações e testes entre sistemas operacionais.
- Suporte à Política de Retenção de Tabelas Temporais adicionado,
- Novo DMV SYS.DM_DB_STATS_HISTOGRAM
- Adição de suporte ao build e recompilação de índice columnstore não clusterizado online
- [sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) é adicionado para análise de estatísticas.
- O Database Tuning Advisor (DTA) lançado com o SQL Server Management Studio versão 16.4, ao analisar o SQL Server 2016 e posterior, tem opções adicionais.    
   - Desempenho aprimorado. Para saber mais, veja [Melhorias de desempenho usando as recomendações do Orientador de Otimização do Mecanismo de Banco de Dados (DTA)](../relational-databases/performance/performance-improvements-using-dta-recommendations.md).
   - A opção `-fc` para permitir recomendações de índices de columnstore. Para saber mais, veja [Utilitário DTA](../tools/dta/dta-utility.md) e [Recomendações de índice Columnstore no Orientador de Otimização do Mecanismo de Banco de Dados (DTA)](../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md).  
   - A opção `-iq` para permitir que o DTA analise uma carga de trabalho do Repositório de Consultas. Para saber mais, veja [Ajustar o Banco de Dados Usando Cargas de Trabalho do Repositório de Consulta](../relational-databases/performance/tuning-database-using-workload-from-query-store.md).  
- Para a funcionalidade na memória, estão disponíveis melhorias adicionais em tabelas com otimização de memória e em funções compiladas nativamente. Para obter exemplos de código que ilustram essas melhorias, consulte [Otimizar o processamento JSON com o OLTP in-memory](../relational-databases/json/optimize-json-processing-with-in-memory-oltp.md).
    - Suporte para colunas computadas em tabelas com otimização de memória, incluindo índices em colunas computadas.
    - Suporte completo para funções JSON em módulos compilados nativamente e em restrições de verificação.  
    - Operador`CROSS APPLY` em módulos compilados nativamente.   
- Foram adicionadas as novas funções de cadeia de caracteres [CONCAT_WS](../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../t-sql/functions/translate-transact-sql.md)e [TRIM](../t-sql/functions/trim-transact-sql.md) .   
- Agora há suporte para a cláusula `WITHIN GROUP` pela função [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) .
- Duas novas famílias de agrupamento em japonês (Japanese_Bushu_Kakusu_140 e Japanese_XJIS_140) foram adicionadas, além da opção de agrupamento Variation-selector-sensitive (_VSS) para uso nesses novos agrupamentos em japonês. Além disso, todos os novos agrupamentos dão suporte automático a caracteres suplementares sem a necessidade de especificar a opção _SC. Para obter mais detalhes, consulte [Suporte a Agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md)   
- As novas opções de acesso em massa [[BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET(BULK...)](../t-sql/functions/openrowset-transact-sql.md)] permitem acessar os dados diretamente em um arquivo especificado como o formato CSV e em arquivos armazenados no armazenamento de Blobs do Azure por meio da nova opção `BLOB_STORAGE` de [EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).
- **COMPATIBILITY_LEVEL** 140 do banco de dados foi adicionado.   Os clientes executando neste nível obterão os últimos recursos de linguagem e comportamentos de otimizador de consulta. Isso inclui alterações em cada versão de pré-lançamento que a Microsoft lançar.
- Melhorias na forma como os limites de atualização de estatísticas incrementais são computados (necessário modo de compatibilidade 140).
- O[sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) foi adicionado.
- Fizemos várias melhorias de desempenho e linguagem em objetos com Otimização de Memória:
    - Agora há suporte para `sp_spaceused` em tabelas com otimização de memória.
    - Agora há suporte para `sp_rename` em tabelas com otimização de memória e em módulos do T-SQL compilados nativamente.
    - Agora há suporte para expressões `CASE` em módulos do T-SQL compilados nativamente.
    - A limitação de 8 índices em tabelas com otimização de memória foi eliminada.
    - Agora há suporte para `TOP (N) WITH TIES` em módulos do T-SQL compilados nativamente.
    - Em geral, a execução de `ALTER TABLE` em tabelas com otimização de memória agora é substancialmente mais rápida.
    - A restauração do log de transações de tabelas com otimização de memória agora é feita em paralelo. Isso reforça tempos de recuperação mais rápidos e aumenta consideravelmente a taxa de transferência sustentada da configuração de grupos de disponibilidade AlwaysOn.
    - Agora, arquivos de grupo de arquivos com otimização de memória podem ser armazenados no Armazenamento do Azure. Agora, Backup/Restauração de arquivos com otimização de memória no Armazenamento do Azure também está disponível.
- Índices Columnstore clusterizados agora oferecem suporte a colunas LOB (nvarchar(max), varchar(max), varbinary(max)).
- A função de agregação [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) foi adicionada.  
- Novas permissões: `DATABASE SCOPED CREDENTIAL` agora é uma classe de protegível, suporte `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP`e `VIEW DEFINITION` permissões. `ADMINISTER DATABASE BULK OPERATIONS`, que é restrito ao Banco de Dados SQL, agora está visível em `sys.fn_builtin_permissions`.   
- A DMV [sys.dm_os_host_info](../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) foi adicionada para fornecer informações de sistema operacional para Windows e Linux.   
- As funções de banco de dados são criadas com R Services para gerenciar permissões associadas aos pacotes. Para obter mais informações, consulte [Gerenciamento de pacotes de R para o SQL Server](../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).

