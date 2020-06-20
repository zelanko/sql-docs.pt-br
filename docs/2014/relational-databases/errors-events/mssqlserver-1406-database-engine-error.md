---
title: MSSQLSERVER_1406 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e823c14fcb6e1a408d1589d0588a3fb966552d7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967946"
---
# <a name="mssqlserver_1406"></a>MSSQLSERVER_1406
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1406|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_BADSTATEFORFORCESERVICE|  
|Texto da mensagem|Não foi possível forçar o serviço com segurança. Remova o espelhamento de banco de dados e recupere o banco de dados "%.*ls" para obter acesso.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não pode forçar o serviço porque o estado de espelhamento não pode garantir que o processo forçar serviço funcione corretamente.  
  
## <a name="user-action"></a>Ação do usuário  
 Remova o espelhamento de banco de dados. Depois, você pode recuperar o banco de dados espelho para obter acesso a ele.  
  
## <a name="see-also"></a>Consulte Também  
 [Forçar serviço em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)   
 [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
