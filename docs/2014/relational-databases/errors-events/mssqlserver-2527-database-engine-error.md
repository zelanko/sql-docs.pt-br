---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f1d2bd9bd3ee1cc26c0bd488af0dd7891d2a8741
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868857"
---
# <a name="mssqlserver2527"></a>MSSQLSERVER_2527
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2527|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Texto da mensagem|Não foi possível processar o índice I_NAME da tabela O_NAME porque o grupo de arquivos F_NAME está offline.|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem informativa indica que não foi possível verificar o índice porque um dos grupos de arquivos que armazena dados para o índice está offline. O estado dos arquivos em um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online. Se não houver outros problemas, todos os demais índices do mesmo objeto serão verificados.  
  
## <a name="user-action"></a>Ação do usuário  
 Para exibir o estado dos arquivos do grupo de arquivos especificado, consulte a exibição do catálogo **sys.database_files** ou **sys.master_files**.  
  
 Restaure o arquivo offline de um backup.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
