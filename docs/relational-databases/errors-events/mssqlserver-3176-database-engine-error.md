---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cca32f5a1a2947dc65cf85976874ce1043de0e3d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3176|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_FILE_CLAIM|  
|Texto da mensagem|O arquivo '%ls' foi reivindicado por '%ls' (%d) e '%ls' (%d). A cláusula WITH MOVE pode ser usada para realocar um ou mais arquivos.|  
  
## <a name="explanation"></a>Explicação  
Tentativa de uso de um arquivo para mais de uma finalidade.  
  
### <a name="possible-causes"></a>Causas possíveis  
Outro banco de dados já está usando o nome de arquivo.  
  
## <a name="user-action"></a>Ação do usuário  
Restaure os arquivos de banco de dados em um local diferente. Em uma instrução RESTORE, use uma cláusula WITH MOVE para mover cada arquivo. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], altere os locais de arquivo na grade **Restaurar os arquivos de banco de dados como** da caixa de diálogo **Restaurar Opções de Banco de Dados**.  
  
## <a name="see-also"></a>Consulte também  
[Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar arquivos em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  

