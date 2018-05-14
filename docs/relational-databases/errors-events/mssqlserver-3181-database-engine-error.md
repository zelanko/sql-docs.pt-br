---
title: MSSQLSERVER_3181 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 863e45dab3eeb3e557acc140e32689e991d16995
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3181|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_STORAGE_VERIFY|  
|Texto da mensagem|A tentativa de restaurar este backup pode encontrar problemas de espaço de armazenamento. As próximas mensagens fornecerão detalhes.|  
  
## <a name="explanation"></a>Explicação  
A instrução RESTORE VERIFYONLY verifica o espaço de armazenamento disponível no disco onde o banco de dados será restaurado.  
  
### <a name="possible-causes"></a>Causas possíveis  
O espaço disponível em disco pode ser insuficiente para restaurar o backup que está sendo verificado.  
  
## <a name="user-action"></a>Ação do usuário  
Restaure o backup em um local com espaço em disco suficiente ou forneça mais espaço no disco.  
  
## <a name="see-also"></a>Consulte Também  
[Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar arquivos em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
