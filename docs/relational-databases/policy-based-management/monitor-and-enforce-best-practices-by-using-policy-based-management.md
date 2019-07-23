---
title: Monitorar e impor as melhores práticas usando o gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d261f84f23131ab9bce11081e1c9d6d1c8dda8d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087091"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Gerenciamento Baseado em Políticas permite que você monitore as práticas recomendadas para o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um conjunto de arquivos de políticas que você pode importar como políticas de práticas recomendadas e avaliar essas políticas em relação a um conjunto de destino que inclui instâncias, objetos de instância, bancos de dados ou objetos de bancos de dados. Avalie as políticas manualmente, defina-as para avaliar um conjunto de destino de acordo para um agendamento ou defina-as para avaliar um conjunto de destino de acordo com um evento. Para obter mais informações sobre o gerenciamento baseado em políticas, veja [Administrar servidores usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="policy-and-rules-for-database-engine"></a>Política e regras para o mecanismo de banco de dados  
 A tabela a seguir lista as políticas que são incluídas com a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e informações sobre as regras de práticas recomendadas que cada política avalia. As políticas são armazenadas como arquivos XML e são importadas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como importar políticas, consulte [Importar uma política de gerenciamento baseado em políticas](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md).  
  
|Nome de política|Regra de prática recomendada|  
|-----------------|------------------------|  
|Algoritmo de Criptografia de Chave Assimétrica|[Intensidade da criptografia de chaves assimétricas](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|Local do Arquivo de Backup e Dados|[Arquivos de backup devem estar em dispositivos separados dos arquivos de banco de dados](https://msdn.microsoft.com/library/7039bebb-1f25-4cf3-81f1-393dfb78da12)|  
|Local do Arquivo de Dados e Log|[Colocar arquivos de dados e de log em unidades separadas](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|Fechamento Automático do Banco de Dados|[Definir a opção do banco de dados AUTO_CLOSE como OFF](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|Redução Automática de Banco de Dados|[Definir a opção do banco de dados AUTO_SHRINK como OFF](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|Ordenação de banco de dados|[Definir a ordenação de bancos de dados definidos pelo usuário para corresponder aos dos bancos de dados mestre e modelo](https://msdn.microsoft.com/library/c686446f-dae1-4b05-a3df-837b3422988d)|  
|Verificação de Página de Banco de Dados|[Definir a opção do banco de dados PAGE_VERIFY como CHECKSUM](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|Status da Página de Banco de Dados|[Verificar a integridade do banco de dados com páginas suspeitas](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|Permissões de Convidado|[Permissões de convidado em bancos de dados de usuários](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|Data do Último Backup bem-sucedido|[Backup desatualizado](../../relational-databases/policy-based-management/outdated-backup.md)|  
|Public Não Recebeu Permissões de Servidor|[Permissões públicas de servidor](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|Sobreposição de Máscara de Afinidade de 64 bits do SQL Server|[Corrigir a sobreposição de máscara de afinidade e máscara de afinidade de entrada e saída](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|Máscara de Afinidade do SQL Server|[Manter o valor padrão da máscara de afinidade](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|Limite de Processo Bloqueado do SQL Server|[Aumentar ou desabilitar o limite de processo bloqueado](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|Rastreamento Padrão do SQL Server|[Arquivos de log de rastreamento padrão desabilitados](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|Bloqueios Dinâmicos do SQL Server|[Manutenção do valor padrão da opção configuração de bloqueios](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|Lightweight Pooling do SQL Server|[Desabilitar o Lightweight Pooling](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|Modo de Logon do SQL Server|[Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md)|  
|Grau Máx de Paralelismo do SQL Server|[Definir o grau máximo da opção de paralelismo para obtenção do desempenho ideal](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|Máx. de Threads de Trabalho do SQL Server para SQL Server 2000 de 32 bits|[Verificar a configuração máxima de threads de trabalho](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Máx de Threads de Trabalho do SQL Server para SQL Server 2000 de 64 bits|[Verificar a configuração máxima de threads de trabalho](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Máx. de Threads de Trabalho do SQL Server para o SQL Server 2005 e posterior|[Verificar a configuração máxima de threads de trabalho](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|Tamanho do Pacote de Rede do SQL Server|[O tamanho do pacote de rede não dever exceder 8060 bytes](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|Expiração de Senha do SQL Server|[Vencimento da senha de logon do SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|Política de Senha do SQL Server|[Nível de segurança da senha de logon do SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|Criptografia de Chave Simétrica para Bancos de Dados de Usuário|[Chaves simétricas em bancos de dados de usuários](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|Chave Simétrica para Banco de Dados Mestre|[Chaves simétricas em bancos de dados do sistema](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Chave Simétrica para Bancos de Dados do Sistema|[Chaves simétricas em bancos de dados do sistema](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Banco de Dados Confiável|[Bit confiável](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Erro de Corrupção do Recurso de Disco de Cluster do Log de Eventos do Windows|[Detectar problemas do adaptador de host SCSI](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Erro de Controle de Driver do Dispositivo do Log de Eventos do Windows|[Erro de controle de driver de dispositivo](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Erro de Dispositivo Não Pronto do Log de Eventos do Windows|[Erro de Dispositivo Não Pronto](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Erro de Solicitação de I_O com Falha do Log de Eventos do Windows|[Detect Failed Input and Output Requests](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|Aviso de Atraso de I_O do Log de Eventos do Windows|[Verificar o subsistema de entrada e saída de disco para problemas de atraso de E/S](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Erro de I_O do Log de Eventos do Windows durante Falha de Página de Hardware|[Erro de entrada e saída durante falha de página física](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Erro de Repetição de Leitura do Log de Eventos do Windows|[Verificar o subsistema de entrada e saída de disco para problemas de repetição de leitura](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Erro de Tempo Limite de I_O do Sistema de Armazenamento do Log de Eventos do Windows|[Tempo limite de entrada e saída dd sistema de armazenamento](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Erro de Falha do Sistema do Log de Eventos do Windows|[Falhas inesperadas do sistema](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com facetas do Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  
