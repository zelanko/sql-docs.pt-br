---
description: MSSQLSERVER_1406
title: MSSQLSERVER_1406 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 45c5889a0f79757ccd2ae4de74cccc1eed8846f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88334772"
---
# <a name="mssqlserver_1406"></a>MSSQLSERVER_1406
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
[Forçar serviço em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](~/database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
[Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
