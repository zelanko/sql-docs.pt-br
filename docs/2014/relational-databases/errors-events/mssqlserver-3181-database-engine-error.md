---
title: MSSQLSERVER_3181 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c2a5f0790969c43c3e8d55340ece141c7ab2069a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009993"
---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
    
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
  
## <a name="see-also"></a>Consulte também  
 [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Restaurar arquivos para um novo local &#40;do SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
  
