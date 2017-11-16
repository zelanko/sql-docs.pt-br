---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 249182dd83285da77677ca9411aa83bc1b92e1e2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
  
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
  
## <a name="see-also"></a>Consulte também  
[Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
