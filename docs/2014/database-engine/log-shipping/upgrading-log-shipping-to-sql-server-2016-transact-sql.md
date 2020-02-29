---
title: Atualizar o envio de logs para SQL Server 2014 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 773426ed91039ee4c0c6fd224547e44102f9846b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175410"
---
# <a name="upgrade-log-shipping-to-sql-server-2014-transact-sql"></a>Atualizar o envio de logs para o SQL Server 2014 (Transact-SQL)
  É possível preservar as configurações de envio de logs ao atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este tópico descreve cenários alternativos e práticas recomendadas para atualizar uma configuração de envio de logs.

> [!NOTE]
>  [A compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) foi introduzida no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]. Uma configuração de envio de logs atualizada usa a opção de configuração no nível do servidor de **compactação de backup padrão** para controlar se a compactação será utilizada para os arquivos de backup de log de transações. O comportamento de compactação de backups de log pode ser especificado para cada configuração de envio de logs. Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).


##  <a name="ProtectData"></a> Proteja os dados antes da atualização
 Como uma prática recomendada, sugerimos que você proteja seus dados antes de uma atualização de envio de logs.

 **Para proteger os dados**

1.  Execute um backup completo de todos os bancos de dados primários.

     Para obter mais informações, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).

2.  Execute o comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) em todos os bancos de dados primários.

##  <a name="UpgradeMonitor"></a>Atualizando a instância do servidor monitor
 Se existir uma instância do servidor monitor, ela poderá ser atualizada em qualquer momento.

 Enquanto o servidor monitor está sendo atualizado, a configuração de envio de logs continua funcionando, mas seu status não será registrado nas tabelas do monitor. Qualquer alerta que tenha sido configurado não será disparado, enquanto o servidor monitor estiver sendo atualizado. Após a atualização, você poderá atualizar as informações nas tabelas do monitor executando o procedimento armazenado do sistema [sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql).

##  <a name="UpgradeSingleSecondary"></a>Atualizando configurações de envio de logs com um único servidor secundário
 O processo de atualização descrito nesta seção assume uma configuração que consiste no servidor primário e somente em um servidor secundário. Essa configuração é representada na ilustração seguinte que mostra uma instância de servidor primário, A, e uma única instância de servidor secundário, B.

 ![Um servidor secundário e nenhum servidor monitor](../media/ls-2-wayconfig-nomonitor.gif "Um servidor secundário e nenhum servidor monitor")

 Para obter informações sobre como atualizar vários servidores secundários, consulte [Atualizando várias instâncias do servidor secundário](#MultipleSecondaries), posteriormente neste tópico.
 

###  <a name="UpgradeSecondary"></a>Atualizando a instância do servidor secundário
 O processo de atualização envolve a atualização das instâncias do servidor secundário de uma configuração de envio de logs do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] antes de atualizar a instância de servidor primário. Sempre atualize primeiro a instância do servidor secundário. Se o servidor primário fosse atualizado antes de um secundário, o envio de logs falharia porque um backup criado em uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser restaurado em uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

 O envio de logs continua ao longo do processo de atualização porque os servidores secundários atualizados continuam restaurando os backups de log do servidor primário do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior. O processo para atualizar as instâncias do servidor secundário depende em parte se a configuração de envio de logs possui vários servidores secundários. Para obter mais informações, consulte [Atualizando várias instâncias do servidor secundário](#MultipleSecondaries)posteriormente neste tópico.

 Enquanto a instância do servidor secundário estiver sendo atualizada, os trabalhos de cópia e restauração de envio de logs não serão executados, portanto, os backups de log de transações não restaurados serão acumulados. A quantidade de acumulação dependerá da frequência de backups agendados no servidor primário. Além disso, se um servidor monitor separado tiver sido configurado, alertas poderão ser gerados indicando que restaurações não foram realizadas por um período mais longo do que o intervalo configurado.

 Depois que o servidor secundário tiver sido atualizado, os trabalhos dos agentes de envio de logs serão retomados e retomarão a copiar e a restaurar os backups de log da instância do servidor primário, o servidor A. O tempo necessário para o servidor secundário atualizar o banco de dados secundário varia, dependendo do tempo necessário para atualizar o servidor secundário e da frequência dos backups no servidor primário.

> [!NOTE]
>  Durante a atualização do servidor, o banco de dados secundário não será atualizado para um banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Ele só será atualizado se estiver online.

> [!IMPORTANT]
>  A opção RESTORE WITH STANDBY não tem suporte para um banco de dados que requer atualização. Se um banco de dados secundário atualizado foi configurado usando RESTORE WITH STANDBY, os logs de transação já não poderão ser restaurados depois da atualização. Para retomar o envio de logs no banco de dados secundário, você precisará configurar o envio de logs novamente no servidor em espera. Para obter mais informações sobre a opção de espera, consulte [argumentos de restore &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).

###  <a name="UpgradePrimary"></a> Atualizando a instância do servidor primário
 Ao planejar uma atualização, uma consideração importante é a quantidade de tempo que seu banco de dados ficará indisponível. O cenário de atualização mais simples indisponibiliza o banco de dados durante a atualização do servidor primário (cenário 1, abaixo).

 Por meio de um processo de atualização mais complicado, você poderá maximizar a disponibilidade do seu banco de dados efetuando failover do servidor primário do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior para um servidor secundário do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] antes de atualizar o servidor primário original (cenário 2, abaixo). Há duas variantes do cenário de failover. Você pode alternar novamente para o servidor primário original e manter a configuração original de envio de logs. Alternativamente, você poderá remover a configuração original de envio de logs antes de atualizar o servidor primário original e posteriormente criar uma nova configuração usando o novo servidor primário. Esta seção descreve os dois cenários.

> [!IMPORTANT]
>  Atualize a instância do servidor secundário antes de atualizar a instância de servidor primário. Para obter mais informações, consulte [Atualizando a instância do servidor secundário](#UpgradeSecondary)anteriormente neste tópico.


####  <a name="Scenario1"></a>Cenário 1: atualizar a instância do servidor primário sem failover
 Este é o cenário mais simples, entretanto ele gera mais tempo de inatividade do que o cenário que usa failover. A instância do servidor primário é simplesmente atualizada e o banco de dados fica indisponível durante esta atualização.

 Quando o servidor é atualizado, o banco de dados fica online automaticamente, o que faz com que ele seja atualizado. Depois que o banco de dados é atualizado, os trabalhos de envio de logs são retomados.

#### <a name="scenario-2-upgrade-primary-server-instance-with-failover"></a>Cenário 2: Atualização da instância do servidor primário com failover
 Este cenário maximiza a disponibilidade e minimiza tempo de inatividade. Ele utiliza um failover controlado para a instância do servidor secundário, o que mantém o banco de dados disponível enquanto a instância do servidor primário original é atualizada. O tempo de inatividade é limitado ao tempo relativamente curto do failover, em vez do tempo necessário para atualizar a instância do servidor primário.

 A atualização da instância do servidor primário com failover envolve três procedimentos gerais: a execução de um failover controlado para o servidor secundário, a atualização da instância do servidor primário original para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]e a configuração de envio de logs em uma instância do servidor primário do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esses procedimentos são descritos nesta seção.

> [!IMPORTANT]
>  Se você planeja ter a instância do servidor secundário como a nova instância do servidor primário, precisará remover a configuração de envio de logs. O envio de logs precisará ser reconfigurado do novo primário para o novo secundário, depois que a instância do servidor primário original tiver sido atualizada. Para obter mais informações, consulte [remover o envio de logs &#40;SQL Server&#41;](remove-log-shipping-sql-server.md).


#####  <a name="Procedure1"></a>Procedimento 1: executar um failover controlado para o servidor secundário
 Failover controlado no servidor secundário:

1.  Execute manualmente um [backup da parte final do log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) do log de transações no banco de dados primário ESPECIFICANDO with NORECOVERY. Esse backup de log captura quaisquer registros de log ainda sem backup e coloca o banco de dados offline. Observe que enquanto o banco de dados estiver offline, o trabalho de backup de envio de logs falhará.

     O exemplo seguinte cria um backup da parte final do log do banco de dados do `AdventureWorks` no servidor primário. O arquivo de backup é nomeado como `Failover_AW_20080315.trn`:

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Failover_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

     Recomendamos que você use uma convenção de nomeação de arquivo distinta para diferenciar o arquivo de backup criado manualmente dos arquivos de backup criados pelo trabalho de backup de envio de logs.

2.  No servidor secundário:

    1.  Assegure-se de que todos os backups obtidos automaticamente pelo backup de envio de logs tenham sido aplicados. Para verificar quais trabalhos de backup foram aplicados, use o procedimento armazenado do sistema [sp_help_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql) no servidor monitor ou nos servidores primários e secundários. O mesmo arquivo deve ser listado nas colunas **last_backup_file**, **last_copied_file**e **last_restored_file** . Se alguns dos arquivos de backup não foram copiados e restaurados, chame manualmente os trabalhos de cópia e restauração do agente para a configuração de envio de logs.

         Para obter informações sobre como iniciar um trabalho, consulte [Start a Job](../../ssms/agent/start-a-job.md).

    2.  Copie o arquivo de backup de log final que você criou na etapa 1 do compartilhamento de arquivo para o local que é usado pelo envio de logs no servidor secundário.

    3.  Restaure o backup do final do log especificando WITH RECOVERY para colocar o banco de dados online. Como resultado de ser colocado online, o banco de dados será atualizado para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

         O exemplo seguinte restaura o backup da parte final do log do banco de dados do `AdventureWorks` no banco de dados secundário. O exemplo usa a opção de WITH RECOVERY que coloca o banco de dados online:

        ```
        RESTORE LOG AdventureWorks 
          FROM DISK = N'c:\logshipping\Failover_AW_20080315.trn' 
           WITH RECOVERY;
        GO
        ```

        > [!NOTE]
        >  Para uma configuração que contém mais de um servidor secundário, há considerações adicionais. Para obter mais informações, consulte [Atualizando várias instâncias do servidor secundário](#MultipleSecondaries)posteriormente neste tópico.

    4.  Efetue o failover do banco de dados redirecionando os clientes do servidor primário original (servidor A) para o servidor secundário online (servidor B).

    5.  Cuidado para que o log de transações do banco de dados secundário não seja preenchido enquanto o banco de dados estiver online. Para impedir que o log de transações seja preenchido, talvez seja necessário fazer seu backup. Nesse caso, recomendamos que você faça seu backup em um local compartilhado, um *compartilhamento de backup*, para tornar os backups disponíveis para restauração em outra instância do servidor.

#####  <a name="Procedure2"></a>Procedimento 2: atualizar a instância do servidor primário original para[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 Depois de atualizar a instância do servidor primário original para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados ainda estará offline e no formato.

#####  <a name="Procedure3"></a>Procedimento 3: configurar o envio de logs em[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 O restante do processo de atualização dependerá de o envio de logs ainda estar configurado, como a seguir:

-   Se você manteve a configuração de envio de logs do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ou posterior, alterne novamente para a instância do servidor primário original. Para obter mais informações, consulte [Para alternar novamente para a instância do servidor primário original](#SwitchToOrigPrimary)posteriormente nessa seção.

-   Se você tiver removido a configuração de envio de logs antes de efetuar o failover, crie uma nova configuração de envio de logs em que a instância do servidor secundário original seja a nova instância do servidor primário. Para obter mais informações, consulte [Para manter a instância do servidor secundário antiga como a nova instância do servidor primário](#KeepOldSecondaryAsNewPrimary)posteriormente nessa seção.

######  <a name="SwitchToOrigPrimary"></a>Para voltar para a instância do servidor primário original

1.  No servidor primário provisório (servidor B), faça backup do final do log usando WITH NORECOVERY para fazer backup da parte final do log e colocar o banco de dados offline. O backup da parte final do log é nomeado como `Switchback_AW_20080315.trn`.Por exemplo:

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Switchback_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

2.  Se alguns backups de log de transações forem feitos no banco de dados primário provisório, além do backup da parte final que você criou na etapa 1, restaure aqueles backups de log usando WITH NORECOVERY para o banco de dados offline no servidor primário original (servidor A). O banco de dados será atualizado para o formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] quando o primeiro backup de log for restaurado.

3.  Restaure o backup do final do log, `Switchback_AW_20080315.trn`, no banco de dados primário original (no servidor A) usando o WITH RECOVERY para colocar o banco de dados online.

4.  Efetue o failover novamente no banco de dados primário original (no servidor A) redirecionando os clientes para o servidor secundário online do servidor primário original.

 Depois que o banco de dados ficar online, a configuração do envio de logs original retomará.

######  <a name="KeepOldSecondaryAsNewPrimary"></a>Para manter a instância antiga do servidor secundário como a nova instância do servidor primário
 Estabeleça uma nova configuração de envio de logs utilizando a instância do servidor secundário antiga, B, como o servidor primário e a instância do servidor primário antiga, A, como o novo servidor secundário, como a seguir:

> [!IMPORTANT]
>  A configuração de envio de logs antiga deve ter sido removida do servidor primário original no início do processo antes do backup manual do log de transações que colocou o banco de dados offline.

1.  Para evitar a realização de um backup completo e restauração do banco de dados no novo servidor secundário (servidor A), aplique os backups de log do novo banco de dados primário no novo banco de dados secundário. Na configuração de exemplo, isto envolve a restauração dos backups de log efetuados no servidor B para o banco de dados do servidor A.

2.  Faça backup do log do novo banco de dados primário (no servidor B).

3.  Restaure os backups de log para a nova instância do servidor secundário (servidor A) usando WITH NORECOVERY. A primeira operação de restauração atualizará o banco de dados para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

4.  Configure o envio de logs com o servidor secundário anterior (servidor B) como a instância do servidor primário.

    > [!IMPORTANT]
    >  Se você usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], especifique se o banco de dados secundário já está inicializado.

     Para obter mais informações, consulte [Configurar o envio de logs &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).

5.  Efetue o failover do banco de dados redirecionando os clientes do servidor primário original (servidor A) para o servidor secundário online (servidor B).

    > [!IMPORTANT]
    >  Quando você efetuar o failover para um novo banco de dados primário, deverá assegurar-se de que os metadados estejam consistentes com os metadados do banco de dados primário original. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).

##  <a name="MultipleSecondaries"></a>Atualizando várias instâncias de servidor secundário
 Essa configuração é representada na ilustração seguinte que mostra uma instância do servidor primário, A, e duas instâncias do servidor secundário, B e C.

 ![Dois servidores secundários e nenhum servidor monitor](../media/ls-3-wayconfig-nomonitor.gif "Dois servidores secundários e nenhum servidor monitor")

 Esta seção discute como atualizar usando um failover e alternando de volta para o servidor primário original. O processo de atualização da instância primária com failover torna-se mais complexo quando há várias instâncias do servidor secundário. No procedimento seguinte, depois que todos os servidores secundários forem atualizados, ocorrerá o failover do servidor primário para um dos bancos de dados secundários atualizados. O servidor primário original será atualizado e ocorrerá o failover do envio de logs novamente para ele.

> [!IMPORTANT]
>  Sempre atualize todas as instâncias do servidor secundário antes de atualizar o servidor primário.

 **Para atualizar usando um failover e alternando de volta para o servidor primário original**

1.  Atualize todas as instâncias do servidor secundário (servidores B e C).

2.  Obtenha a parte final do log de transações do banco de dados primário (no servidor A) e coloque o banco de dados offline efetuando o backup do log de transações por meio do WITH NORECOVERY.

3.  No servidor secundário para o qual você planeja efetuar failover (servidor B) coloque o banco de dados secundário online restaurando o backup de log por meio do WITH RECOVERY.

4.  Em todos os outros servidores secundários (servidor C), deixe o banco de dados secundário offline restaurando o backup de log por meio do WITH NORECOVERY.

    > [!NOTE]
    >  Os trabalhos de cópia e restauração de envio de logs serão executados nos servidores secundários, mas os trabalhos não serão bem-sucedidos porque novos arquivos de backup de log não serão colocados no compartilhamento de backup.

5.  Efetue o failover do banco de dados redirecionando os clientes do servidor primário original (servidor A) para o servidor secundário online (servidor B). O banco de dados online se tornará um servidor primário provisório, mantendo o banco de dados disponível enquanto o servidor primário original estiver offline (servidor A).

6.  Atualize o servidor primário original (servidor A).

7.  No banco de dados no qual você fez o failover – o banco de dados primário provisório (no servidor B), faça backup manualmente do log de transações usando WITH NORECOVERY. Isso coloca o banco de dados offline.

8.  Restaure todos os backups de log de transações que você criou no banco de dados primário provisório (no servidor B) para todos os outros bancos de dados secundários (no servidor C) com o WITH NORECOVERY. Isso permite que o envio de logs continue do banco de dados primário original depois de sua atualização, sem exigir uma restauração completa em cada banco de dados secundário.

9. Restaure o log de transações do servidor primário provisório (servidor B) para o banco de dados primário original (no servidor A) por meio do WITH RECOVERY.

##  <a name="Redeploying"></a>Reimplantando o envio de logs
 Se você não desejar migrar sua configuração de envio de logs usando um dos procedimentos citados acima, é possível reimplantar o envio de logs do zero, reinicializando seu banco de dados secundário com um backup completo e com a restauração do banco de dados primário. Essa pode ser uma boa opção, se você tiver um banco de dados pequeno ou se uma alta disponibilidade não for crucial durante o procedimento de atualização.

 Para obter informações sobre como habilitar o envio de logs, consulte [Configurar o envio de logs &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).

## <a name="see-also"></a>Consulte Também
 [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) [aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md) [tabelas de envio de logs e procedimentos armazenados](log-shipping-tables-and-stored-procedures.md)
