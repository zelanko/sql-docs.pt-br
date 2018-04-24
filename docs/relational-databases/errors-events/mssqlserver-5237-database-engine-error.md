---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7d9dc07600323fe8621a480201a8dab673ce4f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5237|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|Texto da mensagem|Falha na verificação entre conjuntos de linhas DBCC do objeto 'NAME' (ID de objeto O_ID) devido a um erro de consulta interno.|  
  
## <a name="explanation"></a>Explicação  
Um erro interno fez com que DBCC não conseguisse executar a consulta para verificar exibições indexadas.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando DBCC novamente.  
  
