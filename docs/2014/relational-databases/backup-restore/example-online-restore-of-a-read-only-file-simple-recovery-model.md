---
title: 'Exemplo: restauração online de um arquivo somente leitura (modelo de recuperação simples) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], online
- online restores [SQL Server], simple recovery model
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 0c691fc6-9865-46a7-b055-8097424492d6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ccbb89a7af71545c3b410356b6ab6b101983798d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62876146"
---
# <a name="example-online-restore-of-a-read-only-file-simple-recovery-model"></a>Exemplo: Restauração online de um arquivo somente leitura (modelo de recuperação simples)
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
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo de leitura/gravação #40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Exemplo: restauração online de um arquivo somente leitura &#40;Modelo de recuperação completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
