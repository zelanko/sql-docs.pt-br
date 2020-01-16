---
title: Atualizar o envio de logs para o SQL Server 2016 e mais recente
description: Aprenda a ordem apropriada para preservar sua solução de recuperação de desastre de envio de logs ao atualizar para o SQL Server 2016 e mais recente de uma versão anterior.
ms.custom: seo-lt-2019
ms.date: 02/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c3ebe7da68b057e9f84d2b83572a337ede278401
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258576"
---
# <a name="upgrading-log-shipping-to-sql-server-2016-transact-sql"></a>Atualização do envio de logs para SQL Server 2016 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ao atualizar de uma configuração de envio de logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma nova versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], um novo service pack do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma atualização cumulativa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a atualização de seus servidores de envio de log na ordem apropriada preservará sua solução de recuperação de desastres de envio de log.  
  
> [!NOTE]  
>  [A compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) foi introduzida no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]. Uma configuração de envio de logs atualizada usa a opção de configuração no nível do servidor de **compactação de backup padrão** para controlar se a compactação será utilizada para os arquivos de backup de log de transações. O comportamento de compactação de backups de log pode ser especificado para cada configuração de envio de logs. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
 **Neste tópico:**  
  
-   [Pré-requisitos](#Prerequisites)  
  
-   [Proteja os dados antes da atualização](#ProtectData)  
  
-   [Atualizando a instância do servidor monitor](#UpgradeMonitor)  
  
-   [Atualização das instâncias do servidor secundário](#UpgradeSecondaries)  
  
-   [Atualização da instância primária](#UpgradePrimary)  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
 Antes de começar, examine as seguintes informações importantes:  
  
-   [Atualizações compatíveis de versão e edição](../../database-engine/install-windows/supported-version-and-edition-upgrades.md): Verifique se você pode atualizar para o SQL Server 2016 de sua versão do sistema operacional Windows e da versão do SQL Server. Por exemplo, não é possível atualizar diretamente de uma instância do SQL Server 2005 para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   [Escolher um método de atualização do mecanismo de banco de dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selecione o método e as etapas de atualização apropriados com base em sua análise de atualizações de versão e de edição com suporte e também com base em outros componentes instalados em seu ambiente a fim de atualizar os componentes na ordem correta.  
  
-   [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): Analise as notas de versão e os problemas conhecidos da atualização, a lista de verificação pré-atualização, e desenvolva e teste o plano de atualização.  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md):  Analise os requisitos de software para a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se for necessário um software adicional, instale-o em cada nó antes de começar o processo de atualização para minimizar qualquer tempo de inatividade.  
  
##  <a name="ProtectData"></a> Proteja os dados antes da atualização  
 Como uma prática recomendada, sugerimos que você proteja seus dados antes de uma atualização de envio de logs.  
  
 **Para proteger os dados**  
  
1.  Execute um backup completo de todos os bancos de dados primários.  
  
     Para obter mais informações, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Execute o comando [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) em todos os bancos de dados primários.  
  
> [!IMPORTANT]  
>  Verifique se você tem espaço suficiente no servidor primário para manter as cópias de backup do log durante toda a atualização dos secundários.  Se estiver realizando o failover para um secundário, essa mesma preocupação se aplicará ao secundário (o novo primário).  
  
##  <a name="UpgradeMonitor"></a> Atualização da instância do servidor monitor (opcional)  
 Se existir uma instância do servidor monitor, ela poderá ser atualizada em qualquer momento. No entanto, você não precisa atualizar o servidor de monitor opcional ao atualizar os servidores primário e secundário.  
  
 Enquanto o servidor monitor está sendo atualizado, a configuração de envio de logs continua funcionando, mas seu status não será registrado nas tabelas do monitor. Qualquer alerta que tenha sido configurado não será disparado, enquanto o servidor monitor estiver sendo atualizado. Após a atualização, você poderá atualizar as informações nas tabelas do monitor executando o procedimento armazenado do sistema [sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md).   Para obter mais informações sobre um servidor de monitor, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
##  <a name="UpgradeSecondaries"></a> Atualização das instâncias do servidor secundário  
 O processo de atualização envolve a atualização das instâncias do servidor secundário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] antes de atualizar a instância de servidor primário. Sempre atualize primeiro a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] secundário. O envio de logs continua ao longo do processo de atualização, pois as instâncias dos servidores secundários atualizados continuam restaurando os backups de log da instância do servidor primário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se o servidor primário for atualizado antes da instância do servidor secundário, o envio de logs falhará, pois um backup criado em uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser restaurado em uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode atualizar as instâncias secundárias de forma simultânea ou em série, mas todas as instâncias secundárias devem ser atualizadas antes de atualizar a instância primária, a fim de evitar uma falha de envio de logs.  
  
 Enquanto uma instância do servidor secundário estiver sendo atualizada, os trabalhos de cópia e restauração de envio de logs não serão executados. Isso significa que os backups de log de transações não restaurados serão acumulados no primário, e você precisará ter espaço suficiente para manter esses backups não restaurados. A quantidade de acumulação dependerá da frequência de backups agendados na instância do servidor primário e da sequência na qual você atualiza as instâncias secundárias. Além disso, se um servidor monitor separado tiver sido configurado, alertas poderão ser gerados indicando que restaurações não foram realizadas por um período mais longo do que o intervalo configurado.  
  
 Assim que as instâncias do servidor secundário forem atualizadas, os trabalhos de agentes de envio de logs serão retomados e continuarão a copiar e a restaurar os backups de log da instância de servidor primário para as instâncias do servidor secundário. A quantidade de tempo necessário para as instâncias do servidor secundário atualizarem o banco de dados secundário varia, dependendo do tempo gasto para atualizar a instância do servidor secundário e da frequência dos backups no servidor primário.  
  
> [!NOTE]  
>  Durante a atualização do servidor, o próprio banco de dados secundário não será atualizado para um banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Ele será atualizado apenas se for colocado online por meio de um failover do banco de dados de logs enviados. Em teoria, essa condição pode persistir indefinidamente. O tempo necessário para atualizar os metadados do banco de dados quando um failover é iniciado é pequeno.  
  
> [!IMPORTANT]  
>  A opção RESTORE WITH STANDBY não tem suporte para um banco de dados que requer atualização. Se um banco de dados secundário atualizado foi configurado usando RESTORE WITH STANDBY, os logs de transação já não poderão ser restaurados depois da atualização. Para retomar o envio de logs no banco de dados secundário, você precisará configurar o envio de logs novamente no servidor em espera. Para obter mais informações sobre a opção STANDBY, veja [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
  
##  <a name="UpgradePrimary"></a> Atualizando a instância do servidor primário  
 Como o envio de log é basicamente uma solução de recuperação de desastres, o cenário mais simples e mais comum é atualizar a instância primária no local, e o banco de dados simplesmente fica indisponível durante essa atualização. Quando o servidor é atualizado, o banco de dados fica online automaticamente, o que faz com que ele seja atualizado. Depois que o banco de dados é atualizado, os trabalhos de envio de logs são retomados.  
  
> [!NOTE]  
>  O envio de log também dá suporte à opção [Executar failover para um secundário de envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) e, opcionalmente, [Alterar funções entre servidores de envio de log primários e secundários &#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md). No entanto, como o envio de logs raramente é configurado como uma solução de alta disponibilidade (opções mais recentes são muito mais robustas), o failover geralmente não reduzirá o tempo de inatividade, pois os objetos de banco de dados do sistema não serão sincronizados, e permitir que os clientes localizem e se conectem facilmente a um secundário promovido pode ser um trabalho difícil.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Configurar o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)   
 [Monitorar o envio de logs &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)   
 [Tabelas de envio de log e procedimentos armazenados](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
