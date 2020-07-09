---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ab27a6836d59fe226e3f8bfc67b523f048be4327
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781027"
---
# <a name="mssqlserver_1457"></a>MSSQLSERVER_1457
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
    > Você só poderá descartar o banco de dados espelho quando o espelhamento ainda estiver habilitado após a falha de uma instrução SET PARTNER OFF.  
  
## <a name="see-also"></a>Consulte Também  
[Espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
[Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
[Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
