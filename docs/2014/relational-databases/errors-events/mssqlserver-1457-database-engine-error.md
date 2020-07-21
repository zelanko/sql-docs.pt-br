---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9811239df295b584d26f69150aa307a5613fe9e9
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552251"
---
# <a name="mssqlserver_1457"></a>MSSQLSERVER_1457
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1457|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_PAGE_UNDO_PENDING|  
|Texto da mensagem|A sincronização do banco de dados espelho, '%.* ls', foi interrompida, deixando o banco de dados em um estado inconsistente. Falha no comando ALTER DATABASE. Verifique se o banco de dados espelho voltou a funcionar e está online e reconecte a instância do servidor espelho para permitir que o banco de dados espelho termine a sincronização.|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem indica que a instrução ALTER DATABASE *database_name* SET PARTNER OFF falhou. A falha na tentativa de remover o espelhamento de banco de dados interrompeu a sincronização do banco de dados espelho. O banco de dados está em estado inconsistente.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver esse erro, você pode realizar uma das seguintes ações:  
  
-   Restaure o contato entre o servidor espelho e o servidor principal para permitir a sincronização do banco de dados espelho.  
  
-   Descarte o banco de dados espelho.  
  
     Depois de descartar o banco de dados espelho, você pode criar um banco de dados espelho a partir de backups.  
  
    > [!NOTE]  
    >  Você só poderá descartar o banco de dados espelho quando o espelhamento ainda estiver habilitado após a falha de uma instrução SET PARTNER OFF.  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
  
