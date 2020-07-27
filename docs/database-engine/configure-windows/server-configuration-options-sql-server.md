---
title: Opções de configuração de servidor (SQL Server) | Microsoft Docs
description: Descubra como gerenciar e otimizar os recursos do SQL Server. Veja as opções de configuração disponíveis, as configurações possíveis, os valores padrão e os requisitos de reinicialização.
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
keywords:
- configuração de servidor [SQL Server]
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ffbb3df5a8a8dac4ce22c27a1194520e8b058de
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923596"
---
# <a name="server-configuration-options-sql-server"></a>Opções de configuração do servidor (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

É possível gerenciar e otimizar recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de opções de configuração usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o procedimento armazenado do sistema sp_configure. As opções de configuração de servidor usadas com mais frequência estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; todas as opções de configuração podem ser acessadas pelo sp_configure. Avalie atentamente os efeitos dessas opções no sistema antes de defini-las. Para obter mais informações, veja [Exibir ou alterar propriedades de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).

>**IMPORTANTE:** As opções avançadas só devem ser alteradas por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="categories-of-configuration-options"></a>Categorias de opções de configuração

As opções de configuração passam a vigorar:

- Imediatamente após a definição da opção e da emissão da instrução **RECONFIGURE** (ou, em alguns casos, **RECONFIGURE WITH OVERRIDE**). Reconfigurar determinadas opções invalidará planos em cache do plano, fazendo com que novos planos a serem compilados. Para obter mais informações, veja [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md).

  \- ou –

- Após a execução das ações anteriores e da reinicialização da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Opções que exigem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para reiniciar mostrarão inicialmente apenas o valor alterado na coluna value. Após a reinicialização, o novo valor aparecerá nas colunas value e value_in_use.

Algumas opções requerem a reinicialização do servidor antes que o novo valor da configuração entre em vigor. Se você definir um novo valor e executar sp_configure antes de reiniciar o servidor, o novo valor aparecerá na coluna **value** das opções de configuração e não na coluna **value_in_use** . Após reinicializar o servidor, o novo valor aparecerá na coluna **value_in_use** .

As opções de autoconfiguração são aquelas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta de acordo com as necessidades do sistema. Na maioria dos casos, isso elimina a necessidade de definir os valores manualmente. Exemplos incluem a opção **máximo de threads de trabalho** e a opção conexões do usuário.

## <a name="configuration-options-table"></a>Tabela Opções de configuração
 A tabela a seguir lista todas as opções de configuração disponíveis, o intervalo de possíveis configurações e os valores padrão. As opções de configuração são marcadas com códigos de letras como segue:

- A = opções avançadas, que só devem ser alteradas por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado e que requerem que a definição de "mostrar opções avançadas" seja 1.

- RR = opções que requerem a reinicialização do [!INCLUDE[ssDE](../../includes/ssde-md.md)].

- RP = opções que exigem uma reinicialização do Mecanismo PolyBase.

- SC = opções autoconfiguráveis.

| Opções de configuração | Valor mínimo | Valor máximo | Padrão |
|--|--|--|--|
| [access check cache bucket count](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A) | 0 | 16384 | 0 |
| [access check cache quota](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A) | 0 | 2147483647 | 0 |
| [ad hoc distributed queries](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [Tempo limite de nova tentativa do limpador da ADR (min)](../../database-engine/configure-windows/adr-cleaner-retry-timeout-configuration-option.md)<br><br> Introduzido no SQL Server 2019 | 0 | 32767 | 15 |
| [Fator de pré-alocação de ADR](../../database-engine/configure-windows/adr-preallocation-factor-server-configuration-option.md)<br><br> Introduzido no SQL Server 2019 | 0 | 32767 | 4 |
| [affinity I/O mask](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md) (A, RR) | -2147483648 | 2147483647 | 0 |
| [affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md) (A) | -2147483648 | 2147483647 | 0 |
| [affinity64 I/O mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) (A, disponível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) | -2147483648 | 2147483647 | 0 |
| [affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) (A, RR), disponível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] | -2147483648 | 2147483647 | 0 |
| [Agent XPs](../../database-engine/configure-windows/agent-xps-server-configuration-option.md) (A) | 0 | 1 | 0<br /><br /> (É alterado para 1 quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado. O valor padrão será 0 se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for definido para inicialização automática durante a Instalação.) |
| [allow polybase export](../../database-engine/configure-windows/allow-polybase-export.md)<br/><br/> [!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)].| 0 | 1 | 0 |
| [allow updates](../../database-engine/configure-windows/allow-updates-server-configuration-option.md) (Obsoleta. Não use. Causará um erro durante a reconfiguração.) | 0 | 1 | 0 |
| [soft-NUMA automático desabilitado](soft-numa-sql-server.md) | 0 | 1 | 0 |
| [padrão de soma de verificação de backup](../../database-engine/configure-windows/backup-checksum-default.md) | 0 | 1 | 0 |
| [backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) | 0 | 1 | 0 |
| [blocked process threshold](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md) (A) | 5 | 86.400 | 0 |
| [c2 audit mode](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md) (A, RR) | 0 | 1 | 0 |
| [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) | 0 | 1 | 0 |
| [clr strict security](../../database-engine/configure-windows/clr-strict-security.md) (A) <br /> [!INCLUDE [sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]. | 0 | 1 | 0 |
| [column encryption enclave type ](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md) (A, RR) | 0 | 1 | 0 |
| [common criteria compliance enabled](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md) (A, RR) | 0 | 1 | 0 |
| [contained database authentication](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) | 0 | 1 | 0 |
| [cost threshold for parallelism](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A) | 0 | 32767 | 5 |
| [cross db ownership chaining](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md) | 0 | 1 | 0 |
| [cursor threshold](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md) (A) | -1 | 2147483647 | -1 |
| [Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [default full-text language](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) (A) | 0 | 2147483647 | 1046 |
| [idioma padrão](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) | 0 | 9999 | 0 |
| [default trace enabled](../../database-engine/configure-windows/default-trace-enabled-server-configuration-option.md) (A) | 0 | 1 | 1 |
| [disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [EKM provider enabled](../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md) | 0 | 1 | 0 |
| [external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md) (SC) (RR)<br /><br />[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]. | 0 | 1 | 0 |
| [filestream_access_level](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md) | 0 | 2 | 0 |
| [fill factor](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md) (A, RR) | 0 | 100 | 0 |
| [ft crawl bandwidth (max)](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A) | 0 | 32767 | 100 |
| [ft crawl bandwidth (min)](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A) | 0 | 32767 | 0 |
| [ft notify bandwidth (max)](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A) | 0 | 32767 | 100 |
| [ft notify bandwidth (min)](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A) | 0 | 32767 | 0 |
| [hadoop connectivity](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md) (RP)<br /><br />[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]. | 0 | 7 | 0 |
| [in-doubt xact resolution](../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md) (A) | 0 | 2 | 0 |
| [index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) (A, SC) | 704 | 2147483647 | 0 |
| [lightweight pooling](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) (A, RR) | 0 | 1 | 0 |
| [locks](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md) (A, RR, SC) | 5\.000 | 2147483647 | 0 |
| [max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) (A) | 0 | 32767 | 0 |
| [max full-text crawl range](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md) (A) | 0 | 256 | 4 |
| [max server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC) | 16 | 2147483647 | 2147483647 |
| [max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) | 0 | 2147483647 | 65536 |
| [max worker threads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) (A) | 128 | 32767<br /><br /> Recomendamos 1024 como o máximo para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits e 2048 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits. **Observação:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] foi a última versão disponível no sistema operacional de 32 bits. | 0<br /><br /> Zero configura automaticamente o número máximo de threads de trabalho de acordo com o número de processadores usando a fórmula (256 + ( *\<processors>* – 4) * 8) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits e (512 + ( *\<processors>* – 4) * 8) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits. **Observação:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] foi a última versão disponível no sistema operacional de 32 bits. |
| [media retention](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) (A, RR) | 0 | 365 | 0 |
| [min memory per query](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md) (A) | 512 | 2147483647 | 1024 |
| [min server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC) | 0 | 2147483647 | 0 |
| [gatilhos aninhados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) | 0 | 1 | 1 |
| [network packet size](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md) (A) | 512 | 32767 | 4096 |
| [Ole Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [open objects](../../database-engine/configure-windows/open-objects-server-configuration-option.md) (A, RR, obsoleto) | 0 | 2147483647 | 0 |
| [optimize for ad hoc workloads](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [PH_timeout](../../database-engine/configure-windows/ph-timeout-server-configuration-option.md) (A) | 1 | 3600 | 60 |
| [polybase enabled](../../relational-databases/polybase/polybase-installation.md#enable) (RR) <br/><br/>[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]| 0 | 1 | 0 |
| [polybase network encryption](../../relational-databases/polybase/polybase-installation.md#enable) | 0 | 1 | 1 |
| [precompute rank](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [priority boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) (A, RR) | 0 | 1 | 0 |
| [query governor cost limit](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) (A) | 0 | 2147483647 | 0 |
| [query wait](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md) (A) | -1 | 2147483647 | -1 |
| [recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md) (A, SC) | 0 | 32767 | 0 |
| [remote access](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md) (RR) | 0 | 1 | 1 |
| [remote admin connections](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md) | 0 | 1 | 0 |
| [arquivo morto de dados remotos](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md) | 0 | 1 | 0 |
| [tempo limite de logon remoto](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) | 0 | 2147483647 | 10 |
| [remote proc trans](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md) | 0 | 1 | 0 |
| [remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) | 0 | 2147483647 | 600 |
| [Replication XPs Option](../../database-engine/configure-windows/replication-xps-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR) | 0 | 1 | 0 |
| [server trigger recursion](../../database-engine/configure-windows/server-trigger-recursion-server-configuration-option.md) | 0 | 1 | 1 |
| [set working set size](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md) (A, RR, obsoleto) | 0 | 1 | 0 |
| [show advanced options](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md) | 0 | 1 | 0 |
| [SMO and DMO XPs](../../database-engine/configure-windows/smo-and-dmo-xps-server-configuration-option.md) (A) | 0 | 1 | 1 |
| [suppress recovery model errors](../../database-engine/configure-windows/suppress-recovery-model-errors-server-configuration-option.md) (A) <br/><br/>[!INCLUDE [asdbmi](../../includes/applies-to-version/_asdbmi.md)]| 0 | 1 | 0 |
| [tempdb metadata memory-optimized](../../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata) (A) <br/><br/> [!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)].| 0 | 1 | 0 |
| [transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) (A) | 0 | 1 | 0 |
| [two digit year cutoff](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) (A) | 1753 | 9999 | 2049 |
| [user connections](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md) (A, RR, SC) | 0 | 32767 | 0 |
| [opções de usuário](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) | 0 | 32767 | 0 |
| [xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md) (A) | 0 | 1 | 0 |  |

## <a name="see-also"></a>Confira também
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md) [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)


