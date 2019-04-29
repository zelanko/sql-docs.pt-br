---
title: Backups parciais (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4213bcee1d17d27bf63da9eb286b21dea4cc5a02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921912"
---
# <a name="partial-backups-sql-server"></a>Backups parciais (SQL Server)
  Todos os modelos de recuperação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferecem suporte a backups parciais. Então, este tópico é relevante a todos os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, os backups parciais são projetados para uso no modelo de recuperação simples para aprimorar a flexibilidade no backup de bancos de dados muito grandes que contêm um ou mais grupos de arquivos somente leitura.  
  
 Os backups parciais são úteis sempre que você quer excluir grupos de arquivos somente leitura. Um *backup parcial* se assemelha a um backup de banco de dados completo, mas não contém todos os grupos de arquivos. Em vez disso, para um banco de dados somente leitura, um backup parcial contém todos os dados do grupo de arquivos primário, todos os grupos de arquivos de leitura/gravação e, opcionalmente, um ou mais arquivos de somente leitura. Um backup parcial de um banco de dados somente leitura contém apenas o grupo de arquivos primário.  
  
> [!NOTE]  
>  Se o banco de dados somente leitura for alterado para leitura/gravação depois de um backup parcial, será possível haver grupos de arquivos secundários leitura/gravação que não estejam no backup parcial. Nesse caso, se você tentar fazer um backup parcial diferencial, o backup falhará. Para fazer um backup diferencial parcial de banco de dados, é necessário fazer outro backup parcial. O novo backup parcial contém todos os grupos de arquivos leitura/gravação secundários e pode servir de base para backups diferenciais parciais.  
  
 Backups de arquivos de grupos de arquivos do tipo somente leitura podem ser combinados com backups parciais. Para obter informações sobre backups de arquivos, veja [Backups completos de arquivos &#40;SQL Server&#41;](full-file-backups-sql-server.md).  
  
 Um backup parcial pode servir como *base diferencial* para backups parciais diferenciais. Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
> [!NOTE]  
>  Não há suporte para backups parciais no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no Assistente de Plano de Manutenção.  
  
 **Para criar um backup parcial**  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) (READ_WRITE_FILEGROUPS; opção FILEGROUP, se necessário)  
  
 **Para usar um backup parcial em uma sequência de restauração**  
  
-   [Exemplo: Restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: Restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
