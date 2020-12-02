---
title: 'Restauração online: arquivo somente leitura (modelo de recuperação simples)'
description: Este exemplo mostra uma restauração online no SQL Server de um arquivo somente leitura de um banco de dados usando o modelo de recuperação simples com vários grupos de arquivos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], online
- online restores [SQL Server], simple recovery model
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 0c691fc6-9865-46a7-b055-8097424492d6
author: cawrites
ms.author: chadam
ms.openlocfilehash: 58c4448ecde5bfed478ad19aa961dc74c1db59a5
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130433"
---
# <a name="example-online-restore-of-a-read-only-file-simple-recovery-model"></a>Exemplo: Restauração online de um arquivo somente leitura (modelo de recuperação simples)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este tópico é pertinente para bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob o modelo de recuperação simples que contenham um grupo de arquivos somente leitura. No modelo de recuperação simples, um arquivo somente leitura pode ser restaurado online se existir um backup do arquivo que tenha sido feito desde a última vez em que arquivo tornou-se somente leitura.  
  
 Neste exemplo, um banco de dados denominado `adb` contém três grupos de arquivos. O grupo de arquivos `A` é leitura/gravação, e os grupos de arquivos `B` e `C` são somente leitura. Inicialmente, todos os grupos de arquivos estão online. Um arquivo somente leitura no grupo de arquivos `B`, `b1`, tem de ser restaurado. O administrador de banco de dados pode restaurá-lo usando um backup que foi feito depois de o arquivo tornar-se somente leitura. Durante a restauração, o grupo de arquivos `B` estará offline, mas o resto do banco de dados permanecerá online.  
  
## <a name="restore-sequence"></a>Sequência de restauração  
  
> [!NOTE]  
>  A sintaxe para uma sequência de restauração online é igual à de uma sequência de restauração offline.  
  
 Para restaurar o arquivo, o administrador do banco de dados usa a seguinte sequência de restauração:  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup   
WITH RECOVERY  
```  
  
 O arquivo agora está online.  
  
## <a name="additional-examples"></a>Exemplos adicionais  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura #40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
