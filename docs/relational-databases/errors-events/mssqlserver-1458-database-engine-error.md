---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0585f1167083a6b2126ad98d3c6f3b8d81478de2
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321517"
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1458|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_FAILREDO_ON_PRIMARY|  
|Texto da mensagem|A cópia principal do banco de dados '%.*ls' encontrou o erro %d, status %d, severidade %d. O espelhamento de banco de dados foi suspenso. Tente resolver a condição de erro e retomar o espelhamento.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem indica que o banco de dados principal encontrou um erro que causou a suspensão do espelhamento de banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
A maioria dos casos desse erro é corrigida automaticamente. Se o problema persistir, reiniciar o banco de dados ou a instância do servidor geralmente corrige o problema. Para obter mais informações, procure no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cada parceiro o erro associado que precedeu essa mensagem.  
  
## <a name="see-also"></a>Consulte Também  
[Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
