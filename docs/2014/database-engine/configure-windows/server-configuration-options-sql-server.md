---
title: Opções de configuração de servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a903a3246b8a91a8ff0b42862b7bbf4046497c3c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088706"
---
# <a name="server-configuration-options-sql-server"></a>Opções de configuração do servidor (SQL Server)
  É possível gerenciar e otimizar recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de opções de configuração usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o procedimento armazenado do sistema sp_configure. As opções de configuração de servidor usadas com mais frequência estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; todas as opções de configuração podem ser acessadas pelo sp_configure. Avalie atentamente os efeitos dessas opções no sistema antes de defini-las. Para obter mais informações, veja [Exibir ou alterar propriedades de servidor &#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md).  
  
> [!IMPORTANT]  
>  As opções avançadas só devem ser alteradas por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="categories-of-configuration-options"></a>Categorias de opções de configuração  
 As opções de configuração passam a vigorar:  
  
-   Imediatamente após a definição da opção e da emissão da instrução RECONFIGURE (ou, em alguns casos, RECONFIGURE WITH OVERRIDE).  
  
     -ou-  
  
-   Após a execução das ações anteriores e da reinicialização da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Opções que exigem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para reiniciar mostrarão inicialmente apenas o valor alterado na coluna value. Após a reinicialização, o novo valor aparecerá nas colunas value e value_in_use.  
  
 Algumas opções requerem a reinicialização do servidor antes que o novo valor da configuração entre em vigor. Se você definir um novo valor e executar sp_configure antes de reiniciar o servidor, o novo valor aparecerá na coluna value das opções de configuração e não na coluna value_in_use. Após reinicializar o servidor, o valor novo aparecerá na coluna value_in_use.  
  
 As opções de autoconfiguração são aquelas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta de acordo com as necessidades do sistema. Na maioria dos casos, isso elimina a necessidade de definir os valores manualmente. Alguns exemplos são as opções min server memory e max server memory e a opção user connections.  
  
## <a name="configuration-options-table"></a>Tabela Opções de configuração  
 A tabela a seguir lista todas as opções de configuração disponíveis, o intervalo de possíveis configurações e os valores padrão. As opções de configuração são marcadas com códigos de letras como segue:  
  
-   A = opções avançadas, que só devem ser alteradas por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e requerem a definição de show advanced options como 1.  
  
-   RR = opções que requerem a reinicialização do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   SC = opções autoconfiguráveis.  
  
    |Opções de configuração|Valor mínimo|Valor máximo|Padrão|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](affinity64-input-output-mask-server-configuration-option.md) (A, disponível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|-2147483648|2147483647|0|  
    |[affinity mask](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) (A, RR), disponível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> (É alterado para 1 quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado. O valor padrão será 0 se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for definido para inicialização automática durante a Instalação.)|  
    |[allow updates](allow-updates-server-configuration-option.md) (Obsoleta. Não use. Causará um erro durante a reconfiguração.)|0|1|0|  
    |[padrão de soma de verificação de backup](../backup-checksum-default.md)|0|1|0|  
    |[backup compression default](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[blocked process threshold](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[common criteria compliance enabled](common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[contained database authentication](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[cost threshold for parallelism](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1046|  
    |[idioma padrão](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth (max), veja [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min), veja [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max), veja [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min), veja [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[index create memory](configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[in-doubt xact resolution](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[locks](configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[max degree of parallelism](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> (Recomendamos 1024 como o máximo para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits e 2048 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits.)|0<br /><br /> Zero configura automaticamente o número máximo de threads de trabalho de acordo com o número de processadores, usando a fórmula (256+(*\<processors>* -4) * 8) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits e o dobro disso para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits.|  
    |[media retention](configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[min memory per query](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[gatilhos aninhados](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](open-objects-server-configuration-option.md) (A, RR, obsoleto)|0|2147483647|0|  
    |[optimize for ad hoc workloads](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[precompute rank](precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[query governor cost limit](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[remote access](configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[tempo limite de logon remoto](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Replication XPs Option](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](set-working-set-size-server-configuration-option.md) (A, RR, obsoleto)|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO and DMO XPs](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[two digit year cutoff](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[opções de usuário](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
