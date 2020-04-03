---
title: O que há de novo
description: Veja as novidades do Microsoft Analytics Platform System, um dispositivo de escala no local que hospeda o MPP SQL Server Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: faf3bd1f487fb5c850759fdde3ddecd32bdd3b1f
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625536"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>O que há de novo no Analytics Platform System, um data warehouse MPP em escala
Veja as novidades das atualizações mais recentes do Appliance Updates for Microsoft Analytics Platform System (APS). O APS é um aparelho de escala no local que hospeda o MPP SQL Server Parallel Data Warehouse. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.6"></a>
## <a name="aps-cu76"></a>APS CU7.6
Data de lançamento - Abril 2020

### <a name="rename-column"></a>Renomear coluna
Após a atualização para CU7.6, os clientes poderão renomear uma coluna de uma tabela criada pelo usuário. Consulte [RENAME (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/rename-transact-sql) para obter sintaxe, exemplos, limitações e mais informações.

### <a name="alter-view"></a>Alterar visualização
Os clientes agora poderão alterar as visualizações. Consulte [ALTER VIEW (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-view-transact-sql) para obter mais informações.

<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
Data de lançamento - Setembro 2019

### <a name="alter-external-data-source"></a>Alterar fonte de dados externos
Os clientes poderão alterar a definição de fonte de dados externos com a atualização CU7.5. Os clientes com nome Hadoop de alta disponibilidade agora podem alterar a fonte de dados para alterar os argumentos quando um failover acontece. Para APS, somente o LOCAL, RESOURCE_MANAGER_LOCATION e CREDENCIAL podem ser alterados. Consulte [alterar a fonte de dados externos](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017) para obter mais informações.

### <a name="cdh-515-and-516-support-with-polybase"></a>Suporte ao CDH 5.15 e 5.16 com PolyBase
O PolyBase no APS com atualização CU7.5 agora suporta versões CDH 5.15 e 5.16 da distribuição Hadoop da Cloudera. Use a opção 6 para as versões CDH 5.x. 

### <a name="try_convert-and-try_cast-support"></a>apoio Try_Convert e Try_Cast
Cu7.5 APS agora suporta funções [TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017) e [TRY_CONVERT](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) tsql. Ambas as funções devolveum valor convertido para o tipo de dados especificado se o convertido for bem sucedido; caso contrário, retorna nulo.

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
Data de lançamento - Maio 2019

### <a name="loading-large-rows-with-dwloader"></a>Carregando grandes linhas com dwloader
A partir de APS CU7.4, os clientes poderão usar um novo dwloader para carregar linhas em tabelas maiores que 32 KB (32.768 bytes). O novo dwloader suporta o interruptor -l que leva um valor inteiro entre 32768 e 33554432 (em bytes) para carregar linhas maiores que 32 KB. Use apenas essa opção ao carregar linhas grandes (maiores que 32 KB), pois este switch irá alocar mais memória no cliente e no servidor e pode retardar as cargas. Você pode baixar o novo dwloader do site de [download](https://www.microsoft.com/download/details.aspx?id=57472).  

### <a name="hdp-30-and-31-support-with-polybase"></a>Suporte hdp 3.0 e 3.1 com PolyBase
O PolyBase no APS agora suporta HDP 3.0 e 3.1 com esta atualização. Use a opção 7 para versões HDP 3.x. Para obter mais informações, consulte a página [de conectividade PolyBase.](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql)

### <a name="utf16-file-support-with-polybase"></a>Suporte a arquivos UTF16 com PolyBase
O PolyBase agora suporta a leitura de arquivos de texto delimitados que estão na codificação UTF16 (LE). Consulte [criar formato de arquivo externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) para detalhes de configuração. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
Data de lançamento - Dezembro 2018

### <a name="common-subexpression-elimination"></a>Eliminação de subexpressão comum
O APS CU7.3 melhora o desempenho da consulta com a eliminação comum de subexpressão no otimizador de consulta SQL. A melhoria melhora as consultas de duas maneiras. O primeiro benefício é a capacidade de identificar e eliminar tais expressões ajuda a reduzir o tempo de compilação do SQL. O segundo e mais importante benefício é que as operações de movimentação de dados para essas subexpressões redundantes são eliminadas, assim, o tempo de execução para consultas torna-se mais rápido. Uma explicação detalhada deste recurso pode ser encontrada [aqui.](common-sub-expression-elimination.md)

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Conector APS Informatica para Informatica 10.2.0 publicado
Lançamos uma nova versão de conectores Informatica para APS que funciona com a versão Informatica 10.2.0 e 10.2.0 Hotfix 1. Os novos conectores podem ser baixados no site de [download](https://www.microsoft.com/download/details.aspx?id=57472).

#### <a name="supported-versions"></a>Versões compatíveis

| Versão APS | Informatica PowerCenter | Driver |
|:---|:---|:---|
| APS 2016 | 9.6.1 | Cliente nativo do servidor SQL 11.x |
| APS 2016 e posterior | 10.2.0, 10.2.0 Hotfix 1 | Cliente nativo do servidor SQL 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
Data de lançamento - Outubro 2018

### <a name="support-for-tls-12"></a>Suporte para o TLS 1.2
O APS CU7.2 suporta O TLS 1.2. A comunicação intra-nó do cliente para APS e APS agora pode ser definida para se comunicar apenas pelo TLS1.2. Ferramentas como SSDT, SSIS e Dwloader instaladas em máquinas clientes que são definidas para se comunicar apenas através do TLS 1.2 agora podem se conectar ao APS usando o TLS 1.2. Por padrão, o APS suportará todas as versões TLS (1.0, 1.1 e 1.2) para compatibilidade retroativa. Se você deseja definir o seu aparelho APS para usar estritamente o TLS 1.2, você pode fazê-lo alterando as configurações do registro. 

Para obter mais informações, consulte [configuração tls1.2 em APS](configure-tls12-aps.md).

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Suporte à zona de criptografia Hadoop para PolyBase
O PolyBase agora pode se comunicar com as zonas de criptografia Hadoop. Consulte as alterações de configuração do APS necessárias [na configuração da segurança Hadoop](polybase-configure-hadoop-security.md#encryptionzone).

### <a name="insert-select-maxdop-options"></a>Inserir-Selecionar opções maxdop
Adicionamos um [switch de recurso](appliance-feature-switch.md) que permite escolher configurações maxdop maiores que 1 para operações selecionadas por inserção. Agora você pode definir a configuração maxdop como 0, 1, 2 ou 4. O padrão é 1.

> [!IMPORTANT]  
> O aumento do maxdop pode, por vezes, resultar em operações mais lentas ou erros de impasse. Se isso ocorrer, mude a configuração de volta para maxdop 1 e tente novamente a operação.

### <a name="columnstore-index-health-dmv"></a>ColumnStore índice de saúde Detran
Você pode visualizar as informações de saúde do índice columnstore usando **dm_pdw_nodes_db_column_store_row_group_physical_stats** detran. Use a seguinte exibição para determinar a fragmentação e decida quando reconstruir ou reorganizar um índice de columnstore.

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

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>Aumento da faixa de data sinuosa do PolyBase para arquivos ORC e Parquet
A leitura, importação e exportação de tipos de dados de data saem agora com datas anteriores a 1970-01-01 e depois de 2038-01-20 para tipos de arquivos ORC e Parquet.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>Adaptador de destino SSIS para SQL Server 2017 como alvo
Novo adaptador de destino APS SSIS que suporta o SQL Server 2017 como destino de implantação pode ser baixado do site de [download](https://www.microsoft.com/download/details.aspx?id=57472).

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
Data de lançamento - Julho 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>Os comandos DBCC não consomem slots de concorrência (mudança de comportamento)
O APS suporta um subconjunto dos comandos T-SQL [DBCC,](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) como [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql). Anteriormente, esses comandos consumiriam um [slot de simultaneidade](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots), reduzindo o número de carregamentos/consultas do usuário que poderiam ser executadas. Os `DBCC` comandos agora são executados em uma fila local que não consome um slot de slot de concorrência do usuário melhorando o desempenho geral de execução da consulta.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>Substitui algumas chamadas de metadados por objetos de catálogo
O uso de objetos de catálogo para chamadas de metadados em vez de usar o SMO mostrou melhora de desempenho no APS. A partir de CU7.1, algumas dessas chamadas de metadados agora usam objetos de catálogo por padrão. Esse comportamento pode ser desligado pelo [feature switch](appliance-feature-switch.md) se os clientes que usam consultas de metadados se depararem com quaisquer problemas.

### <a name="bug-fixes"></a>Correções de bug
Nós atualizamos para O SQL Server 2016 SP2 CU2 com APS CU7.1. A atualização corrige alguns problemas descritos abaixo.

| Title | Descrição |
|:---|:---|
| **Potencial impasse tuplo** |O upgrade corrige uma possibilidade de impasse de longa data em uma transação distribuída e um segmento de fundo de mover tuplo. Depois de instalar o CU7.1, os clientes que usaram o TF634 para parar o mover tupla como parâmetro de inicialização do SQL Server ou sinalizador de rastreamento global podem removê-lo com segurança. | 
| **Falha em determinada consulta de lag/lead** |Certas consultas em tabelas CCI com funções de lag/lead aninhadas que errariam agora são corrigidas com esta atualização. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
Data de lançamento - Maio 2018

APS 2016 é um pré-requisito para atualizar para AU7. A seguir, novos recursos no APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Estatísticas de criação automática e atualização automática
O APS AU7 cria e atualiza estatísticas automaticamente, por padrão. Para atualizar as configurações de estatísticas, os administradores podem usar um novo item do menu do switch de recursos no [Gerenciador de configuração](appliance-configuration.md#CMTasks). O [switch de recursos](appliance-feature-switch.md) controla o comportamento de criação automática, atualização automática e atualização assíncrona das estatísticas. Você também pode atualizar as configurações de estatísticas com a declaração [ALTER DATABASE (Parallel Data Warehouse).](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)

### <a name="t-sql"></a>T-SQL
O @var select agora é suportado. Para obter mais informações, consulte [selecionar variável local](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

As dicas de consulta HASH e ORDER GROUP são agora suportadas. Para obter mais informações, consulte [Dicas (Transact-SQL) - Consulta](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>Interruptor de recursos
APS AU7 introduz o Feature Switch no [Gerenciador de Configuração](launch-the-configuration-manager.md). AutoStatsEnabled e DmsProcessStopMessageTimetimeInSeconds são agora opções configuráveis que podem ser alteradas pelos administradores.

### <a name="known-issues"></a>Problemas conhecidos
Com o software APS AU7, é fornecida uma atualização do Intel BIOS que corrige um problema descrito como *ataques especulativos de canal lateral de execução*. Os ataques visam explorar as chamadas *vulnerabilidades Spectre e Meltdown.* Embora empacotado em conjunto com o APS, a atualização do BIOS é instalada manualmente, e não como parte da instalação do software APS AU7.

A Microsoft aconselha todos os clientes a instalar o BIOS atualizado. A Microsoft mediu o efeito do Kernel Virtual Address Shadowing (KVAS), da Indirection da Tabela de Página do Kernel (KPTI) e da mitigação da previsão de ramificação indireta (IBP) em várias cargas de trabalho SQL em vários ambientes. As medidas encontraram degradação significativa em algumas cargas de trabalho. Com base nos resultados, a recomendação é que você teste o efeito de desempenho de habilitar a atualização do BIOS antes de implantá-los em um ambiente de produção. Veja a orientação do SQL Server [aqui](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
Esta seção descreveu os novos recursos para APS 2016-AU6.

### <a name="sql-server-2016"></a>SQL Server 2016

O APS AU6 é executado na versão mais recente do SQL Server 2016 e usa o nível de compatibilidade padrão do banco de dados 130. O SQL Server 2016 permite o suporte para novos recursos, como:

- Índices secundários para índices de columnstore agrupados.
- Kerberos para PolyBase.

### <a name="t-sql"></a>T-SQL
O APS AU6 suporta essas melhorias de compatibilidade T-SQL.  Esses elementos adicionais de linguagem facilitam a migração do SQL Server e de outras fontes de dados. 

- [As colagens SQL em nível de coluna][] são agora suportadas, além das colagens do Windows.
- [Índices não agrupados em índices de columnstore agrupados][] melhoram o desempenho de consultas que pesquisam valores específicos no índice de columnstore clustered. 
- [SELECT...INTO][] 
- [sp_spaceused exibe][] o espaço em disco usado ou reservado em uma tabela ou banco de dados.
- O suporte a [tabelas largas][] é o mesmo do SQL Server 2016. O limite anterior de 32 K para o tamanho da linha não existe mais. 

**Tipos de dados**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] e [VARBINARY(MAX)][]. Esses tipos de dados LOB têm um tamanho máximo de 2 GB. Para carregar esses objetos use [bcp Utility][]. O PolyBase e o dwloader não suportam atualmente esses tipos de dados. 
- [SYSNAME][]
- [Uniqueidentifier][]
- Tipos de dados [NUMERIC][] e DECIMAL.

**Funções da janela**

- [LINHAS ou INTERVALO][] na cláusula OVER da declaração SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**Funções de segurança**

- [CHECKSUM()][] e [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME][]

**Funções adicionais**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>Aprimoramentos polyBase/Hadoop

- Compatibilidade com Hortonworks HDP 2.4 e HDP 2.5
- Suporte kerberos via credenciais com escopo de banco de dados
- Suporte de credencial com Blobs de armazenamento Azure

### <a name="install-and-upgrade-enhancements"></a>Instalar e atualizar melhorias

**Atualizações de arquitetura corporativa** O upgrade do seu aparelho existente para o APS AU6 instala as atualizações mais recentes de firmware e driver, que incluem correções de segurança. 

Um novo aparelho da HPE ou DA DELL inclui todas as atualizações mais recentes:

- Suporte ao processador de última geração (Broadwell)
- Atualização para DIMMs DDR4
- Melhor throughput DIMM

**Integração**

- O suporte ao Nome de Domínio Totalmente Qualificado (FQDN) permite configurar uma confiança de domínio para o aparelho. 
- Para usar o FQDN, você precisa fazer uma atualização completa e opt-in durante a atualização. 

**Tempo de inatividade reduzido** A instalação ou atualização do APS AU6 é mais rápida e requer menos tempo de inatividade do que as versões anteriores. Para reduzir o tempo de inatividade, a instalação ou atualização: 

 - Simplifica a aplicação de atualizações wsus usando uma imagem que contém todas as atualizações até junho de 2016
 - Aplica atualizações de segurança com as atualizações de driver e firmware
 - Coloca os mais recentes hotfixes e o utilitário de verificação do aparelho (PAV) no seu aparelho para que eles estejam prontos para instalar sem necessidade de baixá-los.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[Colagem SQL em nível de coluna]: ~/relational-databases/collations/collation-and-unicode-support.md

[Índices não agrupados em índices de columnstore agrupados]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Mesas largas]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[Utilitário bcp]:/sql/tools/bcp-utility
[Uniqueidentifier]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[Numérico]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[LINHAS ou INTERVALO]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


