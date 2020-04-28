---
title: Backups somente cópia (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96267b98d7e17b920e0a7cee70b69e4c964584e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798012"
---
# <a name="copy-only-backups-sql-server"></a>Backups somente cópia (SQL Server)
  Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Geralmente, um backup altera o banco de dados e afeta a forma de restauração dos backups posteriores. Contudo, ocasionalmente, é útil fazer um backup para uma finalidade especial sem afetar o backup global e os procedimentos de restauração do banco de dados. Backups de cópia servem para essa finalidade.  
  
 Os tipos de backups somente cópia são:  
  
-   Backups completos somente cópia (todos os modelos de recuperação)  
  
     Um backup somente cópia não pode servir como base diferencial ou backup diferencial e não afeta a base diferencial.  
  
     Restaurar um backup completo somente cópia é o mesmo que restaurar qualquer outro backup completo.  
  
-   Backups de log somente cópia (só modelo de recuperação completa e modelo de recuperação bulk-logged)  
  
     Um backup de log somente cópia preserva o ponto de arquivo de log existente e, portanto, não afeta a sequência de backups de log regulares. Backups de log somente cópia em geral são desnecessários. Em vez disso, você pode criar um novo backup de log de rotina (usando WITH NORECOVERY) e usar esse backup com qualquer backup de log anterior necessário para a sequência de restauração. No entanto, um backup de log somente cópia pode ser útil às vezes para executar uma restauração online. Para obter um exemplo disso, veja [Exemplo: restauração online de um arquivo leitura/gravação &#40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md).  
  
     O log de transações nunca é truncado após um backup somente cópia.  
  
 Backups somente cópia são registrados na coluna **is_copy_only** da tabela [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) .  
  
## <a name="to-create-a-copy-only-backup"></a>Para criar um backup somente cópia  
 Você pode criar um backup somente cópia usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell.  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
1.  Na página **Geral** da caixa de diálogo de **Banco de Dados de Backup**, selecione a opção **Backup somente cópia**.  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 A sintaxe [!INCLUDE[tsql](../../../includes/tsql-md.md)] essencial é a seguinte:  
  
-   Para um backup completo somente cópia:  
  
     *Database_name* de banco de \<dados*>* de backup para backup_device... COM COPY_ONLY...  
  
    > [!NOTE]  
    >  COPY_ONLY não tem nenhum efeito quando é especificado com a opção DIFFERENTIAL.  
  
-   Para um backup de log somente cópia:  
  
     *Database_name* de log de *\<* backup*>* para backup_device... COM COPY_ONLY...  
  
###  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
  
Use o cmdlet `Backup-SqlDatabase` com o parâmetro `-CopyOnly`.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  

### <a name="to-create-a-full-or-log-backup"></a>Para criar um backup completo ou de log
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
### <a name="to-view-copy-only-backups"></a>Para exibir backups somente cópia
  
-   [conjunto de backup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
### <a name="to-set-up-and-use-the-sql-server-powershell-provider"></a>Para configurar e usar o provedor do SQL Server PowerShell
  
-   [Provedor do SQL Server PowerShell](../../powershell/sql-server-powershell-provider.md)  

## <a name="see-also"></a>Consulte Também  
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [Copiar bancos de dados com backup e restauração](../databases/copy-databases-with-backup-and-restore.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
