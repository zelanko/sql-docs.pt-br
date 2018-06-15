---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85a3954b37ca6f3467bf1fc0d4fafda7dadb59ad
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34322207"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1457|  
|Origem do evento|MSSQLSERVER|  
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
    > Você só poderá descartar o banco de dados espelho quando o espelhamento ainda estiver habilitado após a falha de uma instrução SET PARTNER OFF.  
  
## <a name="see-also"></a>Consulte Também  
[Espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
[Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
[Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
