---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 76ad2670dc60665fa128dd97aa335330228262ef
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780353"
---
# <a name="mssqlserver_2530"></a>MSSQLSERVER_2530
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|2530|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_INDEX_IS_OFFLINE|  
|Texto da mensagem|O índice "%.*ls" na tabela "%.\*ls" está desabilitado.|  
  
## <a name="explanation"></a>Explicação  
A instrução DBCC não pode continuar porque o índice especificado está desabilitado. Depois que um índice é desabilitado, ele permanece em estado desabilitado até que seja reconstruído ou descartado e recriado.  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Habilite o índice desabilitado usando um dos seguinte métodos:  
  
    -   Instrução ALTER INDEX com a cláusula REBUILD  
  
    -   CREATE INDEX com a cláusula DROP_EXISTING  
  
    -   DBCC DBREINDEX  
  
2.  Execute novamente a instrução DBCC.  
  
## <a name="see-also"></a>Consulte Também  
[Habilitar índices e restrições](~/relational-databases/indexes/enable-indexes-and-constraints.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[DBCC DBREINDEX &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)  
  
