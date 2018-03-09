---
title: "Restaurar banco de dados (página Opções) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0bdd383335126a36265bc917c1679dbd5ab0dc3e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="restore-database-options-page"></a>Restaurar o banco de dados (página Opções)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use a página **Opções** da caixa de diálogo **Restaurar Banco de Dados** para modificar o comportamento e o resultado da operação de restauração.  
  
 **Para usar o SQL Server Management Studio para restaurar o backup de um banco de dados**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Ao especificar uma tarefa de restauração por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondente que contenha as instruções RESTORE para essa operação de restauração. Para gerar o script, clique em **Script** e, em seguida, selecione um destino para o script. Para obter informações sobre a sintaxe RESTORE, veja [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
## <a name="options"></a>Opções  
  
### <a name="restore-options"></a>Opções de restauração  
 Para modificar os aspectos do comportamento da operação de restauração, use as opções do painel **Opções de restauração** .  
  
 **Substituir o banco de dados existente [WITH REPLACE]**  
 A operação de restauração substituirá os arquivos de qualquer banco de dados que estiver atualmente usando o nome do banco de dados que você está especificando no campo **Restaurar em**, na página [Geral](../../relational-databases/backup-restore/restore-database-general-page.md) , da caixa de diálogo **Restaurar Banco de Dados** . Os arquivos do banco de dados existente serão substituídos mesmo se você estiver restaurando os backups de um banco de dados diferente daquele com o nome existente. Selecionar esta opção equivale ao uso da opção REPLACE em uma declaração [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!CAUTION]  
>  Use esta opção somente cuidadosa consideração. Para obter mais informações, veja [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 **Preservar as configurações de replicação [WITH KEEP_REPLICATION]**  
 Preserva as configurações de replicação ao restaurar um banco de dados publicado em um servidor diferente daquele onde o banco de dados foi criado. Esta opção será relevante somente se o banco de dados foi replicado quando o backup foi criado.  
  
 Esta opção está disponível somente com a opção **Deixar o banco de dados pronto para uso revertendo as transações não confirmadas** (descrita posteriormente nesta tabela), que é equivalente à restauração de um backup com a opção RECOVERY.  
  
 Selecionar essa opção equivale a usar a opção KEEP_REPLICATION em uma instrução [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .  
  
 Para obter mais informações, veja [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
 **Acesso restrito ao banco de dados restaurado [WITH RESTRICTED_USER]**  
 Disponibiliza o banco de dados restaurado apenas para os membros do **db_owner**, **dbcreator**ou **sysadmin**.  
  
 A seleção dessa é sinônimo do uso da opção RESTRICTED_USER na instrução RESTORE.  
  
### <a name="recovery-state"></a>Estado de recuperação  
 Para determinar o estado do banco de dados após a operação de armazenamento, você deve selecionar uma das opções do painel **Estado de recuperação** .  
  
 **RESTORE WITH RECOVERY**  
 Recupera o banco de dados após a restauração do backup final marcado na grade **Conjuntos de backup a serem restaurados**na [página Geral](../../relational-databases/backup-restore/restore-database-general-page.md). Essa é a opção padrão e equivale à especificação de WITH RECOVERY em uma instrução [RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!NOTE]  
>  No modelo de recuperação completa ou modelo de recuperação bulk-logged, selecione esta opção somente se estiver restaurando todos os arquivos de logs agora.  
  
 **RESTORE WITH NORECOVERY**  
 Deixa o banco de dados no estado de restauração. Isto possibilita a restauração adicional de backups no caminho de recuperação atual. Para recuperar o banco de dados, será necessário realizar uma outra operação de restauração usando a opção RESTORE WITH RECOVERY (veja a opção anterior).  
  
 Esta opção equivale à especificação WITH NORECOVERY em uma declaração RESTORE.  
  
 Se selecionar esta opção, a opção **Preservar parâmetros de replicação** não estará disponível.  
  
 **RESTORE WITH STANDBY**  
 Deixa o banco de dados em estado de espera, no qual o banco de dados estará disponível para acesso de somente leitura limitado. Esta opção equivale à especificação WITH STANDBY em uma declaração RESTORE.  
  
 A escolha desta opção requer que você especifique o arquivo em espera na caixa de texto **Arquivo em espera** . O arquivo em espera permite que os efeitos da recuperação sejam desfeitos.  
  
 **Arquivo em espera**  
 Especifica um arquivo em espera. Você pode procurar pelo arquivo em espera ou digitar o nome do caminho diretamente na caixa de texto.  
  
### <a name="tail-log-backup"></a>Backup do final do log  
 Permite designar que um backup do final do log seja executado junto com a restauração do banco de dados.  
  
 **Fazer backup da parte final do log antes da restauração**  
 Marque essa caixa para designar que um backup do final do log deve ser executado.  
  
> [!NOTE]  
>  Se o momento específico selecionado na caixa de diálogo [Linha do Tempo do Backup](../../relational-databases/backup-restore/backup-timeline.md) exigir um backup do final do log, essa caixa será selecionada e não será possível editá-la.  
  
 **Arquivo de backup**  
 Especifica um arquivo de backup para o final do log. Você pode procurar pelo arquivo de backup ou inserir seu nome diretamente na caixa de texto.  
  
### <a name="server-connections"></a>Conexões do servidor  
 Permite fechar conexões de bancos de dados existentes.  
  
 **Encerre as conexões existentes**  
 As operações de restauração poderão falhar se houver conexões ativas com o banco de dados. Marque a opção **Fechar conexões existentes** para assegurar que todas as conexões ativas entre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o banco de dados sejam fechadas. Essa caixa de seleção define o banco de dados no modo de usuário único antes de executar as operações de restauração e define o banco de dados no modo de vários usuários ao concluir.  
  
### <a name="prompt"></a>Aviso  
 **Perguntar antes de restaurar cada backup**  
 Especifica que, após a restauração de cada backup, a caixa de diálogo **Continuar Restauração** será exibida para perguntar se você deseja continuar a sequência de restauração. Esta caixa de diálogo exibe o nome do conjunto de mídia seguinte (se conhecido) e o nome e a descrição do conjunto de backup seguinte.  
  
 Esta opção permite pausar a sequência da restauração após restaurar qualquer backup. Esta opção é muito importante quando precisar trocar as fitas para conjuntos de mídia diferentes, por exemplo, quando o servidor tiver apenas um dispositivo de fita. Quando você estiver pronto para continuar, clique em **OK**.  
  
 É possível interromper um sequência de restauração clicando em **Não**. O banco de dados ficará em estado de restauração. Se for conveniente, você pode continuar a sequência de restauração mais tarde começando pelo backup seguinte descrito na caixa de diálogo **Continuar com a Restauração** . O procedimento para restaurar o backup seguinte depende do mesmo conter dados ou backups de log de transações conforme a seguir:  
  
-   Se o backup seguinte for um backup completo ou diferencial, use a tarefa **Restaurar Banco de Dados** novamente.  
  
-   Se o próximo backup for um backup de arquivo, use a tarefa **Restaurar Arquivos e Grupos de Arquivos**. Para obter mais informações, veja [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md).  
  
-   Se o backup seguinte for um backup de log, use a tarefa **Restaurar Log de Transações** . Para obter informações sobre como retomar uma sequência de restauração restaurando um log de transações, veja [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurar um backup de um dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
