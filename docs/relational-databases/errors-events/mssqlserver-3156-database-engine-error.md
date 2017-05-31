---
title: MSSQLSERVER_3156 | Microsoft Docs
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
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 08f8ea872ef58a42b07254417db0a19a5dfd9fd7
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3156"></a>MSSQLSERVER_3156
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3156|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_CANT_WRITE|  
|Texto da mensagem|O arquivo '%ls' não pode ser restaurado para '%ls'. Use WITH MOVE para identificar um local válido para o arquivo.|  
  
## <a name="explanation"></a>Explicação  
Esta mensagem geral identifica os nomes de arquivo lógicos ou físicos dos arquivos que não puderam ser restaurados devido a um problema com o local especificado.  
  
### <a name="possible-causes"></a>Causas possíveis  
As causas possíveis incluem as seguintes:  
  
-   Talvez seja preciso acessar o diretório especificado do Windows.  
  
-   Você pode ter digitado incorretamente o caminho ou pode ter especificado um caminho que não existe.  
  
-   O nome de arquivo pode estar sendo usado por um arquivo que não pode ser substituído.  
  
## <a name="user-action"></a>Ação do usuário  
Veja nos logs de erros outras mensagens mais detalhadas.  
  
Corrija o problema com o local especificado, por exemplo, concedendo acesso, ou use a opção WITH MOVE em sua instrução RESTORE para realocar o arquivo.  
  
## <a name="see-also"></a>Consulte também  
[Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar arquivos em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  

