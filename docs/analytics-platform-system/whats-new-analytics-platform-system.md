---
title: O que há de novo no Analytics Platform System – um depósito de dados de expansão
description: Veja o que há de novo no Microsoft Analytics Platform System, um dispositivo de escalabilidade horizontal no local que hospeda o MPP SQL Server Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5467362b32733e6ef10036bf9b45d38fe3150a1e
ms.sourcegitcommit: c51f7f2f5d622a1e7c6a8e2270bd25faba0165e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53626350"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>O que há de novo no Analytics Platform System, um data warehouse MPP de escalabilidade horizontal
Veja o que há de novo nas atualizações mais recentes do dispositivo para o Microsoft Analytics Platform System (APS). Pontos de acesso é um dispositivo de escalabilidade horizontal no local que hospeda o MPP SQL Server Parallel Data Warehouse. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>CU7.3 DE APS
Data de lançamento - dezembro de 2018

### <a name="common-subexpression-elimination"></a>Eliminação de subexpressão comum
APS CU7.3 melhora o desempenho de consulta com eliminação de subexpressão comum no otimizador de consulta SQL. O aprimoramento melhora a consultas de duas maneiras. A primeira vantagem é a capacidade de identificar e eliminar tais expressões ajudam a reduzir o tempo de compilação do SQL. O benefício de segundo e mais importante é que operações de movimentação de dados para essas subexpressão com redundância são eliminadas, portanto, o tempo de execução para consultas se torna mais rápido. Uma explicação detalhada desse recurso pode ser encontrada [aqui](common-sub-expression-elimination.md).

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Conector de APS Informatica para o Informatica 10.2.0 publicado
Lançamos uma nova versão dos conectores do Informatica para APS que funciona com o Informatica versão 10.2.0. Os novos conectores podem ser baixados em [site de download](https://www.microsoft.com/download/details.aspx?id=57472).

#### <a name="supported-versions"></a>Versões com suporte
| Versão APS | PowerCenter de Informatica | Driver |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 e posterior | 10.2.0 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
Data de lançamento - outubro de 2018

### <a name="support-for-tls-12"></a>Suporte para TLS 1.2
APS CU7.2 dá suporte a TLS 1.2. Computador cliente para pontos de acesso e APS comunicação entre nós agora pode ser definida para se comunicar somente por TLS1.2. Ferramentas como o SSDT, SSIS e Dwloader instalado nos computadores cliente que são definidas para se comunicar somente por TLS 1.2 agora podem se conectar ao APS usando o TLS 1.2. Por padrão, os APS oferecerão suporte a todas as versões do TLS (1.0, 1.1 e 1.2) para compatibilidade com versões anteriores. Se você deseja definir o seu dispositivo de APS estritamente usar TLS 1.2, você pode fazer isso alterando as configurações do registro. 

Para obter mais informações, consulte [Configurando o TLS1.2 em APS](configure-tls12-aps.md).

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Suporte a zona de criptografia do Hadoop para o PolyBase
PolyBase agora pode comunicar-se às zonas de criptografia do Hadoop. Veja as alterações de configuração de pontos de acesso que são necessários no [configurar a segurança do Hadoop](polybase-configure-hadoop-security.md#encryptionzone).

### <a name="insert-select-maxdop-options"></a>Opções de maxdop Insert-Select
Adicionamos uma [comutador de recurso](appliance-feature-switch.md) que permite que você escolha as configurações de maxdop maiores que 1 para operações insert-select. Agora você pode definir a configuração maxdop como 0, 1, 2 ou 4. O padrão é 1.

> [!IMPORTANT]  
> Aumentar o maxdop, às vezes, pode resultar em operações mais lentas ou erros de deadlock. Se isso ocorrer, altere a configuração novamente para maxdop 1 e repita a operação.

### <a name="columnstore-index-health-dmv"></a>Integridade do índice ColumnStore DMV
Você pode exibir informações de integridade de índice de columnstore usando **dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv. Use a exibição a seguir para determinar a fragmentação e decidir quando recriar ou reorganizar um índice columnstore.

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

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>Aumento de intervalo de data do PolyBase para arquivos ORC e Parquet
Ler, importar e exportar tipos de dados de data usando o PolyBase dá suporte a datas antes de 1970-01-01 e depois 2038-01-20 para tipos de arquivo ORC e Parquet.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>Adaptador de destino do SSIS para SQL Server 2017 como destino
Novo adaptador de destino SSIS APS que dá suporte ao SQL Server 2017 como destino de implantação pode ser baixado do [site de download](https://www.microsoft.com/download/details.aspx?id=57472).

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
Data de lançamento - julho de 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>Comandos DBCC não consomem slots de simultaneidade (alteração de comportamento)
APS dá suporte a um subconjunto do T-SQL [comandos DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) tais como [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql). Anteriormente, esses comandos consumiria um [slot de simultaneidade](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots) reduzindo o número de carregamentos/consultas de usuário que podem ser executadas. O `DBCC` comandos agora são executados em uma fila local que não consomem um slot de simultaneidade de usuário melhorando o desempenho de execução de consulta global.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>Substitui algumas chamadas de metadados com objetos de catálogo
Usar objetos de catálogo para chamadas de metadados em vez de usar o SMO mostrou a melhoria de desempenho dos pontos de acesso. A partir da CU7.1, algumas dessas chamadas de metadados agora usam objetos de catálogo por padrão. Esse comportamento pode ser desativado pelo [comutador de recurso](appliance-feature-switch.md) se os clientes que usam consultas de metadados se tiver algum problema.

### <a name="bug-fixes"></a>Correções de bugs
Atualizamos para SQL Server 2016 SP2 CU2 com CU7.1 APS. A atualização corrige alguns problemas descritos abaixo.

| Title | Descrição |
|:---|:---|
| **Deadlock potencial de motor de tupla** |A atualização corrige uma possibilidade de longa data de deadlock em um thread de plano de fundo de motor tupla e de transação distribuído. Depois de instalar CU7.1, os clientes que usaram TF634 para interromper o motor da tupla como parâmetro de inicialização do SQL Server ou o sinalizador de rastreamento global com segurança remova-a. | 
| **Ocorre falha na consulta determinados lag/lead.** |Determinadas consultas em tabelas CCI com funções aninhadas lag/lead que seriam o erro agora é corrigido com essa atualização. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
Data de lançamento - maio de 2018

APS 2016 é um pré-requisito para atualizar para AU7. Estes são os novos recursos no APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Criação automática e a atualização automática de estatísticas
APS AU7 cria e atualiza as estatísticas automaticamente, por padrão. Para atualizar as configurações de estatísticas, os administradores podem usar um novo item de menu do comutador de recurso nas [Configuration Manager](appliance-configuration.md#CMTasks). O [comutador de recurso](appliance-feature-switch.md) controla a auto-create, a atualização automática e o comportamento de atualização assíncrona de estatísticas. Você também pode atualizar as configurações de estatísticas com o [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) instrução.

### <a name="t-sql"></a>T-SQL
Selecione @var agora tem suporte. Para obter mais informações, consulte [selecione a variável local](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

Agora há suporte para dicas de consulta HASH e o grupo de ordem. Para obter mais informações, consulte [Hints(Transact-SQL) - consulta ](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>Comutador de recurso
Apresenta o comutador de recurso no APS AU7 [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled e DmsProcessStopMessageTimeoutInSeconds agora são opções configuráveis que podem ser alteradas por administradores.

### <a name="known-issues"></a>Problemas conhecidos
Com o software AU7 APS, uma atualização do BIOS da Intel é fornecida que corrige um problema descrito como *ataques de canal lateral de execução especulativa*. Os ataques tem como objetivo para explorar o que é chamado *vulnerabilidades Spectre e Meltdown*. Embora empacotado junto com os pontos de acesso, a atualização do BIOS é instalada manualmente e não como parte da instalação de software AU7 APS.

Microsoft recomenda que todos os clientes instalem a atualização do BIOS. Microsoft mediu o efeito de Kernel Virtual endereço sombreamento (KVAS), o Kernel página tabela de indireção (kpti) e e mitigação de previsão de ramificação indireta (IBP) em várias cargas de trabalho do SQL em vários ambientes. As medidas encontrada uma redução significativa no algumas cargas de trabalho. Com base nos resultados, a recomendação é que você teste o efeito de desempenho de habilitar a atualização do BIOS antes de implantá-los em um ambiente de produção. Consulte o guia do SQL Server [aqui](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
Esta seção descreveu os novos recursos para AU6 APS 2016.

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 é executado sobre a versão mais recente do SQL Server 2016 e usa o nível de compatibilidade do banco de dados padrão 130. SQL Server 2016 permite o suporte para novos recursos, como:

- Índices secundários para índices columnstore clusterizados.
- Kerberos para o PolyBase.

### <a name="t-sql"></a>T-SQL
APS AU6 dá suporte a esses aprimoramentos de compatibilidade do T-SQL.  Esses elementos de linguagem adicionais facilitam a migração do SQL Server e outras fontes de dados. 

- [Agrupamentos no nível de coluna SQL][] agora têm suporte, além de agrupamentos do Windows.
- [Índices não clusterizados em índices columnstore clusterizados][] melhorar o desempenho de consultas que pesquisam valores específicos no índice columnstore clusterizado. 
- [SELECT...INTO][] 
- [sp_spaceused()][] exibe o espaço em disco usado ou reservado em uma tabela ou banco de dados.
- [Tabelas largas][] suporte é o mesmo SQL Server 2016. O limite anterior de 32 K para o tamanho de linha não existe mais. 

**Tipos de dados**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] e [VARBINARY(MAX)][]. Esses tipos de dados LOB têm um tamanho máximo de 2 GB. Para carregar esses objetos usam [utilitário bcp][]. O PolyBase e dwloader não damos suporte a esses tipos de dados. 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][] e tipos de dados DECIMAL.

**Funções de janela**

- [ROWS ou RANGE][] na cláusula OVER da instrução SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**Funções de segurança**

- [CHECKSUM()][] e [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**Funções adicionais**

- [NEWID)][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>Aprimoramentos do PolyBase/Hadoop

- Compatibilidade com o Hortonworks HDP 2.4 e HDP 2.5
- Suporte a Kerberos por meio de credenciais no escopo do banco de dados
- Suporte de credencial com Blobs de armazenamento do Azure

### <a name="install-and-upgrade-enhancements"></a>Instalar e aprimoramentos de atualização

**Atualizações de arquitetura empresarial** atualizar seu dispositivo existente para APS AU6 instala o firmware mais recente e atualizações de driver, que incluem correções de segurança. 

Um novo dispositivo de HPE ou DELL inclui todas as atualizações mais recentes plus:

- Suporte de processador de geração mais recente (Broadwell)
- Atualizar para DIMMs DDR4
- Taxa de transferência aprimorada DIMM

**Integração**

- Totalmente o suporte de nome de domínio qualificado (FQDN) possibilita configurar uma relação de confiança de domínio para o dispositivo. 
- Para usar o FQDN, você precisa fazer uma atualização completa e inscreva-se no durante a atualização. 

**Tempo de inatividade reduzido** instalando ou atualizando para o APS AU6 é mais rápido e requer menos tempo de inatividade que nas versões anteriores. Para reduzir o tempo de inatividade, a instalação ou atualização: 

 - Simplifica a aplicação de atualizações do WSUS usando uma imagem que contém todas as atualizações por meio de junho de 2016
 - Aplica atualizações de segurança com as atualizações de firmware e driver
 - Coloca os hotfixes mais recentes e o utilitário de verificação de dispositivo (PAV) em seu dispositivo para que eles estão prontos para instalar sem precisar baixá-los.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[Agrupamentos no nível de coluna SQL]: ~/relational-databases/collations/collation-and-unicode-support.md

[Índices não clusterizados em índices columnstore clusterizados]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Tabelas largas]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[Utilitário bcp]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS ou RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID)]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


