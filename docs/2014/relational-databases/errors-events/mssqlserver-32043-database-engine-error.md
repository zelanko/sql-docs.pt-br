---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27b08927861e9222fe87ebb108d8595f63edb813
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551731"
---
# <a name="mssqlserver_32043"></a>MSSQLSERVER_32043
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|32043|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum32043|  
|Texto da mensagem|O alerta de 'log não restaurado' foi ativado. O valor atual '%d' ultrapassa o limite '%d'.|  
  
## <a name="explanation"></a>Explicação  
 Esse evento de espelhamento de banco de dados é emitido na instância do servidor espelho para indicar que a quantidade de logs não restaurados alcançou um valor do limite especificado pelo usuário. Normalmente, esse evento acontece porque o desempenho do sistema foi alterado. A largura da banda entre os dois sistemas diminuiu ou a carga aumentou.  
  
 Um log não restaurado é um log que foi recebido pela instância do servidor espelho e foi gravado no disco, mas está aguardando para ser restaurado no banco de dados espelho. A quantidade de logs não restaurados em KB (quilobytes) é uma métrica de desempenho que pode ajudar a avaliar o tempo atual de failover. O tempo necessário para aplicar o log não restaurado é o fator principal no tempo de failover, além de um curto período adicional necessário para restaurar o banco de dados e fazer com que ele fique online.  
  
> [!NOTE]  
>  Em um failover automático, o tempo necessário para que o sistema perceba a falha é independente do tempo de failover.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique a causa nas cargas das instâncias do servidor principal e espelho, bem como nas respectivas conexões de rede.  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
