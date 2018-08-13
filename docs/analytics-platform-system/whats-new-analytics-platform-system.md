---
title: O que há de novo no Analytics Platform System – um depósito de dados de expansão
description: Veja o que há de novo no Microsoft® Analytics Platform System, um dispositivo de escalabilidade horizontal no local que hospeda o MPP SQL Server Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b4059d9460eec5cd69e6e8b4a2f2ac95af5b3d0e
ms.sourcegitcommit: 2e038db99abef013673ea6b3535b5d9d1285c5ae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39400639"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>O que há de novo no Analytics Platform System, um data warehouse MPP de escalabilidade horizontal
Veja o que há de novo nas atualizações mais recentes do dispositivo para o Microsoft® Analytics Platform System (APS). Pontos de acesso é um dispositivo de escalabilidade horizontal no local que hospeda o MPP SQL Server Parallel Data Warehouse. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"

## <a name="aps-au7"></a>AU7 APS
APS 2016 é um pré-requisito para atualizar para AU7. A seguir é novos no APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Criação automática e a atualização automática de estatísticas
APS AU7 cria e atualiza as estatísticas automaticamente, por padrão. Para atualizar as configurações de estatísticas, os administradores podem usar um novo item de menu do comutador de recurso nas [Configuration Manager](appliance-configuration.md#CMTasks). O [comutador de recurso](appliance-feature-switch.md) controla a auto-create, a atualização automática e o comportamento de atualização assíncrona de estatísticas. Você também pode atualizar as configurações de estatísticas com o [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) instrução.

### <a name="t-sql"></a>T-SQL
Selecione @var agora tem suporte. Para obter mais informações, consulte [Selecione variável local] (/ sql/t-sql/language-elements/select-local-variable-transact-sql) 

Agora há suporte para dicas de consulta HASH e o grupo de ordem. Para obter mais informações, consulte [Hints(Transact-SQL) - consulta] (/ sql/t-sql/consultas/dicas-transact-sql-query)

### <a name="feature-switch"></a>Comutador de recurso
Apresenta o comutador de recurso no APS AU7 [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled e DmsProcessStopMessageTimeoutInSeconds agora são opções configuráveis que podem ser alteradas por administradores.

### <a name="known-issues"></a>Problemas conhecidos
Com o software AU7 APS, uma atualização do BIOS da Intel é fornecida que corrige um problema descrito como *ataques de canal lateral de execução especulativa*. Os ataques tem como objetivo para explorar o que é chamado *vulnerabilidades Spectre e Meltdown*. Embora empacotado junto com os pontos de acesso, a atualização do BIOS é instalada manualmente e não como parte da instalação de software AU7 APS.

Microsoft recomenda que todos os clientes instalem a atualização do BIOS. Microsoft mediu o efeito de Kernel Virtual endereço sombreamento (KVAS), o Kernel página tabela de indireção (kpti) e e mitigação de previsão de ramificação indireta (IBP) em várias cargas de trabalho do SQL em vários ambientes. As medidas encontrada uma redução significativa no algumas cargas de trabalho. Com base nos resultados, a recomendação é que você teste o efeito de desempenho de habilitar a atualização do BIOS antes de implantá-los em um ambiente de produção. Consulte o guia do SQL Server [aqui](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"

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

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] e [VARBINARY(MAX)][]. Esses tipos de dados LOB têm um tamanho máximo de 2 GB. Para carregar esses objetos usam [utilitário bcp][]. O Polybase e dwloader não damos suporte a esses tipos de dados. 
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


  

  


