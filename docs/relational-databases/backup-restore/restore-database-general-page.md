---
title: "Restaurar banco de dados (página Geral) | Microsoft Docs"
ms.custom: 
ms.date: 07/01/2016
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
- sql13.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db20fb80e64e3ffecee629dd5fc9310755ff58b0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="restore-database-general-page"></a>Restaurar banco de dados (página Geral)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a página **Geral** para especificar informações sobre os bancos de dados de origem e destino para uma operação de restauração de banco de dados.  
    
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Ao especificar uma tarefa de restauração usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) correspondente clicando em **Script** e selecionando um destino para o script.  
  
## <a name="permissions"></a>Permissões  
 Se o banco de dados que está sendo restaurado não existir, o usuário deverá ter permissões CREATE DATABASE para poder executar o comando RESTORE. Se o banco de dados existir, as permissões RESTORE assumirão como padrão os membros das funções de servidor fixas **sysadmin** e **dbcreator** , e o proprietário (**dbo**) do banco de dados.  
  
 As permissões RESTORE são concedidas a funções nas quais as informações de associação estão sempre disponíveis para o servidor. Como a associação da função de banco de dados fixa pode ser verificada apenas quando o banco de dados está acessível e não danificado, o que nem sempre é o caso quando RESTORE é executado, os membros da função de banco de dados fixa **db_owner** não têm permissões RESTORE.  
  
 A restauração a partir de um backup criptografado requer que as permissões **VIEW DEFINITION** no certificado ou na chave assimétrica sejam usadas na criptografia durante o backup.  
  
## <a name="options"></a>Opções  
  
### <a name="source"></a>Origem  
 As opções do painel **Restaurar de**identificam o local dos conjuntos de backup no banco de dados e os conjuntos de backups que você deseja restaurar.  
  
|Termo|Definição|  
|----------|----------------|  
|**Backup de banco de dados**|Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .|  
|**Dispositivo**|Selecione os dispositivos lógicos ou físicos de backup (fitas, URLs ou arquivos) que contêm o backup ou os backups a serem restaurados. Isso será necessário se o backup de banco de dados foi feito em uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para selecionar um ou mais dispositivos de backup lógicos ou físicos, clique no botão Procurar que abre a caixa de diálogo **Selecione dispositivos de backup** . Nessa caixa de diálogo você poderá selecionar até 64 dispositivos que pertencem a um único conjunto de mídias. Os dispositivos de fita devem ser conectados fisicamente ao computador que executa a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um arquivo de backup pode estar em um dispositivo de disco local ou remoto. Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md). Você também pode selecionar **URL** como o tipo de dispositivo para os arquivos de backup incluídos no armazenamento do Windows Azure.<br /><br /> Quando você fechar a caixa de diálogo **Selecione dispositivos de backup** , o dispositivo selecionado aparecerá como valores somente leitura na lista **Dispositivo** .|  
|**Backup de banco de dados**|Selecione o nome do banco de dados a partir do qual os backups deverão ser restaurados na lista suspensa.<br /><br /> Observação: essa lista estará disponível apenas quando **Dispositivo** for selecionado. Apenas os bancos de dados que têm backups nos dispositivos selecionados estarão disponíveis.|  
  
### <a name="destination"></a>Destino  
 As opções do painel **Restaurar para** identificam o banco de dados e o ponto de restauração.  
  
|Termo|Definição|  
|----------|----------------|  
|**Backup de banco de dados**|Insira o banco de dados a ser restaurado na lista. Você pode digitar um novo banco de dados ou escolher um banco de dados existente na lista suspensa. A lista inclui todos os bancos de dados do servidor, excluindo os bancos de dados do sistema **mestre** e **tempdb**.<br /><br /> Observação: para restaurar um backup protegido por senha, você deve usar a instrução [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .|  
|**Restaurar para**|A caixa **Restaurar para** será definida, por padrão, como "Para o último backup obtido". Você também pode clicar em **Linha do Tempo** para mostrar a caixa de diálogo **Linha do Tempo do Backup** que exibe o histórico de backup de banco de dados no formato de uma linha do tempo. Clique em **Linha do Tempo** para designar um **datetime** específico para o qual você deseja restaurar o banco de dados. O banco de dados será restaurado então no estado em que estava naquele momento determinado especificado. Consulte [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md).|  
  
### <a name="restore-plan"></a>Plano de restauração  
  
|Termo|Definição|Valores|  
|----------|----------------|------------|  
|**Conjuntos de backup a serem restaurados**|Exibe os conjuntos de backup disponíveis para o local especificado. Cada conjunto de backup, o resultado de uma operação de backup única, é distribuído por todos os dispositivos do conjunto de mídias. Por padrão, um plano de recuperação é sugerido para atingir a meta da operação de restauração que baseia-se na seleção dos conjuntos de backup necessários. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa o histórico de backup no **msdb** para identificar quais backups são necessários para restaurar um banco de dados, e cria um plano de restauração. Por exemplo, para a restauração de um banco de dados, o plano de restauração seleciona o backup completo de banco de dados mais recente, seguido do backup de banco de dados mais recente, subsequente e diferencial, se houver. No modelo de recuperação completa, o plano de restauração, em seguida, seleciona todos os backups de log subsequentes.<br /><br /> Para substituir o plano de recuperação sugerido, você pode alterar as seleções na grade. Todos os backups que dependem de um backup não selecionado serão desmarcados automaticamente.<br /><br /> As caixas de seleção serão habilitadas apenas quando a caixa de **Seleção Manual** estiver marcada. Isso permite selecionar os conjuntos de backup a serem restaurados.<br /><br /> Quando a caixa **Seleção Manual** estiver marcada, a exatidão da opção Restaurar Plano será verificada a cada vez que for modificada. Se a sequência de backups estiver incorreta, será exibida uma mensagem de erro.|**Restaurar**: <br />                          As caixas de seleção selecionadas indicam os conjuntos de backup a serem restaurados.<br /><br /> **Nome**: <br />                          O nome do conjunto de backup.<br /><br /> **Componente**: o componente com backup: **Banco de Dados**, **Arquivo** ou **\<em branco>** (para logs de transações).<br /><br /> **Tipo**: tipo de backup realizado: **Completo**, **Diferencial**ou **Log de Transações**.<br /><br /> **Servidor**: o nome da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que executou a operação de backup.<br /><br /> **Banco de dados**: <br />                          Nome do banco de dados envolvido na operação de backup.<br /><br /> **Posição**: a posição do conjunto de backup no volume.<br /><br /> **Primeiro LSN**: <br />                          Número de sequência de log da primeira transação do conjunto de backup. Em branco para backups de arquivo.<br /><br /> **Último LSN**: <br />                          O número de sequência de log da última transação do conjunto de backup. Em branco para backups de arquivo.<br /><br /> **LSN do Ponto de Verificação**: <br />                          O número de sequência de log (LSN) do ponto de verificação mais recente no momento da criação do backup.<br /><br /> **LSN Completo**: <br />                          Número de sequência de log do backup de banco de dados completo mais recente.<br /><br /> **Data de Início**: <br />                          A data e hora de início da operação de backup, apresentadas na configuração regional do cliente.<br /><br /> **Data de Término**: <br />                          A data e hora da conclusão da operação de backup, apresentadas na configuração regional do cliente.<br /><br /> **Tamanho**: <br />                          O tamanho do conjunto de backup em bytes.<br /><br /> **Nome de Usuário**: <br />                          O nome do usuário que realizou a operação de backup.<br /><br /> **Expiração**: <br />                          A data e hora de validade do conjunto de backup.|  
|**Verificar mídia de backup**|Chama uma instrução RESTORE VERIFY_ONLY nos conjuntos de backup selecionados.<br /><br /> Observação: essa é uma operação de execução longa e seu progresso pode ser acompanhado e cancelado por meio do Monitor de Progresso na Estrutura da Caixa de Diálogo.<br /><br /> Esse botão permite verificar a integridade dos arquivos de backup selecionados antes da restauração.<br /><br /> Ao verificar a integridade de conjuntos de backup, o status do progresso na parte inferior esquerda da caixa de diálogo dirá "Verificando" em vez de "Executando".||  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é possível restaurar um banco de dados de usuário de um backup de banco de dados criado por meio do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou de uma versão posterior. No entanto, os backups do **mestre**, **modelo** e **msdb** que foram criados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] por meio do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] não poderão ser restaurados pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Além disso, backups criados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não podem ser restaurados por nenhuma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usa um caminho padrão diferente das versões anteriores. Assim, para restaurar um banco de dados que foi criado no local padrão de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve usar a opção MOVE.  
  
 Depois de você restaurar um banco de dados da versão anterior para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados será atualizado automaticamente. Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se o banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação poderá levar várias horas e a recriação poderá ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados.  
  
## <a name="restoring-from-an-encrypted-backup"></a>Restaurando a partir de um backup criptografado  
 A restauração requer que o certificado ou a chave assimétrica usada originalmente para criar o backup esteja disponível na instância para a qual você está realizando a restauração. A conta que está executando a restauração deve ter as permissões **VIEW DEFINITIONS** no certificado ou na chave assimétrica. Os certificados usados para criptografar o backup não deverão ser renovados ou atualizados.  
  
## <a name="restoring-from-microsoft-azure-storage"></a>Restaurando por meio do Armazenamento do Microsoft Azure  
Selecione **URL** na lista suspensa **Tipo de mídia de backup:** da caixa de diálogo **Selecione dispositivos de backup** .  Em seguida, clique em **Adicionar** para abrir a caixa de diálogo **Selecione um Local do Arquivo de Backup** na qual você pode selecionar um contêiner de armazenamento do Azure/credenciais do SQL Server, adicionar um novo contêiner de armazenamento do Azure com uma assinatura de acesso compartilhado ou gerar uma assinatura de acesso compartilhado e uma credencial do SQL Server para um contêiner de armazenamento existente. Depois que estiver conectado à conta de armazenamento, os arquivos de backup serão exibidos na caixa de diálogo **Localizar Arquivo de Backup no Microsoft Azure** , na qual você poderá selecionar o arquivo a ser usado na restauração.  Consulte também [Connect to a Microsoft Azure Subscription](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)(Conectar-se a uma assinatura do Microsoft Azure).
  
## <a name="see-also"></a>Consulte Também  
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Restaurar um backup de um dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
