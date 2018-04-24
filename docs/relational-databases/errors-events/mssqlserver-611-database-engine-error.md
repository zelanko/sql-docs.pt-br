---
title: MSSQLSERVER_611 | Microsoft Docs
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
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e4bf81ee5f885318cf87c69237bf436fee5a75a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|611|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|VAR_SIZE_TOO_BIG|  
|Texto da mensagem|Não é possível inserir ou atualizar uma linha porque o tamanho total da coluna variável, incluindo a sobrecarga, está %d bytes acima do limite.|  
  
## <a name="explanation"></a>Explicação  
O tamanho máximo da coluna variável é maior que o permitido pelo esquema. O erro 611 é retornado quando a coluna variável está acima do limite no caso fixo quando o formato de armazenamento vardecimal está habilitado ou quando o tamanho da coluna variável está acima do limite permitido no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para um registro de dados compactado.  
  
## <a name="user-action"></a>Ação do usuário  
Reduza o tamanho do registro.  
  
