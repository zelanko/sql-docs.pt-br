---
title: MSSQLSERVER_32040 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32040 (Database Engine error)
ms.assetid: 709219b1-f8b2-4696-8923-dd2e91492eb8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 198a58816388a1f5c80b45b776548508f01a1c73
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914263"
---
# <a name="mssqlserver32040"></a>MSSQLSERVER_32040
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|32040|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum32040|  
|Texto da mensagem|O alerta de 'transação não enviada mais antiga' foi ativado. O valor atual '%d' ultrapassa o limite '%d'.|  
  
## <a name="explanation"></a>Explicação  
 Esse evento de espelhamento de banco de dados é emitido na instância do servidor principal para indicar que a duração da transação mais antiga não enviada alcançou um valor de limite especificado pelo usuário. Normalmente, esse evento acontece porque o desempenho do sistema foi alterado. A largura da banda entre os dois sistemas diminuiu ou a carga aumentou.  
  
 A duração da transação mais antiga não enviada é uma métrica de desempenho que pode ajudar a avaliar o potencial de perda de dados mensurado pelo número de minutos das transações não enviadas. Essa métrica é especialmente relevante para sessões em modo de alto desempenho. No entanto, essa métrica também é relevante para uma sessão em modo de alta segurança, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique a causa nas cargas das instâncias do servidor principal e espelho, bem como nas respectivas conexões de rede.  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
