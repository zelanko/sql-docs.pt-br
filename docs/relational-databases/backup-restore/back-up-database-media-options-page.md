---
title: Fazer backup de banco de dados (página Opções de Mídia) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql13.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d7103048caf9d4cc66a32065a410d41529110939
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="back-up-database-media-options-page"></a>Backup de Banco de Dados (página Opções de Mídia)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a página  **Opções de Mídia** da caixa de diálogo **Fazer Backup de Banco de Dados** para exibir ou modificar opções de mídia de banco de dados.  
  
 **Para criar um backup usando o SQL Server Management Studio**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  Você pode definir um plano de manutenção de banco de dados para criar backups de banco de dados. Para obter mais informações, consulte [Planos de Manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md) e [Usar o Assistente de Plano de Manutenção](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) correspondente clicando no botão **Script** e selecionando um destino para o script.  
  
## <a name="options"></a>Opções  
  
### <a name="overwrite-media"></a>Substituir mídia  
 As opções do painel **Substituir mídia** controlam como o backup é gravado na mídia. Se você tiver selecionado a URL (Armazenamento do Windows Azure) como destino de backup na página Geral da caixa de diálogo Backup de Banco de Dados, as opções na seção Substituir mídia serão desabilitadas. É possível substituir um backup usando a instrução Transact-SQL **BACKUP TO URL. WITH FORMAT**. Para saber mais, confira [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
 Há suporte somente para a opção **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes** nas opções de criptografia. Se você selecionar as opções na seção **Fazer backup na mídia existente**, as opções de criptografias na página **Opções de Backup** serão desabilitadas.  
  
> [!NOTE]  
>  Para obter informações sobre conjuntos de mídias, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 **Fazer backup no conjunto de mídias existente**  
 Faz o backup de um banco de dados em um conjunto de mídias existente. A seleção desse botão de opção habilita três opções.  
  
 Escolha uma das seguintes opções:  
  
 **Anexar ao conjunto de backup existente**  
 Anexe o conjunto de backup ao conjunto de mídias existente, preservando qualquer backup anterior.  
  
 **Substituir todos os conjuntos de backup existentes**  
 Substitua pelo backup atual quaisquer backups anteriores no conjunto de mídias existente.  
  
 **Verificar nome do conjunto de mídias e validade do conjunto de backup**  
 Opcionalmente, ao efetuar o backup para um conjunto de mídias existente, solicite que a operação de backup verifique o nome e a data de validade dos conjuntos de backup.  
  
 **Nome do conjunto de mídias**  
 Se a opção **Verificar nome do conjunto de mídias e validade do conjunto de backup** for marcada, opcionalmente, especifique o nome do conjunto de mídias a ser usado para essa operação de backup.  
  
 **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
 Use um conjunto de mídias novo, apagando os conjuntos de backup anteriores.  
  
 Clicando-se nessa opção as seguintes opções são habilitadas:  
  
 **Novo nome do conjunto de mídias**  
 Opcionalmente, digite um nome novo para os conjuntos de mídias.  
  
 **Descrição do novo conjunto de mídias**  
 Opcionalmente, digite uma descrição significativa do novo conjunto de mídias. Essa descrição deve ser específica o suficiente para comunicar o conteúdo com precisão.  
  
### <a name="reliability"></a>Confiabilidade  
 As opções do painel **Log de transações** controlam o gerenciamento de erro pela operação de backup.  
  
 **Verificar backup quando concluído**  
 Verifique se o conjunto de backup está completo e se todos os volumes estão legíveis.  
  
 **Executar soma de verificação antes de gravar na mídia**  
 Verifique as somas de verificação antes de gravar na mídia de backup. A seleção dessa opção é o equivalente a especificar a opção CHECKSUM na instrução BACKUP de [!INCLUDE[tsql](../../includes/tsql-md.md)]. A seleção dessa opção pode aumentar a carga de trabalho e diminuir a taxa de transferência da operação de backup. Para obter informações sobre somas de verificação de backup, veja [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 **Continuar se houver erro**  
 A operação de backup deve continuar mesmo tendo-se encontrado um ou mais erros.  
  
### <a name="transaction-log"></a>Log de transações  
 As opções do painel **Log de transações** controlam o comportamento de um backup de log de transações. Essas opções são relevantes apenas no modelo de recuperação completa ou modelo de recuperação bulk-logged. Elas são habilitadas apenas se o **Log de transações** tiver sido selecionado no campo **Tipo de backup** na página [Geral](../../relational-databases/backup-restore/back-up-database-general-page.md) da caixa de diálogo **Fazer Backup de Banco de Dados**.  
  
> [!NOTE]  
>  Para obter informações sobre backups do log de transações, veja [Backups do log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 **Truncar o log de transações**  
 Faça backup do log de transações e trunque-o para liberar espaço de log. O banco de dados permanece online. Essa é a opção padrão.  
  
 **Fazer backup da parte final do log e deixar o banco de dados no estado de restauração**  
 Faça o backup da parte final do log e deixe o banco de dados em um estado de restauração. Essa opção cria um *backup da parte final do log*, que faz o backup de logs que ainda não tiveram seus backups executados (o log ativo), normalmente, em preparação para a restauração de um banco de dados. O banco de dados ficará indisponível para usuários até que seja completamente restaurado.  
  
 A seleção dessa opção equivale à especificação de WITH NO_TRUNCATE, NORECOVERY em uma instrução [BACKUP](../../t-sql/statements/backup-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]). Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### <a name="tape-drive"></a>Unidade de fita  
 As opções do painel **Unidade de fita** controlam o gerenciamento de fita durante a operação de backup. Essas opções serão habilitadas apenas se **Fita** tiver sido selecionada no painel **Destino** da página [Geral](../../relational-databases/backup-restore/back-up-database-general-page.md) da caixa de diálogo **Fazer Backup de Banco de Dados**.  
  
> [!NOTE]  
>  Para obter informações sobre como usar dispositivos de fita, veja [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 **Descarregar a fita após o backup**  
 Depois que o backup for concluído, descarregue a fita.  
  
 **Rebobinar a fita antes de descarregar**  
 Antes de descarregar, libere e rebobine a fita. Isso só será habilitado se **Descarregar a fita após o backup** for selecionado.  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
