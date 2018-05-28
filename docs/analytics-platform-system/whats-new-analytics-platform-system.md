---
title: O que há de novo no Analytics Platform System – um depósito de dados de expansão
description: Veja o que há de novo no Microsoft® Analytics Platform System, um aplicativo de expansão no local que hospeda MPP SQL Server Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2408e84e7ff81f54ad00a98f85cd8dce7b04131
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>O que há de novo no Analytics Platform System, um data warehouse de MPP de expansão
Veja o que há de novo nas atualizações mais recentes do dispositivo para o Microsoft® Analytics Platform System (APS). Pontos de acesso é um aplicativo de expansão no local que hospeda MPP SQL Server Parallel Data Warehouse. 


## <a name="aps-au7"></a>AU7 APS
APS2016 é um pré-requisito para atualizar para AU7. A seguir estão os novos recursos para os PAS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Criar automaticamente e a atualização automática de estatísticas
APS AU7 cria e atualiza estatísticas automaticamente, por padrão. Para atualizar as configurações de estatísticas, os administradores podem usar um novo item de menu de comutador de recurso no [do Configuration Manager](appliance-configuration.md#CMTasks). O [opção](appliance-feature-switch.md) controla a auto-create, a atualização automática e o comportamento de atualização assíncrona de estatísticas. Você também pode atualizar as configurações de estatísticas com a [ALTER DATABASE (Parallel Data Warehouse)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) instrução.

### <a name="t-sql"></a>T-SQL
Selecione @var agora tem suporte. Para obter mais informações, consulte [Selecione variável local] (/ sql/t-sql/language-elements/select-local-variable-transact-sql) 

Agora há suporte para dicas de consulta HASH e o grupo de ordem. Para obter mais informações, consulte [Hints(Transact-SQL) - consulta] (/ / t-sql/consultas/dicas-transact-sql-consulta sql)

### <a name="feature-switch"></a>Opção de recurso
APS AU7 apresenta o recurso de comutador no [do Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled e DmsProcessStopMessageTimeoutInSeconds agora são opções configuráveis que podem ser alteradas por administradores.

### <a name="known-issues"></a>Problemas conhecidos
Com o software de APS AU7, estamos empacotamento e fornecendo a atualização de BIOS Intel que corrige "ataques de canal lateral execução especulativa" (também conhecido como. Vulnerabilidades spectre e sobrecarga). Embora a atualização do BIOS reunidos, é instalada manualmente e não faz parte do software APS AU7 instalar. O Microsoft avisa todos os clientes instalem a atualização do BIOS. A Microsoft medido o efeito de Kernel virtuais endereço sombreamento (KVAS), inversão de controle de tabela na página do Kernel (KPTI) e previsão de ramificação indireta mitigação (IBP) em várias cargas de trabalho do SQL em vários ambientes e encontrar uma queda significativa em alguns cargas de trabalho. É recomendável que você teste o efeito de desempenho de habilitar a atualização do BIOS antes de implantá-los em um ambiente de produção. Se o efeito de desempenho de habilitar esses recursos é muito alto para um aplicativo existente, você pode considerar se isolar seu aparelho de pontos de acesso de execução de código não confiável é uma melhor atenuação para seu aplicativo. Consulte o guia do SQL Server [aqui](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

## <a name="aps-2016"></a>APS 2016
Estes são os novos recursos do APS 2016:

### <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 é executado na versão mais recente do SQL Server 2016 e usa o nível de compatibilidade do banco de dados padrão 130.  SQL Server 2016 torna possível dar suporte a alguns dos novos recursos, como índices secundários para índices columnstore clusterizados e o Kerberos para PolyBase. 


### <a name="t-sql"></a>T-SQL
APS 2016 dá suporte a esses melhorias de compatibilidade do T-SQL.  Esses elementos de linguagem adicionais facilitam a migração do SQL Server e outras fontes de dados. 

- [Agrupamentos no nível de coluna SQL][] agora têm suporte além de agrupamentos do Windows.
- [Índices não clusterizados em índices columnstore clusterizados][] melhorar o desempenho de consultas que pesquisam valores específicos no índice columnstore clusterizado. 
- [SELECT...INTO][] 
- [sp_spaceused()][] exibe o espaço em disco usado ou reservados em uma tabela ou banco de dados.
- [Tabelas largas][] suporte é o mesmo SQL Server 2016. O limite anterior de 32K para o tamanho de linha não existe mais. 

**Tipos de dados**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] e [VARBINARY(MAX)][]. Esses tipos de dados LOB têm um tamanho máximo de 2 GB. Para carregar esses objetos de uso [bcp Utility][]. Polybase e dwloader atualmente não suportam esses tipos de dados. 
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

### <a name="polybasehadoop-enhancements"></a>Aprimoramentos de PolyBase/Hadoop

- Compatibilidade com Hortonworks HDP 2.4 e HDP 2.5
- Suporte a Kerberos por meio de credenciais no escopo do banco de dados
- Suporte de credencial com Blobs de armazenamento do Azure

### <a name="install-and-upgrade-enhancements"></a>Instalar e aprimoramentos de atualização

**Atualizações de arquitetura empresarial** atualizar seu dispositivo existente para APS 2016 instala o firmware mais recente e atualizações de driver, que incluem correções de segurança. 

Um novo dispositivo de HPE ou DELL inclui todas as atualizações mais recentes plus:

- Suporte de processador de geração mais recente (Broadwell)
- Atualizar para DIMMs DDR4
- Maior taxa de transferência do DIMM

**Integração**

- Totalmente o suporte de nome de domínio qualificado (FQDN) possibilita configurar uma relação de confiança de domínio para o dispositivo. 
- Para usar o FQDN, você precisa fazer uma atualização completa e participar durante a atualização. 

**Tempo de inatividade reduzido** instalando ou atualizando para o APS 2016 é mais rápido e requer menos tempo de inatividade de versões anteriores. Para reduzir o tempo de inatividade, a instalação ou atualização: 

 - Simplifica a aplicação de atualizações do WSUS usando uma imagem que contém todas as atualizações por meio de junho de 2016
 - Aplica atualizações de segurança com as atualizações de firmware e driver
 - Coloca os hotfixes mais recentes e o utilitário de verificação de dispositivo (PAV) em sua aplicação para que eles fiquem prontos para instalar sem precisar baixá-los.


<!--MSDN references-->
[database compatibility level 130]:/sql/t-sql/statements/alter-database-transact-sql-compatibility-level
[Agrupamentos no nível de coluna SQL]:/sql/relational-databases/collations/collation-and-unicode-support
[Índices não clusterizados em índices columnstore clusterizados]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Tabelas largas]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp Utility]:/sql/tools/bcp-utility
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


  

  


