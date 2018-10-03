---
title: 'Exemplo: Restauração Offline de arquivos primário e um (modelo de recuperação completa) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- offline restores [SQL Server]
- restore sequences [SQL Server], offline
ms.assetid: 7d6c50eb-dc84-4d66-855a-0b5f1bd89737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fec409bf6f391e14dd5e1a2b8b102df2fd00cfd4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060476"
---
# <a name="example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model"></a>Exemplo: Restauração offline do grupo de arquivos primário e mais um (modelo de recuperação completa)
  Este tópico é relevante apenas para bancos de dados com modelos de recuperação completa e que contêm vários grupos de arquivos.  
  
 Neste exemplo, um banco de dados denominado `adb` contém três grupos de arquivos. Os grupos de arquivos `A` e `C` são de leitura/gravação e o grupo de arquivos `B` é somente leitura. O grupo de arquivos primário e o grupo de arquivos `B` estão danificados, mas os grupos de arquivos `A` e `C` estão intactos. Antes do desastre, todos os grupos de arquivos estavam online.  
  
 O administrador de banco de dados decide restaurar e recuperar o grupo de arquivos primário e grupo de arquivos `B`. O banco de dados está usando o modelo de recuperação completa; portanto, antes do início da restauração, um backup do final do log deve ser extraído do banco de dados. Quando o banco de dados estiver online, os grupos de arquivos `A` e `C` ficarão automaticamente online.  
  
> [!NOTE]  
>  A sequência de restauração offline tem menos etapas do que a restauração online de um arquivo somente leitura. Para obter um exemplo, veja [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md). Porém, todo o banco de dados está offline na duração da sequência.  
  
## <a name="tail-log-backup"></a>Backup do final do log  
 Antes de restaurar o banco de dados, o administrador do banco de dados deve fazer backup do final do log. Como o banco de dados está danificado, é preciso usar a opção NO_TRUNCATE para criar o backup do final do log:  
  
```  
BACKUP LOG adb TO tailLogBackup   
   WITH NORECOVERY, NO_TRUNCATE  
```  
  
 O backup do final do log é o último backup aplicado nas sequências de restauração a seguir.  
  
## <a name="restore-sequence"></a>Sequência de restauração  
 Para restaurar o grupo de arquivos primário e o grupo de arquivos `B`, o administrador do banco de dados usa uma sequência de restauração sem a opção PARTIAL, do seguinte modo:  
  
```  
RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
WITH NORECOVERY  
RESTORE DATABASE adb FILEGROUP='B' FROM backup2   
WITH NORECOVERY  
RESTORE LOG adb FROM backup3 WITH NORECOVERY  
RESTORE LOG adb FROM backup4 WITH NORECOVERY  
RESTORE LOG adb FROM backup5 WITH NORECOVERY  
RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
```  
  
 Os arquivos que não estão restaurados ficam automaticamente online. Todos os grupos de arquivos agora estão online.  
  
## <a name="see-also"></a>Consulte também  
 [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
