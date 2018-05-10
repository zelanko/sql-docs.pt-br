---
title: MSSQLSERVER_1204 | Microsoft Docs
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
- 1204 (Database Engine error)
ms.assetid: de6ece78-79de-484d-9224-ca0f7645815f
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34d2c6e19ec1625c8213e7cb7bc2cc7894d847d2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver1204"></a>MSSQLSERVER_1204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1204|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LK_OUTOF|  
|Texto da mensagem|A instância do Mecanismo de Banco de Dados do SQL Server não pode obter um recurso LOCK neste momento. Execute a instrução novamente quando houver menos usuários ativos. Peça ao administrador de banco de dados que verifique a configuração do bloqueio e da memória dessa instância ou as transações de longa execução.|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde obter um recurso de bloqueio. Isso pode ter sido causado por qualquer uma das seguintes razões:  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode alocar mais memória do sistema operacional porque está sendo usado por outros processos ou porque o servidor está operando com a opção **memória máxima do servidor** configurada.  
  
-   O gerenciador de bloqueio não usará mais que 60 por cento da memória disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Ação do usuário  
Se você suspeitar que o SQL Server não pode alocar memória suficiente, tente o seguinte:  
  
-   Se outros aplicativos além do SQL Server estiverem consumindo recursos, tente interromper esses aplicativos ou considere executá-los em um servidor separado. Isso irá liberar memória de outros processos para o SQL Server.  
  
-   Se você tiver configurado a memória máxima do servidor, aumente a definição da memória máxima do servidor.  
  
Se você suspeitar que o gerenciador de bloqueio usou o máximo de memória disponível, identifique a transação que está mantendo a maioria dos bloqueios e a conclua. O script seguinte identificará a transação com a maioria de bloqueios:  
  
```  
SELECT request_session_id, COUNT (*) num_locks  
FROM sys.dm_tran_locks  
GROUP BY request_session_id   
ORDER BY count (*) DESC  
```  
  
Identifique a ID da sessão mais elevada e encerre-a usando o comando KILL.  
  
