---
title: SQL Server, objeto Espelhamento de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Database Mirroring
- database mirroring [SQL Server], performance counters
- performance counters [SQL Server], database mirroring
- Database Mirroring object
ms.assetid: a27b51ee-7637-4525-9424-bcc16947dc13
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 639d661dd9a7196119bbb34f11f0ed5a9161a978
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67986682"
---
# <a name="sql-server-database-mirroring-object"></a>SQL Server, objeto Database Mirroring
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho **SQLServer:Database Mirroring** contém contadores de desempenho que relatam informações sobre o espelhamento de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A tabela a seguir lista os contadores contidos nesse objeto.  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|**Bytes Recebidos/s**|Número de bytes recebidos por segundo.|  
|**Bytes Enviados/s**|Número de bytes enviados por segundo.|  
|**Bytes de Log Recebidos/s**|Número de bytes de log recebidos por segundo.|  
|**Bytes de Log Refeitos do Cache/s**|Número de bytes de log refeitos, obtidos do cache de log de espelhamento, no último segundo.<br /><br /> Este contador é usado somente no servidor espelho. No servidor principal o valor é sempre 0.|  
|**Bytes de Log Enviados do Cache/s**|Número de bytes de log enviados obtidos do cache de log de espelhamento, no último segundo.<br /><br /> Este contador é usado somente no servidor de principal. No servidor espelho o valor é sempre 0.|  
|**Bytes de Log Enviados/s**|Número de bytes de log enviados por segundo.|  
|**Bytes Compactados de Log Recebidos/s**|Número de bytes de log compactados recebidos, no último segundo.|  
|**Bytes Compactados de Log Enviados/s**|Número de bytes de log compactados enviados, no último segundo.|  
|**Tempo de Intensificação do Log (ms)**|Milissegundos que os blocos de log aguardaram para serem intensificados no disco, no último segundo.|  
|**KB de Log Restante para Desfazer**|Total de quilobytes de log que permanecem para serem verificados pelo novo servidor espelho após failover.<br /><br /> Este contador é usado somente no servidor espelho durante a fase de desfazer. Após a conclusão da fase de desfazer, o contador é redefinido para  0. No servidor principal o valor é sempre 0.|  
|**KB de Log Verificado para Desfazer**|Total de quilobytes de log que foram verificados pelo novo servidor espelho desde a failover.<br /><br /> Este contador é usado somente no servidor espelho durante a fase de desfazer. Após a conclusão da fase de desfazer, o contador é redefinido para  0. No servidor principal o valor é sempre 0.|  
|**Tempo de Controle de Fluxo de Envio do Log**|Milissegundos que as mensagens do fluxo de log aguardaram para envio de controle de fluxo, no último segundo.<br /><br /> O envio de dados de log e metadados ao parceiro de espelhamento é a operação mais intensiva de dados em um espelhamento de banco de dados e pode monopolizar os buffers de envio do espelhamento de banco de dados e do Service Broker. Use este contador para monitorar o uso deste buffer por meio da sessão de espelhamento de banco de dados.|  
|**KB da Fila de Envio de Log**|Número total de quilobytes de log que ainda não foram enviados ao servidor espelho.|  
|**Transações de Gravação Espelhadas/s**|Número de transações que foram gravadas no banco de dados espelho e aguardaram que o espelho enviasse o log para confirmar, no último segundo.<br /><br /> Este contador só é incrementado quando o servidor principal estiver enviando ativamente registros de log ao servidor espelho.|  
|**Páginas Enviadas/s**|Número de páginas enviadas por segundo.|  
|**Recebimentos/s**|Número de mensagens espelhadas recebidas por segundo.|  
|**Refazer Bytes/s**|Número de bytes de log no qual foi efetuado roll forward no banco de dados espelho por segundo.|  
|**Refazer KB da Fila**|Número total de quilobytes de log intensificados que permanecem atualmente para serem aplicados para que o banco de dados espelho possa ser avançado. Isto é enviado ao principal a partir do espelho.|  
|**Enviar/Receber Tempo de Confirmação**|Milissegundos que as mensagens aguardaram pela confirmação do parceiro, no último segundo.<br /><br /> Este contador é útil para solucionar um problema que pode ser causado por um gargalo na rede, como failovers inexplicáveis, grandes filas de envio ou alta latência de transação. Nestes casos, você pode analisar o valor deste contador para determinar se a rede está causando o problema.|  
|**Envios/s**|Número de mensagens espelhadas enviadas por segundo.|  
|**Atraso na Transação**|Atraso na espera por reconhecimento de confirmação não terminado.|  
  
> [!NOTE]  
>  Em cada parceiro, alguns dos contadores mostram um valor zero dependendo de qual função o parceiro desempenha atualmente.  
  
## <a name="remarks"></a>Comentários  
 Os contadores de desempenho permitem que você monitore o desempenho de espelhamento de banco de dados. Por exemplo, você pode examinar o contador **Atraso na Transação** para verificar se o espelhamento de banco de dados está afetando o desempenho do servidor principal, você pode examinar os contadores **Fila de Restauração** e **Fila de Envio de Log** para verificar como o banco de dados espelho está se comportando em relação ao banco de dados principal. Você pode examinar o contador **Bytes de Log Enviados/s** para monitorar a quantidade de logs enviados por segundo.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
