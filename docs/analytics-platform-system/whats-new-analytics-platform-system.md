---
title: O que há de novo no Analytics Platform System-um data warehouse de expansão
description: Veja o que há de novo no Microsoft Analytics Platform System, um dispositivo local de expansão que hospeda o MPP SQL Server data warehouse paralela.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9d0ff3861912270091b6a63cbd3fd7b2e8e0e481
ms.sourcegitcommit: 853c2c2768caaa368dce72b4a5e6c465cc6346cf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227108"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>O que há de novo no Analytics Platform System, um data warehouse MPP de expansão
Veja o que há de novo nas atualizações de dispositivo mais recentes para Microsoft Analytics Platform System (APS). O APS é um dispositivo local de expansão que hospeda o MPP SQL Server paralelo data warehouse. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU 7.5
Data de lançamento – setembro de 2019

### <a name="alter-external-data-source"></a>Alterar fonte de dados externa
Os clientes poderão alterar a definição da fonte de dados externa com a atualização do CU 7.5. Os clientes com o nó de nome do Hadoop alta disponibilidade agora podem alterar a fonte de dados para alterar os argumentos quando ocorre um failover. Para APS, somente o local, RESOURCE_MANAGER_LOCATION e CREDENTIAL podem ser alterados. Consulte [Alterar fonte de dados externa](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017) para obter mais informações.

### <a name="cdh-515-and-516-support-with-polybase"></a>Suporte a CDH 5,15 e 5,16 com polybase
O polybase no APS com a atualização do CU 7.5 Agora dá suporte às versões CDH 5,15 e 5,16 da distribuição do Hadoop do Cloudera. Use a opção 6 para as versões do CDH 5. x. 

### <a name="try_convert-and-try_cast-support"></a>Suporte a Try_Convert e Try_Cast
O CU 7.5 APS agora dá suporte às funções TSQL [TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017) e [TRY_CONVERT](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) . Essas duas funções retornarão um valor convertido para o tipo de dados especificado se a conversão for concluída com sucesso; caso contrário, retornará NULL.

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
Data de lançamento – maio de 2019

### <a name="loading-large-rows-with-dwloader"></a>Carregando linhas grandes com dwloader
A partir do APS CU 7.4, os clientes poderão usar um novo dwloader para carregar linhas em tabelas com mais de 32 KB (32.768 bytes). O novo dwloader dá suporte à opção-l que usa um valor inteiro entre 32768 e 33554432 (em bytes) para carregar linhas maiores que 32 KB. Use essa opção apenas ao carregar linhas grandes (maiores que 32 KB), pois essa opção alocará mais memória no cliente e no servidor e poderá retardar as cargas. Você pode baixar o novo dwloader do [site de download](https://www.microsoft.com/download/details.aspx?id=57472).  

### <a name="hdp-30-and-31-support-with-polybase"></a>Suporte a HDP 3,0 e 3,1 com polybase
O polybase no APS agora dá suporte a HDP 3,0 e 3,1 com essa atualização. Use a opção 7 para as versões do HDP 3. x. Para obter mais informações, consulte a página [conectividade do polybase](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) .

### <a name="utf16-file-support-with-polybase"></a>Suporte a arquivo UTF16 com polybase
O polybase agora dá suporte à leitura de arquivos de texto delimitados que estão na codificação UTF16 (LE). Consulte [criar formato de arquivo externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) para obter detalhes de instalação. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
Data de lançamento – dezembro de 2018

### <a name="common-subexpression-elimination"></a>Eliminação de subexpressão comum
O APS CU 7.3 melhora o desempenho da consulta com a eliminação de subexpressão comum no otimizador de consulta do SQL. A melhoria melhora as consultas de duas maneiras. O primeiro benefício é a capacidade de identificar e eliminar essas expressões, ajudando a reduzir o tempo de compilação do SQL. O segundo e mais importante benefício é que as operações de movimentação de dados para essas subexpressões redundantes são eliminadas, portanto, o tempo de execução das consultas se torna mais rápido. A explicação detalhada desse recurso pode ser encontrada [aqui](common-sub-expression-elimination.md).

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Conector do APS informatica para informatica 10.2.0 publicado
Lançamos uma nova versão dos conectores do informatica para APS que funciona com informatica versão 10.2.0 e 10.2.0 hotfix 1. Os novos conectores podem ser baixados do [site de download](https://www.microsoft.com/download/details.aspx?id=57472).

#### <a name="supported-versions"></a>Versões com suporte

| Versão do APS | Informatica PowerCenter | Driver |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11. x |
| APS 2016 e posterior | 10.2.0, 10.2.0 hotfix 1 | SQL Server Native Client 11. x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
Data de lançamento – outubro de 2018

### <a name="support-for-tls-12"></a>Suporte para TLS 1,2
O APS CU 7.2 dá suporte a TLS 1,2. A comunicação entre nós do computador cliente para APS e APS no nó agora pode ser definida para se comunicar somente por TLS 1.2. Ferramentas como SSDT, SSIS e Dwloader instaladas em computadores cliente que estão definidos para se comunicar somente por TLS 1,2 agora podem se conectar ao APS usando o TLS 1,2. Por padrão, o APS dará suporte a todas as versões de TLS (1,0, 1,1 e 1,2) para compatibilidade com versões anteriores. Se você quiser definir seu dispositivo APS para usar estritamente o TLS 1,2, poderá fazer isso alterando as configurações do registro. 

Para obter mais informações, consulte [Configurando o TLS 1.2 no APS](configure-tls12-aps.md).

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Suporte à zona de criptografia do Hadoop para polybase
O polybase agora pode se comunicar com as zonas de criptografia do Hadoop. Consulte as alterações de configuração do APS que são necessárias em [Configurar a segurança do Hadoop](polybase-configure-hadoop-security.md#encryptionzone).

### <a name="insert-select-maxdop-options"></a>Inserir-selecionar opções de MAXDOP
Adicionamos uma [opção de recurso](appliance-feature-switch.md) que permite que você escolha as configurações de MAXDOP maiores que 1 para operações de inserção e seleção. Agora você pode definir a configuração MAXDOP como 0, 1, 2 ou 4. O padrão é 1.

> [!IMPORTANT]  
> Às vezes, aumentar MAXDOP pode resultar em operações mais lentas ou erros de deadlock. Se isso ocorrer, altere a configuração de volta para MAXDOP 1 e repita a operação.

### <a name="columnstore-index-health-dmv"></a>DMV de integridade do índice ColumnStore
Você pode exibir informações de integridade do índice columnstore usando DMV **dm_pdw_nodes_db_column_store_row_group_physical_stats** . Use a exibição a seguir para determinar a fragmentação e decidir quando recriar ou reorganizar um índice columnstore.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>Aumento do intervalo de datas do polybase para arquivos ORC e parquet
Ler, importar e exportar tipos de dados de data usando o polybase agora oferece suporte a datas anteriores a 1970-01-01 e posteriores a 2038-01-20 para os tipos de arquivo ORC e parquet.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>Adaptador de destino SSIS para SQL Server 2017 como destino
Novo adaptador de destino SSIS APS que dá suporte a SQL Server 2017, pois o destino de implantação pode ser baixado do [site de download](https://www.microsoft.com/download/details.aspx?id=57472).

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
Data de lançamento – julho de 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>Comandos DBCC não consomem slots de simultaneidade (alteração de comportamento)
O APS dá suporte a um subconjunto dos [comandos DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) do T-SQL, como [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql). Anteriormente, esses comandos consumiram um [slot de simultaneidade](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots) que reduz o número de cargas/consultas de usuário que poderiam ser executadas. Os `DBCC` comandos agora são executados em uma fila local que não consomem um slot de simultaneidade do usuário, melhorando o desempenho geral da execução da consulta.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>Substitui algumas chamadas de metadados por objetos de catálogo
O uso de objetos de catálogo para chamadas de metadados em vez de usar o SMO mostrou a melhoria de desempenho no APS. A partir de CU 7.1, algumas dessas chamadas de metadados agora usam objetos de catálogo por padrão. Esse comportamento pode ser desativado pela [opção de recurso](appliance-feature-switch.md) se os clientes que usam consultas de metadados apresentarem problemas.

### <a name="bug-fixes"></a>Correções de bug
Atualizamos para SQL Server 2016 SP2 CU2 com APS CU 7.1. A atualização corrige alguns problemas descritos abaixo.

| Título | Descrição |
|:---|:---|
| **Deadlock potencial de movimentação de tupla** |A atualização corrige uma grande possibilidade de deadlock em um thread em segundo plano de transação distribuída e de movimentação de tupla. Depois de instalar o CU 7.1, os clientes que usaram TF634 para interromper o motor de tupla como SQL Server parâmetro de inicialização ou sinalizador de rastreamento global podem removê-lo com segurança. | 
| **Determinada consulta de retardo/Lead falha** |Algumas consultas em tabelas CCI com funções de retardo/Lead aninhadas que o erro agora são corrigidas com essa atualização. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
Data de lançamento – maio de 2018

O APS 2016 é um pré-requisito para atualizar para o AU7. Estes são os novos recursos no APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Estatísticas de criação automática e atualização automática
O APS AU7 cria e atualiza estatísticas automaticamente, por padrão. Para atualizar as configurações de estatísticas, os administradores podem usar um novo item de menu de switch de recursos no [Configuration Manager](appliance-configuration.md#CMTasks). A [opção de recurso](appliance-feature-switch.md) controla a criação automática, a atualização automática e o comportamento de atualização assíncrona de estatísticas. Você também pode atualizar as configurações de estatísticas com a instrução [ALTER DATABASE (Parallel Data warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) .

### <a name="t-sql"></a>T-SQL
Agora @var há suporte para Select. Para obter mais informações, consulte [selecionar variável local](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

O HASH de dicas de consulta e o grupo de pedidos agora têm suporte. Para obter mais informações, consulte [Hints (Transact-SQL)-Query](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>Opção de recurso
O APS AU7 introduz a opção de recurso no [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled e DmsProcessStopMessageTimeoutInSeconds agora são opções configuráveis que podem ser alteradas por administradores.

### <a name="known-issues"></a>Problemas conhecidos
Com o software APS AU7, é fornecida uma atualização de BIOS da Intel que corrige um problema descrito como *ataques de canal lateral de execução especulativa*. Os ataques visam explorar o que é chamado de *vulnerabilidades Spectre e Meltdown*. Embora sejam empacotados junto com o APS, a atualização do BIOS é instalada manualmente e não como parte da instalação do software APS AU7.

A Microsoft aconselha todos os clientes a instalarem o BIOS atualizado. A Microsoft mediu o efeito de KVAS (sombra de endereço virtual) de kernel, KPTI (indireção de tabela de página de kernel) e IBP (mitigação de previsão de ramificação indireta) em várias cargas de trabalho do SQL em vários ambientes. As medidas encontraram uma degradação significativa em algumas cargas de trabalho. Com base nos resultados, a recomendação é que você teste o efeito de desempenho da habilitação da atualização do BIOS antes de implantá-las em um ambiente de produção. Consulte as diretrizes de SQL Server [aqui](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
Esta seção descreveu os novos recursos para o APS 2016-AU6.

### <a name="sql-server-2016"></a>SQL Server 2016

O APS AU6 é executado na versão mais recente do SQL Server 2016 e usa o nível de compatibilidade de banco de dados padrão 130. O SQL Server 2016 permite o suporte para novos recursos, como:

- Índices secundários para índices columnstore clusterizados.
- Kerberos para polybase.

### <a name="t-sql"></a>T-SQL
O APS AU6 dá suporte a esses aprimoramentos de compatibilidade com T-SQL.  Esses elementos de linguagem adicionais facilitam a migração de SQL Server e outras fontes de dados. 

- Os [agrupamentos do SQL em nível de coluna][] agora têm suporte, além de agrupamentos do Windows.
- Os [índices não clusterizados em índices columnstore clusterizados][] melhoram o desempenho de consultas que pesquisam valores específicos no índice columnstore clusterizado. 
- [SELECT...INTO][] 
- [sp_spaceused ()][] exibe o espaço em disco usado ou reservado em uma tabela ou banco de dados.
- O suporte a [tabelas largas][] é o mesmo que SQL Server 2016. O limite anterior de 32 K para o tamanho da linha não existe mais. 

**Tipos de dados**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] e [VARBINARY(MAX)][]. Esses tipos de dados LOB têm um tamanho máximo de 2 GB. Para carregar esses objetos, use o [utilitário bcp][]. Atualmente, o polybase e o dwloader não dão suporte a esses tipos de dados. 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- Tipos de dados [NUMERIC][] e decimais.

**Funções de janela**

- [LINHAS ou intervalo][] na cláusula over da instrução SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**Funções de segurança**

- [CHECKSUM()][] e [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**Funções adicionais**

- [NEWID ()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>Aprimoramentos do polybase/Hadoop

- Compatibilidade com Hortonworks HDP 2,4 e HDP 2,5
- Suporte a Kerberos por meio de credenciais no escopo do banco de dados
- Suporte a credenciais com blobs de armazenamento do Azure

### <a name="install-and-upgrade-enhancements"></a>Aprimoramentos de instalação e atualização

**Atualizações de arquitetura empresarial** Atualizar seu dispositivo existente para o APS AU6 instala as atualizações mais recentes de firmware e Driver, que incluem correções de segurança. 

Um novo dispositivo da HPE ou da DELL inclui todas as atualizações mais recentes, além de:

- Suporte do processador de geração mais recente (Broadwell)
- Atualizar para DIMMs DDR4
- Taxa de transferência de DIMM aprimorada

**Integrar**

- O suporte ao FQDN (nome de domínio totalmente qualificado) possibilita a configuração de uma relação de confiança de domínio para o dispositivo. 
- Para usar o FQDN, você precisa fazer uma atualização completa e aceitar durante a atualização. 

**Tempo de inatividade reduzido** Instalar ou atualizar para o APS AU6 é mais rápido e requer menos tempo de inatividade do que as versões anteriores. Para reduzir o tempo de inatividade, instale ou atualize: 

 - Simplifica a aplicação de atualizações do WSUS usando uma imagem que contém todas as atualizações até junho de 2016
 - Aplica atualizações de segurança com as atualizações de driver e firmware
 - Coloca os hotfixes mais recentes e o PAV (utilitário de verificação do dispositivo) em seu dispositivo para que eles estejam prontos para serem instalados sem a necessidade de baixá-los.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[Agrupamentos do SQL em nível de coluna]: ~/relational-databases/collations/collation-and-unicode-support.md

[Índices não clusterizados em índices columnstore clusterizados]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused ()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Tabelas largas]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[Utilitário bcp]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[LINHAS ou intervalo]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID ()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


