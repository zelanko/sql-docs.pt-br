---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 64e1a836995fe8738bb5c2ff0cb4de10d84d1f29
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054008"
---
# <a name="mssqlserver_3176"></a>MSSQLSERVER_3176
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3176|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_FILE_CLAIM|  
|Texto da mensagem|O arquivo '%ls' foi reivindicado por '%ls' (%d) e '%ls' (%d). A cláusula WITH MOVE pode ser usada para realocar um ou mais arquivos.|  
  
## <a name="explanation"></a>Explicação  
 Tentativa de uso de um arquivo para mais de uma finalidade.  
  
### <a name="possible-causes"></a>Possíveis causas  
 Outro banco de dados já está usando o nome de arquivo.  
  
## <a name="user-action"></a>Ação do usuário  
 Restaure os arquivos de banco de dados em um local diferente. Em uma instrução RESTORE, use uma cláusula WITH MOVE para mover cada arquivo. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], altere os locais de arquivo na grade **Restaurar os arquivos de banco de dados como** da caixa de diálogo **Restaurar Opções de Banco de Dados**.  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Restaurar arquivos para um novo local &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
