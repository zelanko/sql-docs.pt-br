---
title: MSSQLSERVER_7916 | Microsoft Docs
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
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64b1f813540c6e07140df419691bd4b4d32d77f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7916"></a>MSSQLSERVER_7916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7916|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_REPAIR_RECORD|  
|Texto da mensagem|Correção: registro excluído referente a ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE), na página P_ID, slot S_ID. Os índices serão recriados.|  
  
## <a name="explanation"></a>Explicação  
Essa é uma mensagem informativa da cláusula REPAIR que indica que o registro especificado foi excluído da página.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum  
  
