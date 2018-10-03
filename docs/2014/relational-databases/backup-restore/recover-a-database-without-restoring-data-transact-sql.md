---
title: Recuperar um banco de dados sem restaurar os dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: af089910155ea865812bf8f21c18745bc26a0bd4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050366"
---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>Recuperar um banco de dados sem restaurar dados (Transact-SQL)
  Normalmente, todos os dados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são restaurados antes de o banco de dados ser recuperado. Porém, uma operação de restauração pode recuperar um banco de dados sem de fato restaurar um backup; por exemplo, ao recuperar um arquivo somente leitura que seja consistente com o banco de dados. Isso é chamado de uma *restauração somente recuperação*. Quando dados offline já são consistentes com o banco de dados e só precisam ser disponibilizados, uma operação de restauração somente recuperação conclui a recuperação do banco de dados e coloca os dados online.  
  
 Uma restauração somente recuperação pode ocorrer para um banco de dados inteiro ou para um ou mais arquivos ou grupos de arquivos.  
  
## <a name="recovery-only-database-restore"></a>Restauração de banco de dados somente recuperação  
 Uma restauração somente recuperação de banco de dados pode ser útil nas seguintes situações:  
  
-   Você não recuperou o banco de dados ao restaurar o último backup em uma sequência de restauração, e agora quer recuperar o banco de dados para colocá-lo online.  
  
-   O banco de dados está em modo de espera e você quer atualizá-lo sem aplicar outro backup de log.  
  
 A sintaxe [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para a restauração de um banco de dados somente recuperação é a seguinte:  
  
 RESTORE DATABASE *database_name* WITH RECOVERY  
  
> [!NOTE]  
>  A cláusula FFROM **=** \<*backup_device>* não é usada em restaurações somente recuperação porque nenhum backup é necessário.  
  
 **Exemplo**  
  
 O exemplo a seguir recupera o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de amostra em uma operação de restauração sem restaurar dados.  
  
```  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## <a name="recovery-only-file-restore"></a>Restauração de arquivo somente recuperação  
 Uma restauração somente recuperação pode ser útil na situação seguinte:  
  
 Um banco de dados é restaurado por etapas. Depois da conclusão da restauração do grupo de arquivos primário, um ou mais dos arquivos não restaurados estão consistentes com o novo estado do banco de dados, talvez porque tenham sido somente leitura por algum tempo. Esses arquivos só precisam ser recuperados; a cópia de dados é desnecessária.  
  
 Uma operação de restauração somente recuperação coloca os dados do grupo de arquivos offline online; nenhuma fase de cópia de dados, refazer ou desfazer acontece. Para obter informações sobre as fases de restauração, confira [Visão geral da restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md).  
  
 A sintaxe [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para a restauração de um arquivo somente recuperação é:  
  
 RESTORE DATABASE *database_name* { FILE **=***logical_file_name* | FILEGROUP **=***logical_filegroup_name* }[ **,**...* n* ] WITH RECOVERY  
  
 **Exemplo**  
  
 O exemplo a seguir ilustra uma restauração de arquivos somente recuperação de um grupo de arquivos secundário, `SalesGroup2`, no banco de dados `Sales` . O grupo de arquivos primário já foi restaurado como a etapa inicial de uma restauração por etapas e `SalesGroup2` está consistente com o grupo de arquivos primário restaurado. Recuperar esse grupo de arquivos e colocá-lo online requer somente uma única instrução.  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>Exemplos de conclusão de um cenário de restauração por etapas com uma restauração somente recuperação  
 **Modelo de recuperação simples**  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **Modelo de recuperação completa**  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>Consulte também  
 [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
