---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33dfe774838aa88dc0c68829ae0abe34f3f1dda9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083628"
---
# <a name="mssqlserver17065"></a>MSSQLSERVER_17065
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17065|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLASSERT_BOTH|  
|Texto da mensagem|Declaração do SQL Server: arquivo: \<%s>, linha = %d falha de declaração = '%s' %s. Talvez esse erro esteja relacionado à temporização. Se o erro persistir após a repetição da instrução, use DBCC CHECKDB para verificar a integridade estrutural do banco de dados ou reinicie o servidor para assegurar que as estruturas de dados na memória não estejam corrompidas.|  
  
## <a name="explanation"></a>Explicação  
 Talvez o erro seja causado por erros transitórios relacionados à temporização ou por dados corrompidos na memória ou no disco.  
  
## <a name="user-action"></a>Ação do usuário  
 Exiba novamente a instrução que causou o disparo da exceção. Se o erro foi causado por um evento relacionado à temporização, talvez ele não ocorra novamente. Se o problema persistir, execute DBCC CHECKDB para verificar se há dados corrompidos no disco. Reinicie o servidor para assegurar que as estruturas de dados na memória não estão corrompidas.  
  
## <a name="see-also"></a>Consulte também  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
