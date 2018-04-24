---
title: MSSQLSERVER_7308 | Microsoft Docs
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
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f67200d7489bf90102325cf3463b5ea58424f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7308|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|RMT_STA_DISABLED|  
|Texto da mensagem|Não é possível usar o provedor OLE DB '%ls' para consultas distribuídas porque ele está configurado para execução no modo STA.|  
  
## <a name="explanation"></a>Explicação  
Você usou um provedor OLE DB configurado para execução no modo STA. Provedores do OLE DB executados no modo STA não podem ser usados para consultas distribuídas.  
  
## <a name="user-action"></a>Ação do usuário  
Para resolver o erro, configure o provedor para execução no modo MTA. Se o provedor não tiver suporte para MTA e não for possível atualizá-lo para uma versão com suporte a MTA, considere configurá-lo para execução fora do processo. O fornecedor do provedor deverá ser capaz de informar se o provedor dá suporte para MTA ou execução fora do processo.  
  
